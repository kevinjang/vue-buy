<template>
  <div>
    {{name}}购物车
    <table border="1">
      <tr>
        <th></th>
        <th>课程名</th>
        <th>单价</th>
        <th>数量</th>
        <th>价格</th>
      </tr>
      <tr v-for="(c,i) in cart " :key="c.text" :class="{active:c.active}">
        <td>
          <input type="checkbox" v-model="c.active">
        </td>
        <td>{{c.text}}</td>
        <td>{{c.price}}</td>
        <td>
          <button @click="minus(i)">-</button>
          <span>{{c.count}}</span>
          <button @click="add(i)">+</button>
        </td>
        <td>{{c.price * c.count}}</td>
      </tr>
      <tr>
        <td colspan="3">{{activeCount}}/{{count}}</td>
        <td colspan="2">{{total}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  // name:"Cart"
  // props:['name','cart'],
  props: {
    name: {
      type: String,
      required: true
    },
    // cart: {
    //   type: Array
    // }
  },
  data() {
    return {
        cart:[]
    };
  },
  methods: {
    minus(i) {
      let count = this.cart[i].count;
      if (count > 1) this.cart[i].count -= 1;
      else this.remove(i);
    },
    add(i) {
      this.cart[i].count += 1;
    },
    remove(i) {
      if (window.confirm(`是否要删除课程${this.cart[i].text}?`)) {
        this.cart.splice(i, 1);
      }
    },
    setLocal(){
      window.localStorage.setItem('cart',JSON.stringify(this.cart));
    }
  },
  created(){
      this.cart = JSON.parse(window.localStorage.getItem('cart'))||[];

      this.$bus.$on('addCart',good=>{
          const ret = this.cart.find(v=>v.text == good.text);
          if(ret) {
              ret.count += 1;
          }
          else{
              this.cart.push({
                  ...good,
                  active:true,
                  count:1
              })
          }

        //   this.setLocal();
      });
  },
  watch:{
      cart: {
          handler(){
              this.setLocal();
          },
          deep:true
      }
  },
  computed: {
    count() {
      return this.cart.length;
    },
    activeCount() {
      return this.cart.filter(c => c.active).length;
    },
    total() {
      //   let num = 0;
      // this.cart.forEach(c => {
      //     if(c.active){
      //         num += c.price*c.count;
      //     }
      // });

      // return num;
      return this.cart.reduce((sum, v) => {
        if (v.active) {
          return sum + v.price * v.count;
        }
        return sum;
      }, 0);
    }
  }
};
</script>

<style>
table {
  border: 5px solid cyan;
  border-collapse: collapse;
}

tr {
  border: 5px solid cyan;
}
tr.active {
  color: red;
  font-weight: bolder;
}
</style>

