<template>

  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/article-svgrepo-com.svg" alt="site logo">
        <h1>
          Published Articles
        </h1>

      </div>
      <div class="order">

        <button @click="handleClick('title')"> Order by title </button>
        <button @click="handleClick('salary')">  Order by Salary </button>
        <button @click="handleClick('location')">  Order by Location </button>
      </div>
    </header>
    <JobList :jobs = "jobs" :order="order" />
  </div>
</template>

<script lang="ts">


import { defineComponent, reactive, ref, toRefs } from 'vue';
import Job from './Types/Job'
import OrderTerm from './Types/OrderTerm'
import JobList from './components/JobList.vue'


export default defineComponent({  //This function is from vue and it allows us to create components that works well with typescript
  name: 'App',
  components: { JobList },
    setup() {  // Using the composition api

      const jobs = ref<Job[]>([ // We are using generic to signify that this is an array of job objects
            { title: 'Farm worker ', location: "mountain of fire bustop", salary: 30000, id: '1'},
            { title: 'Footballer', location: "Okoko miako", salary: 6078000, id: '2'},
            { title: 'Super Hero ', location: "port-harcourt", salary: 33450000, id: '3'},
            { title: 'Parent ', location: "road 2 bustop", salary: 1000000, id: '4'},
            { title: 'Web developer', location: "rukpokwu new layout", salary: 987600000, id: '5'}
      ]);

      // Create a local state using a ref() to keep track of the OrderTerm that we choose 
      const order = ref<OrderTerm>('title')
      
      const handleClick = (term: OrderTerm) => {  // Only one of these three values: title, location or salary can be passed there
        order.value = term
      }

      return { jobs, handleClick, order } // Returning these functions so that we could them in the template above

  
      
    },

  //  Creating the methods property ton hold all our functions


});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;

  }
  header .title {
    display: flex;
    justify-content: center;
  }
  header img {
    width: 60px;
    margin-right: 20px;
  }
  header h1 {
    font-size: 3rem;
  }


</style>




<!--   
//   const state = reactive({  // Here we can pass in our data properties
  //     name: 'Aselemi',
  //     age: 26 as string | number // we are using type ascersion to explicitly tell vue that the property will be of a certain type.
  //   });

  //   // state.name = 89 annot change type 
  //   state.age = 89

  //   return { ...toRefs(state) } -->
