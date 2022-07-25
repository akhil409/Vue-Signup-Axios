<template>
     <div>
    <div class="fromData">
      <p>UserName:- {{formValues.UserName}}</p> 
      <p> E-Mail:-  {{formValues.EMail}}</p>
      <p>Password:- {{formValues.Password}}</p> 
      <p>Password Confirm:- {{formValues.PasswordConfirm}}</p> 
      <p>Role:- {{formValues.Role}}</p>
      <p>Terms:- {{formValues.Terms}}</p>
      <p>Names CheckBox:-{{formValues.Names}}</p> 
      <p>Text Area Data:- {{formValues.textarea}}</p> 
      <p>Radio Buttons:- {{formValues.gender}}</p> 
      <p>Selected: {{ formValues.selected }}</p> 
      <p>Age:- {{formValues.age}}</p>  
    </div>
    <!-- <div>
        <pre>{{ JSON.stringify(formValues, null, 2) }}</pre>
    </div> -->
    
    <div class='container'>
      <form @submit.prevent="handleSubmit" id="form">
        <div class="alert alert-success" v-if="isSuccess">Details Submitted Successfully</div>
       <h1>Registration Form</h1>
       <div> <hr /> </div>
       <div>
           <div>
               <label for="UserName">UserName:-</label> 
               <input type="text" 
                      v-model="formValues.UserName"
                      placeholder='UserName'
                      required
                      class="form-control"
                      id="UserName"/>
           </div>
           <!-- Conditional Rendering -->
           <p v-if="formValues.UserName.length == 0" class="formError">This field is required!</p>
           <p v-else-if="formValues.UserName.length < 4" class="formError">Lenght should be more that 4 Chars</p>
           <p v-else-if="formValues.UserName.length > 20" class="formError">Lenght should not be exceed 20 Chars</p>
           <p v-else id="usernameCon">Strong Username</p>
            <br>
           <div>
               <label >E-Mail:-</label>
               <input type="email" 
                      v-model="formValues.EMail"
                      placeholder="E-Mail"
                      
                      class="form-control"
                      />
           </div>
           <br>
 
            <div>
               <label for="Profile-Summary">Profile Summary:-</label>
               <textarea type="text" 
                      v-model="formValues.textarea"
                      placeholder="Summary"
                      
                      class="form-control"
                      id="Profile-Summary"
                      />
           </div>
           <br>

           <div>
               <label >Password:-</label>
               <input type="password" 
                      v-model.number="formValues.Password"
                      placeholder="Password"
                      
                      class="form-control"
                      />
           </div>
           <div v-if="formValues.passwordError" class="error">{{ formValues.passwordError }}</div>
           <br>
           <div>
               <label >Password Confirm:-</label>
               <input type="password" 
                      v-model="formValues.PasswordConfirm"
                      placeholder="Password Confirm"
                      
                      class="form-control"
                      />
           </div>
           
           <br>
            <div>
               <label for="role">Role:-</label>
                   <select multiple v-model="formValues.Role" class="form-control" id="role" >
                       <option disabled value="">Select Role</option>
                       <option value="Web Designer" >Web Designer</option>
                       <option value="Web Developer" >Web Developer</option>
                       <option value="Tester" >Tester</option>
                       <option value="Project Manager" >Project Manager</option>
                   </select>
            </div>
           <br>
             <div>
               <label for="count">Country:-</label>
                   <select multiple v-model="formValues.country" class="form-control" id="count" >
                       <option value="india" >India</option>
                       <option value="singapore" >Singapore</option>
                       <option value="america" >America</option>
                       <option value="russia" >Russia</option>
                   </select>
            </div>
            <br>

            <div>
                <label for="age">Age:-</label>
                <input id="age" type="number" 
                      v-model="formValues.age" 
                      placeholder="Enter your age"
                      
                      class="form-control">
            </div>

           <div>
                 <label class='filedCB'>Skills:-</label>
                 <input type="text" v-model="formValues.tempSkill" @keypress.alt="addSkill" class="form-control" >   
            </div>
            <div v-for="skill in formValues.skills" :key="skill.value" class="pill">
                <span @click="skillDelete(skill)">{{ formValues.skill }}</span>  
            </div>
            <br>
            <div>
                 <input type="checkbox" v-model="formValues.Terms"  >
                 <label class='filedCB'>ACCEPT TERMS AND CONDITIONS</label>
            </div>

             <div>
                 <input type="checkbox" value="Akhil"  v-model="formValues.Names">
                 <label class='filedCB'>Akhil</label>
            </div>
            <div>
                 <input type="checkbox" value="Alladi"  v-model="formValues.Names">
                 <label  class='filedCB'>Kumar</label>
            </div>
            <div>
                 <input type="checkbox" value="Kumar" v-model="formValues.Names">
                 <label  class='filedCB'>Alladi</label>
            </div>
             <br>
            <!-- Radio Buttons -->
            <label for="">Gender:-</label> <br>
            <div>
               <input type="radio" value="male" v-model="formValues.gender"/>    
               <label for="male">Male</label>
            
               <input type="radio" value="female" v-model="formValues.gender"/>    
               <label for="female">Female</label>
            </div> 

            <!-- Select options can be dynamically rendered with v-for: -->
            <select multiple v-model="formValues.selected">
               <option v-for="option in formValues.options" v-bind:key="option.value">
                {{ option.text }}
                </option>    
            </select> 
            <br>  

            <!-- DropDown Effect  
            <AppDropDown>
                   <template>
                      <button>Toggle</button>
                   </template>
                   <AppDropdownContent>
                            <AppDropdownItem>Python Developer</AppDropdownItem>
                            <AppDropdownItem>MEAN Stack</AppDropdownItem>
                            <AppDropdownItem>React Developer</AppDropdownItem>
                   </AppDropdownContent>
            </AppDropDown> -->

           <button type="submit" class="form-control btn btn-primary" id="btnsubmit">Create An Account</button>
           
       </div>
     </form>
    </div>
