<template id="app">
       <div id="container">
            <div class="row">
              <div class="col-md-12">
                  <div>
                      <SignUpForms @postCreated="onCreatePost" />
                  </div>
                  <div class="my-2" v-if="showPosts">
                      <PostDetails />
                  </div>
              </div>
            </div>           
       </div>   
</template>

<script>
import SignUpForms from './components/SignUpforms.vue'
import PostDetails from './components/PostDetails.vue'


export default{
  name:"App",
  components:{
    SignUpForms,
    PostDetails
},

  data(){
    return{
          showPosts:true,
    }
  },
  methods:{
        onCreatePost(){
        this.showPosts = false;
        setTimeout(() => {
         this.showPosts = true;   
        }, 50);
    }
  }
}

</script>

<style scoped>
 

</style>


<!--
<template>
  <div class="container">
      <div id="bck">
           <SampleCode1 />
      </div>
  </div>
</template>

<script>
import SampleCode1 from './components/SampleCode1.vue'

export default {
    name:"App",
    components:{
    SampleCode1
}

}
</script>

<style>

#bck{
  margin-top: 10rem;
  background-color: aqua;
}

</style>

-->



