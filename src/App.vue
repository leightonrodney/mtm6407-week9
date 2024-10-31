<script setup>

import { ref, watch, onMounted, onUpdated } from 'vue';
import Message from './components/Message.vue';

onMounted(() => {
  console.log('The App is now mounted');
});

onUpdated(() => {
  console.log('Data has just been updated');
});

const count = ref(0);
const text = ref('');
const username = ref('');
const password = ref('');
const isLoggedIn = ref(false)

const name = 'MTM6407';

const showGreeting = () => {
  console.log(`Welcome to: ${name}!!`)
}

const cart = [
  {
    id: 1,
    name: 'Bookbag'
  },
  {
    id: 2,
    name: 'Pencil'
  },
  {
    id: 3,
    name: 'Coffe Mug'
  }
]

const options = [
  {
    name: 'Select a size',
    value: ''
  },
  {
    name: 'S',
    value: 'small'
  },
  {
    name: 'M',
    value: 'medium'
  },
  {
    name: 'L',
    value: 'large'
  },
  {
    name: 'XL',
    value: 'xtra-large'
  }
]

const handleCheckout = () => {
  console.log(`You sucessfully checked out: ${cart.length} items!`);
}

const handleSelect = (e) => {
  /*
  const selectedOption = e.target.value;
  if (selectedOption !== '') {
    console.log(`You have selected: ${selectedOption}`)
  }
  */
}

const handleErase = () => {
  text.value = ''
}

const handleWordDoc = (e) => {

  // Save Function
  if ( e.ctrlKey === true && e.key === 's') {
    console.log(e.target.value);
  }
}


const handleSubmit = (e) => {
  // prevented the default behaviour of refreshing the page on form submit
  e.preventDefault();
  console.log(`username: ${username.value} + password: ${password.value}`);
  if (username.value !== '' && password !== '') {
    isLoggedIn.value = true;
  } else {
    alert('Please enter a username and password!');
  }

}



// Watcher
watch(count, (newValue, oldValue) => {
  console.log(`Count button was clicked, value was changed from ${oldValue} to ${newValue}.`);
})


// Lifecycle of a Vue App
/*

onBeforeMount - the App/Component is about to be mounted

onMounted - App/Component has been mounted to the DOM

onBeforeUpdate - Data is about to be updated

onUpdated - Data has been updated

onBeforeUnmount - the App/Component is about to be un-mounted

onUnmounted - App/Component has been un-mounted from the DOM

*/

</script>

<template>

  <!-- onclick with JavaScript expression -->
  <button @click="count++">This is the count: {{ count }}</button>

  <!-- Running a function -->
  <button v-on:click="showGreeting">Show greeting message</button>
  <br/>

  <!-- Running a function -->
  <button @click="handleCheckout">Checkout</button>

  <br/>

  <form>
    <select @change="handleSelect">
      <option v-for="option in options" :value="option.value">{{ option.name }}</option>
    </select>
  </form>


  <div class="word-app">

    <textarea cols="30" rows="15" @keydown="handleWordDoc" v-model="text"></textarea>
    <button @click="handleErase">Erase</button>

  </div>

  <form v-if="!isLoggedIn" @submit="handleSubmit">
    <input placeholder="Username" v-model="username"/>
    <input type="password" placeholder="Password" v-model="password" />
    <button>Log in</button>
  </form>

  <Message />

</template>

<style scoped>

.word-app > input {
  width: 700px;
  min-height: 300px;
  margin: 15px;
  padding:0;
}

</style>
