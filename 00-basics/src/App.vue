<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')

// Handling User Input
function reverseMessage() {
  // Access/mutate the value of a ref via its .value property.
  message.value = message.value.split('').reverse().join('')
}

function notify() {
  alert('navigation was prevented.')
}

// Attribute Bindings
const isRed = ref(true)
const color = ref('green')

function toggleRed() {
  isRed.value = !isRed.value
}

function toggleColor() {
  color.value = color.value === 'green' ? 'blue' : 'green'
}

// Conditionals and Loops
const show = ref(true)
const list = ref([1, 2, 3])

</script>

<template>

  <h1>{{ message }}</h1>

<!--  // Handling User Input-->
  <section>
    <div class="buttons">
      <button @click="reverseMessage">Reverse Message</button>
      <button @click="message += '!'">Append "!"</button>
    </div>
    <a href="https://vuejs.org" @click.prevent="notify">
      A link with e.preventDefault()
    </a>
  </section>

<!--  // Attribute Bindings-->
  <section>
    <p>
    <span :title="message">
      Hover your mouse over me for a few seconds to see my dynamically bound title!
    </span>
    </p>

    <p :class="{ red: isRed }" @click="toggleRed">
      This should be red... but click me to toggle it.
    </p>

    <p :style="{ color }" @click="toggleColor">
      This should be green, and should toggle between green and blue on click.
    </p>
  </section>

<!--  // Conditionals and Loops-->
  <section>
    <div class="buttons">
      <button @click="show = !show">Toggle List</button>
      <button @click="list.push(list.length + 1)">Push Number</button>
      <button @click="list.pop()">Pop Number</button>
      <button @click="list.reverse()">Reverse List</button>
    </div>

    <ul v-if="show && list.length">
      <li v-for="item of list">{{ item }}</li>
    </ul>
    <p v-else-if="list.length">List is not empty, but hidden.</p>
    <p v-else>List is empty.</p>
  </section>


</template>

<style>
button, a {
  display: block;
  margin-bottom: 1em;
}

section {
  padding: 1rem 0;
}

.red {
  color: red;
}

.buttons {
  display: flex;
}
</style>