</div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
Vue.use(VueAxios, axios);

export default {
    name:'SignUpForm',
    data(){
        return{
            formValues:{
                        UserName:"",
                        EMail:"",
                        textarea:"",
                        Password:"",
                        PasswordConfirm:"",
                        Role:"",
                        age:[],
                        Terms:false,
                        Names: [],
                        gender:'',
                        tempSkill:"",
                        skills:[],
                        passwordError:"",
                        country:'',
                        selected:[],
                        options:[
                            {text:'One',value:'A'},
                            {text:'Two',value:'B'},
                            {text:'Three',value:'C'}]
                        
                        },
                        isSuccess:false
                        
            
        }
    },
    methods:{
        addSkill(e){
            if(e.key==="," && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                      this.skills.push(this.tempSkill)
                }                
                this.tempSkill=""
            }
        },
    skillDelete(skill){
          this.skills = this.skills.filter((item)=>{
            return skill !== item
          })
    },
    // Posting details to the Firebase
    handleSubmit(){
        // this.passwordError = this.Password.length < 5 ? "Password should be 6 chars long":""
        
        // if(!this.passwordError){
        //     console.log("Username is",this.UserName)
        //     console.log("Email is ",this.EMail);
        //     console.log("Role",this.Role);
        //     console.log("Skills are",this.skills);
        // }

        axios.post(`https://samplerequests-620b4-default-rtdb.firebaseio.com/posts.json`,{ UserName: this.formValues.UserName, 
                                                                                           EMail: this.formValues.EMail,
                                                                                           Password: this.formValues.Password,
                                                                                           PasswordConfirm: this.formValues.PasswordConfirm,
                                                                                           Role: this.formValues.Role,
                                                                                           Terms: this.formValues.Terms,
                                                                                           Names: this.formValues.Names,
                                                                                           textarea: this.formValues.textarea,
                                                                                           gender: this.formValues.gender,
                                                                                           selected: this.formValues.selected ,
                                                                                           age: this.formValues.age })
            .then((res)=>{
                     this.isSuccess = true;
                     console.log('Details Submitted to Firbase successfully',res);
                     this.$emit('postCreated')
            }).catch((err)=>{
                     console.log('Error while Posting Data to Firebase',err);
            })
        
    },

    mounted(){
        this.handleSubmit();
    }
    

  }
    
}
</script>

<style>
    * {
          box-sizing: border-box;
      }

  body {
    background: rgb(2, 0, 36);
    background: radial-gradient(
      circle,
      rgba(2, 0, 36, 1) 0%,
      rgba(30, 54, 59, 1) 0%,
      rgba(93, 93, 116, 1) 100%
    );
  }

.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    max-width: 500px;
    margin: auto;
    color: black;
    
}

.container > form{
   width: 45%;
   height:100vh;
   overflow-y:hidden;
   padding: 20px;
   border: 2px solid #dfdfdf;
   border-radius: 5px;
   background: #fff;
}

.container > form:hover{
    overflow-y: scroll ;
}

pre{
    width: 70%;
    color: white;
    font-size: large;
    margin-left: 50%;
    
}

/* .btn{
    background: #0b6dff;
    color: whitesmoke;
    padding: 20px;
    margin-top: 20px;
    border-radius: 20px ;
    border: 0;
} */

.msg-success{
    background-color: aqua;
    color: darkgreen;
    border-radius: 5px;
    margin-bottom: 10px;
    width: 22%;
    height: 8vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.fromData{
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    color: darkgoldenrod;
   
}

.filedCB{
    padding-left: 10px;
    
}

#form{
    margin-bottom: 2rem;
}

#btnsubmit{
    margin-top: 1rem;
}

.pill{
    display:inline-block;
    margin:  20px 10px 0 0;
    padding: 6px 12px;
    background-color: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}

.error{
     padding-top: 10px;
     color: red;
     font-weight: bold;
     font-size: 0.8rem;
}

/* Conditional Rendering */
.formError{
    color: red;
    font-weight: bold;
}
#usernameCon{
    color: green;
    font-weight: bold;
}
</style>