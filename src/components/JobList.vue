<template>
    <div class="job-list">
        <h2> Ordered by {{ order }}</h2>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2> {{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>{{ job.salary }} Naira </p>
                </div>
                <div class="description">
                    <p> Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eum optio fugit a qui nihil officia, ad aut, nobis recusandae incidunt quo molestiae tenetur veritatis ex, neque ullam earum? Non, quibusdam.</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/Types/Job'
import OrderTerm from '@/Types/OrderTerm';

export default defineComponent({
    props: {
        jobs: {
            required: true,
            type: Array as PropType<Job[]> // we are using type ascersion to say that this is an array of job
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },
    // Will be using a computed value. We first need a setup function
    setup(props) {
        const orderedJobs = computed(() => {  // this takes in a function as an argument that will ultimately return the computed jobs
        // This computed method will watch any props or reactive value that is used in this function. so we can rerun anytime the value changes

            return [...props.jobs].sort((a: Job, b:Job) => {
                return a[props.order] > b[props.order] ? 1 : -1
            }) 
        })

        return { orderedJobs }
    }
})
</script>

<style >
    .job-list {
        max-width: 960px;
        margin: 40px auto;
    }
    .job-list ul {
        padding: 0;
    }
    .job-list li {
        list-style: none;
        background: white;
        padding: 16px;
        margin: 16px 0;
        border-radius: 4px;
    }
    .job-list h2 {
        margin: 0 0 10px;
        text-transform: capitalize;
    }
    .salary {
        display: flex;
    }
    .salary img {
        width: 30px;
    }
    .salary p {
        color: #17bf66;
        font-weight: bold;
        margin: 10px 4px;
    }
    .list-move{
        transition: all 1s;
    }

</style>
