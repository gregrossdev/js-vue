<script setup>
import {ref} from 'vue'

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

// Form Bindings
const text = ref('Edit me')
const checked = ref(true)
const checkedNames = ref(['Jack'])
const picked = ref('One')
const selected = ref('A')
const multiSelected = ref(['A'])

</script>

<template>

  <main>
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


    <!--  // Form Bindings-->
    <section class="row">
      <div class="box">
        <h2>Text Input</h2>
        <input v-model="text">
        <p>{{ text }}</p>
      </div>

      <div class="box">
        <h2>Checkbox</h2>
        <input id="checkbox" v-model="checked" type="checkbox">
        <label for="checkbox">Checked: {{ checked }}</label>
      </div>

      <!--multiple checkboxes can bind to the same array v-model value-->
      <div class="box">
        <h2>Multi Checkbox</h2>
        <input id="jack" v-model="checkedNames" type="checkbox" value="Jack">
        <label for="jack">Jack</label>
        <input id="john" v-model="checkedNames" type="checkbox" value="John">
        <label for="john">John</label>
        <input id="mike" v-model="checkedNames" type="checkbox" value="Mike">
        <label for="mike">Mike</label>
        <p>Checked names:</p>
        <pre>{{ checkedNames }}</pre>
      </div>

      <div class="box">
        <h2>Radio</h2>
        <input id="one" v-model="picked" type="radio" value="One">
        <label for="one">One</label>
        <br>
        <input id="two" v-model="picked" type="radio" value="Two">
        <label for="two">Two</label>
        <br>
        <span>Picked: {{ picked }}</span>
      </div>

      <div class="box">
        <h2>Select</h2>
        <select v-model="selected">
          <option disabled value="">Please select one</option>
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select>
        <span>Selected: {{ selected }}</span>
      </div>

      <div class="box">
        <h2>Multi Select</h2>
        <select v-model="multiSelected" multiple style="width:100px">
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select>
        <span>Selected: {{ multiSelected }}</span>
      </div>

    </section>

  </main>
</template>

<style>
main {
  max-width: 600px;
}

section {
  padding: 1rem 0;
}

button, a {
  display: block;
  margin-bottom: 1em;
}

span {
  display: block;
}

.red {
  color: red;
}

.buttons, .row {
  display: flex;
  flex-wrap: wrap;
}

.box {
  padding-right: 2rem;
  padding-bottom: 3rem;
}
</style>