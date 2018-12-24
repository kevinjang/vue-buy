<template>
<div>
    
    <table>
        <tr>
            <th>课程名</th>
            <th>单价</th>
            <th>数量</th>
            <th>价格</th>
        </tr>
        <tr v-for="c in cart" :key="c.text">
            <td>
                {{c.text}}
            </td>
            <td>
                {{c.price}}
            </td>
            <td>
                {{c.count}}
            </td>
            <td>
                {{c.price * c.count}}
            </td>
        </tr>
    </table>

</div>
</template>

<script>
 export default {
    name:'Cart',
    props:{
        name : {
            type: String,
            required: true
        },
            cart:{
                type: Array
            }
        },
    data(){
        return {
            // name:{
            //     type:String,
            //     required:true
            // }
        }
    },
    created(){
        // this.$bus.$on('addCart',good=>{
        //     this.cart = [];
        //     const ret = this.card.find(v=>v.text == good.text);
        //     if(ret){
        //         ret.count +=1;
        //     }else{
        //         this.card.push({
        //             ...good,
        //             active:true,
        //             count:1
        //         })
        //     }
        // })
    },
    methods:{
    }
 }
</script>

<style>

</style>