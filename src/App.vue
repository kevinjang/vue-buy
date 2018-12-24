<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    
    <div>
        {{name}}购物车
    </div>

    <ul>
      <li v-for='(good, index) in goods' :key="good.text">
        {{good.text}}
        <button @click="addCart(index)">添加到购物车</button>
        </li>
    </ul>

    <!-- <input type="text" v-model="text">
    <button @click="addGood">添加课程</button> -->
    

    <Cart :name="name" :cart="cart"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Cart from './components/Cart.vue'

export default {
  name: 'app',
  components: {
    // HelloWorld,
    Cart
  },
  // props:['name',"cart"],
  // props:{
  //   text:String
  // },
  // props:{
  //   fatherName :{
  //     type: String 
  //   },
  //   goods:[{text:'百万年薪架构师'}]
  // },
  data(){
    return {
      text:'',
      name:'开课吧',
            goods:[
                {text:'百万年薪架构师',price:100,count:0},
                {text:'web全栈架构师',price:80,count:0},
                {text:'Python爬虫',price:60,count:0},
                {text:'Java架构师',price:70,count:0},
            ]
    }
  },
  created(){
    // this.fatherName = '开课吧';
  },
  mounted(){
    // this.fatherName = '开课吧';
  },
  methods:{
        addCart(i){
            const good = this.goods[i];
            console.log(typeof this.cart);
            const ret = this.cart.find(c=>c.text == good.text);

            if(ret){
                ret.count += 1;
            }else{            
                cart.push({
                    ...good,
                    active:true,
                    count:1
                })
            }

        // console.log(cart);
        // this.$bus.$emit('addCart',good);
        },
    addGood(){
      if(this.text){
        this.goods.push({
          text:this.text
        });
        this.text = '';
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
