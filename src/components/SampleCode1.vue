<template>
       <div id="div">
            <div v-if="showData">
             <p>My name is {{name}} and i am {{age}} years old and i am from {{place}}</p>
             <p>Increment:- {{increment}}  and Decrement:- {{decrement}}</p>
             <p>Prement Location:- {{Location}}</p>
            </div>

             <button @click="changeName">Change Name</button>
             <button @click="changeAge">Change Age</button>
             <button @click="changePlace">Change Place</button>
              <!-- Increment and Decrement  -->
             <button @click="increment++">Increment</button>
             <button @click="decrement--">Decrement</button>
            <!-- Arguments passing method -->
             <button @click="changeLocation('Hyderabad')">Change Location</button>
             <!-- Conditional Rendering using directives -->
             <button @click="toggleShowData">
                    <span v-if="showData">Hide Data</span>
                    <!-- <span v-if="!showData">Show Data</span> -->
                    <span v-else>Show Data</span>
             </button>
             <!-- We can use v-show instead of v-f also (v-if removes and add elements in the DOM & v-show just hidden the conetent but it takes place in DOM)-->
             <div v-show="showData">Show Directive Data </div>
             
       </div>
</template>

<script>

export default {
    name:"SampleCode1",
    components:{
     
      },
    data(){
          return{
               name:"Alladi",
               age:"27",
               place:"Hyderabad",
               increment:0,
               decrement:0,
               Location:"Chirala",
               showData:true,
          }
    },
    methods:{
            changeName(){
              this.name="Akhil"
            },
            changeAge(){
              this.age=19
            },
            changePlace(){
              this.place="Bangalore"
            },
            changeLocation(locate){
               this.Location = locate
            },
            toggleShowData(){
              this.showData = !this.showData
            }
    }

}
</script>

<style>
   * {
    box-sizing: border-box;
  }
</style>