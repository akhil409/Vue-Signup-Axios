<template>
       <header>
             <h1 id="app"> {{title}} </h1>
       </header>
</template>

<script>
export default {
    name:"SampleCode",
    props:{
        title:String,
    },
}
</script>

<style scoped>
   #app{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 5rem 5rem;
   }

</style>
