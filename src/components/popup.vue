<template>
  <h1>This is a popup</h1>
  <input type="text" v-model="name">
  <button @click="$emit('close',name)">Close popup</button>
</template>

<script>
export default {
name:'pop-up',
// emits:['close']
emits:{
    close:(name)=>{
if(!name)
{
    return false
}
else
{
    return true
}
    }
},
data(){
    return{
        name:''
    }
}
}
</script>

<style>

</style>