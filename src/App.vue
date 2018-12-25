<template>
  <!-- <div v-if="showName">{{name}}</div> -->
  <div>
    <!-- {{name}}
    
    -->
    <!-- 
<input type="text" v-model="text">
    <button @click="addGood">添加</button>-->
    <ul>
      <li v-for="(good,index) in goods" :key="good.text">
        {{good.text}} ￥{{good.price}}
        <button @click="addCart(index)">添加购物车</button>
      </li>
    </ul>

    <hr>
    <Cart :name="name" ></Cart>
  </div>
</template>

<script>
import Cart from "./components/Cart";
import axios from "axios";
export default {
  name: "app",
  components: {
    Cart
  },
  data() {
    return {
      name: "开课吧",
      showName: true,
      text: "",
      //购物车
      // cart: [],
      goods: []
    };
  },
  async created() {
    // 组件创建后会自动执行once
    // setTimeout(() => {
    //   this.showName = false;
    // }, 2000);
    try {
      const ret = await axios.get("/api/goods");
      this.goods = ret.data.list;
    } catch (err) {}

    // axios.get("/api/goods").then(res => {
    //   this.goods = res.data.list;
    // }).catch(err=>{
    //   alert(err)
    // });
  },
  methods: {
    addGood() {
      if (this.text) {
        this.goods.push({ text: this.text });
      }
    },
    addCart(i) {
      // const good = this.goods[i]; //this.cart.find(v=>v.text ==)
      // const ret = this.cart.find(v => v.text == good.text);

      // if (ret) {
      //   ret.count += 1;
      // } else {
      //   this.cart.push({
      //     ...good,
      //     active: true,
      //     count: 1
      //   });
      // }
      const good = this.goods[i];
      // 触发一个事件
      this.$bus.$emit("addCart", good);
    }
  }
};
</script>

<style>
</style>


