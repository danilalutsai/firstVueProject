<script setup lang="ts">
import { reactive, ref } from 'vue';
import type { Job } from './types/Job.ts';
import type { OrderTerm } from './types/OrderTerm.ts';
import JobsList from './components/JobsList.vue';

// With ref() we use <generic type> argument instead of type assertion : type
const message = ref<string>('Hello, hyrule');
const name = ref<string>('Link');

// We don't pass ref() if it is a value that we will never change or use interactively
// With ref() we wrap any value (primitives and objects). You access it via .value in the script
const age = ref<number>(25);
const count = ref<number>(0);

// With reactive() we wrap only objects/arrays (not primitives). No .value -> you use it directly
// If you access variable with reactive() you access properties not wrapped -> object.property (syntax)
const state = ref({ count: 0 as number, name: 'Josh' as string });

// Passing the types in the object with -> as type-name
const object = {
  name: "Danila" as string,
  age: 25 as number,
}

const jobs = ref<Job[]>([
{ id: 'id1', title: 'Farm Worker', location: 'Lon Lon Ranch', salary: 30000, description: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since 1966, when designers at Letraset and James Mosley, the librarian at St Bride Printing Library in London, took a 1914 Cicero translation and scrambled it to make dummy text for Letrasets Body Type sheets." },
{ id: 'id2', title: 'Quarryman', location: 'Death Mountain', salary: 40000, description: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since 1966, when designers at Letraset and James Mosley, the librarian at St Bride Printing Library in London, took a 1914 Cicero translation and scrambled it to make dummy text for Letrasets Body Type sheets."},
{ id: 'id3', title: 'Flute Player', location: 'The Lost Woods', salary: 35000, description: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since 1966, when designers at Letraset and James Mosley, the librarian at St Bride Printing Library in London, took a 1914 Cicero translation and scrambled it to make dummy text for Letrasets Body Type sheets." },
{ id: 'id4', title: 'Fisherman', location: 'Lake Haliya', salary: 21000, description: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since 1966, when designers at Letraset and James Mosley, the librarian at St Bride Printing Library in London, took a 1914 Cicero translation and scrambled it to make dummy text for Letrasets Body Type sheets." },
{ id: 'id5', title: 'Prison Guard', location: 'Gerudo Valley', salary: 32000, description: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since 1966, when designers at Letraset and James Mosley, the librarian at St Bride Printing Library in London, took a 1914 Cicero translation and scrambled it to make dummy text for Letrasets Body Type sheets." },
]);

const order = ref<OrderTerm>('title');

function handleClick(term: OrderTerm) {
  order.value = term;
}

// Using composition API from -> ref() -> .value
function add() {
  count.value++
  console.log(count.value);
}

function modifyState() {
  state.value.count++;
  state.value.name = 'Danila';
}

function changeAge(newAge: number) {
  age.value = newAge;
}

function changeName(newName: string) {
  name.value = newName;
}

console.log(count.value);
</script>

<template>
  <header>
  </header>

    <main>
      <div class="app">
      <div class="button-row">
        <button @click="handleClick('title')">Order by title</button>
        <button @click="handleClick('salary')">Order by salary</button>
        <button @click="handleClick('location')">Order by location</button>
      </div>
      <JobsList :order="order" :jobs="jobs"/>

      <p>His name is {{ name }} and is {{ age }} years old and the count is {{ count }}.</p>

      <p>First worker is {{ jobs[0]?.title }}.</p>

      <button @click="changeName('Danila')">Change name</button>
      <button @click="changeAge(42)">Change age</button>
      <button @click="add">Count: {{ count }}</button>
      <button @click="modifyState">Count + and change name</button>

      <!-- With the reactive keyword you have to access the data with full name-of-object.name-of-property -->
      <p>The count is {{ state.count }} and name is {{ state.name }}.</p>

      </div>
    </main>
</template>

<style scoped>
main {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem 1rem;
  font-family: system-ui, sans-serif;
}

.app {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.app p {
  margin: 0;
  color: #333;
  line-height: 1.5;
}

.button-row {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

button {
  align-self: flex-start;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 6px;
  background: #42b883;
  color: #fff;
  font-size: 0.95rem;
  cursor: pointer;
  transition: background 0.15s ease;
}

button:hover {
  background: #369870;
}
</style>
