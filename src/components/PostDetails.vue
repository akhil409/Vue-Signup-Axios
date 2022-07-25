<template>
       <v-container>
            <v-row class="text-center">
                <h1>Posted User Data</h1>
                    <div>
                     <button @click="display=!display" class="btn btn-info">
                          <span v-if="!display">Show Data</span>
                          <span v-else>Hide Data</span>
                     </button>
                     <table class="table table-bordered table-striped mt-5" v-if="display">
                          <thead>
                             <tr>
                                            <th>Username</th>
                                            <th>Email</th>
                                            <th>Profile Summary</th>
                                            <th>Password</th>
                                            <th>Password Confirm</th>
                                            <th>Role</th>
                                            <th>Age</th>                                            
                                            <th>Gender</th>
                                            <th>Country</th>
                                            <th>Selected</th>
                                            <th>Options</th>
                             </tr>
                          </thead>
                          <tbody>
                             <tr v-for="(value,index) in postDetails"  :key="index">
                                          <td v-text="value.UserName"> </td>
                                          <td v-text="value.EMail"></td>
                                          <td v-text="value.textarea"> </td>
                                          <td v-text="value.Password"> </td>
                                          <td v-text="value.PasswordConfirm"> </td>
                                          <td v-text="value.Role"> </td>
                                          <td v-text="value.age"> </td>
                                          <td v-text="value.gender"> </td>
                                          <td v-text="value.country"> </td>
                                          <td v-text="value.selected" ></td>
                                          <td v-text="value.options" ></td>
                                          
                                          
                            </tr>
                        </tbody>
                    </table>
                </div>
            </v-row>
       </v-container>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
Vue.use(VueAxios, axios);

export default {
       name:'PostDetails',
       data(){
          return{
            display:false,
            postDetails:[],
            showPosts:true,
          }
       },
       methods:{
        getUsers: function() {
                          axios.get(`https://samplerequests-620b4-default-rtdb.firebaseio.com/posts.json`).then((response)=>{
                            //    this.fakeData = response.data
                               console.log(response.data)
                               this.formatePostDetails(response.data)
                          }).catch((error)=>{
                           console.log('Error while fetching Data',error)
                          }).finally(()=>{
                           console.log('Loading Data completed');
                          })
    },
    formatePostDetails(posts){
         for(let key in posts){
            this.postDetails.push({ ...posts[key], id:key })
         }
         console.log(this.postDetails);
    },
       },
       mounted(){
              this.getUsers();
       },
       
}
</script>

<style>

</style>