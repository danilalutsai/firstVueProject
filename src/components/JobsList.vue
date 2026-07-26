<script setup lang="ts">

// To go to the root of the project use @
import type { Job } from '@/types/Job';
import type { OrderTerm } from '@/types/OrderTerm';
import { computed } from 'vue';

const props = withDefaults(defineProps<{
  order: OrderTerm
  jobs: Job[]
}>(), { order: 'title' });

const orderedJobs = computed(() => {
  return [...props.jobs].sort((a, b) => (a[props.order] > b[props.order] ? 1 : -1));
});

</script>

<template>
  <!-- The key give each copy a stable tag -->
  <p>Ordered by {{ order }}</p>
  <div v-for="job in orderedJobs" :key="job.id" class="job">
    <h2>{{ job.title }}</h2>
    <h3>{{ job.location }} - {{ job.salary }}</h3>
    <p>{{ job.description }}</p>
  </div>
</template>

<style scoped>
.job {
  padding: 1.25rem 1.5rem;
  margin-bottom: 1rem;
  background: #fff;
  border: 1px solid #e0e0e0;
  border-left: 5px solid #42b883;
  border-radius: 8px;
}

.job h2 {
  margin: 0 0 0.25rem;
  color: #42b883;
  font-size: 1.3rem;
}

.job h3 {
  margin: 0 0 0.75rem;
  color: #666;
  font-size: 1rem;
  font-weight: 500;
}

.job p {
  margin: 0;
  color: #333;
  line-height: 1.6;
}
</style>
