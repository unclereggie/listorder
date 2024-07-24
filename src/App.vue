<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" ></JobList>/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobList from './components/JobList.vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'

export default defineComponent({
  name: 'App',
  components: { JobList},
  setup(){
    /*const state = reactive({
      name: "Link",
      age: 25 as number | string    
    })

    return { ...toRefs(state)}
    */
    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary:30000, id:'1'},
      { title: 'quarryman', location: 'dinamark', salary:45000, id:'2'},
      { title: 'flute player', location: 'paris', salary:10000, id:'3'},
      { title: 'fisherman', location: 'spain', salary:100000, id:'4'},
    ])

    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) =>{
      order.value = term
    }

    return {jobs, handleClick, order}
  },
});
</script>

<style>
  header{
    text-align: center;
  }
  header .order{
    margin: 20px;
  }
  button{
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>
