<template>
  <h1>{{childname}} {{secondChild}}</h1>
  <button @click="showpopup=true">Open PopUp</button>
  <!-- v-show directives not working have to check -->
  <!-- <popup v-if="showpopup"  @close="showpopup=false" /> -->
  <!-- or -->
  <popup v-if="showpopup"  @close="Isshow" />
  <second/>
</template>

<script>
const second = require("./child2.vue")
import popup from './popup.vue'
// import second from './child2.vue'

export default {
    name:'first-child-name',
    props:{
    childname:String,
    secondChild:String
    },
// or
// props:['childname','secondChild']
components:{
popup,second
},
data(){
  return{
    showpopup:false
  }
},
methods:{
  Isshow(value){
    this.showpopup=false,
console.log('Myname is',value)
  }
}
}
</script>

<style>

</style>