<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in OrderedJobs" :key="job.id">
        <h2>{{ job.title }} - {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Odit
            provident dolor magni perspiciatis velit nulla itaque quia, earum
            nemo, obcaecati modi cum, ab est repellendus. Magni omnis laboriosam
            dignissimos veritatis
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order:{
        required: true,
        type:String as PropType<OrderTerm>
    }
  },
  setup(props){
    const OrderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) =>{
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return {OrderedJobs}
  }
});
</script>

<style scoped>
    .job-list{
        max-width: 960px;
        margin: 40px auto;
    }
    .job-list ul{
        padding: 0;
    }
    .job-list li{
        list-style-type: none;
        background: #fff;
        padding: 16px;
        margin: 16px 0;
        border-radius: 4px;
    }
    .job-list h2{
        margin: 0 0 10px;
        text-transform: capitalize;
    }
    .salary{
        display: flex;
    }
    .salary img{
        width: 30px;
    }
    .salary p{
        color: #17bf66;
        font-weight: bold;
        margin: 10px 4px;
    }
    .list-move{
      transition: all 1s;
    }
</style>
