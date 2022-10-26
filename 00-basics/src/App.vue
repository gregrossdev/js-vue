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

</script>

<template>

  <h1>{{ message }}</h1>
<!--  // Handling User Input-->
  <button @click="reverseMessage">Reverse Message</button>
  <button @click="message += '!'">Append "!"</button>
  <a href="https://vuejs.org" @click.prevent="notify">
    A link with e.preventDefault()
  </a>
<!--  // Attribute Bindings-->
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
</template>

<style>
button, a {
  display: block;
  margin-bottom: 1em;
}
.red {
  color: red;
}
</style>