<script setup lang="ts">
import { reactive, ref } from 'vue'
import type Job from './types/Job'

// With ref() we use <generic type> argument instead of type assertion : type
const message = ref<string>('Hello, hyrule');
const name = ref<string>('Link');

// We don't pass ref() because is a value that we will never change or use interactively
// With ref() wraps any value (primitives and objects). You access it via .value in the script
const age = ref<number>(25);
const count = ref<number>(0);

// With reactive() wraps only objects/arrays (not primitives). No .value, you use it directly
// If you access variable with reactive() you access properties not wrapped -> object.property (syntax)
const state = reactive({ count: 0 as number, name: 'Josh' as string });

// Passing the types in the object with -> as type-name
const object = {
  name: "Danila" as string,
  age: 25 as number,
}

const jobs = ref<Job[]>([{ id: 'id1', title: 'machinist', location: 'Tallinn', salary: 500 }]);

// Using composition API from -> ref() -> .value
function add() {
  count.value++
  console.log(count.value);
}

function modifyState() {
  state.count++;
  state.name = 'Danila';
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

      <p>His name is {{ name }} and is {{ age }} years old and the count is {{ count }}.</p>

      <p>First worker is {{ jobs[0]?.title }}.</p>

      <button @click="changeName('Danila')">Change name</button><br><br>
      <button @click="changeAge(42)">Change age</button><br><br>
      <button @click="add">Count: {{ count }}</button><br><br>
      <button @click="modifyState">Count + and change name</button><br><br>

      <!-- With the reactive keyword you have to access the data with full name-of-object.name-of-property -->
      <p>Name is {{ state.count }} and name is {{ state.name }}.</p>

      </div>
    </main>
</template>

<style scoped>
</style>
