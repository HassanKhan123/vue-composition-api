<template>
  <section class="container">
    <UserData :user-name="fullName" />
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Name" v-model="firstName" />
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <button @click="setLastName">Set Last Name</button>
    </div>
  </section>
</template>

<script>
import {
  reactive,
  toRefs,
  ref,
  computed,
  watch,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from 'vue';

import UserData from './components/UserData';

export default {
  components: {
    UserData,
  },
  setup() {
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);

    const user = reactive({
      name: 'Hassan',
      age: 21,
    });

    const userRefs = toRefs(user);

    function setNewAge() {
      user.age = 32;
    }
    function setLastName() {
      lastName.value = lastNameInput.value.value;
    }
    watch([firstName, lastName], (newValues, oldValues) => {
      console.log('old first name', oldValues[0]);
      console.log('new first name', newValues[0]);
      console.log('old last name', oldValues[1]);
      console.log('new last name', newValues[1]);
    });

    const uName = computed(() => {
      return firstName.value + ' ' + lastName.value;
    });

    onBeforeMount(() => {});
    onMounted(() => {});

    onBeforeUpdate(() => {});

    onUpdated(() => {});

    onBeforeUnmount(() => {});
    onUnmounted(() => {});
    return {
      user,
      userName: userRefs.name,
      userAge: userRefs.age,
      setAge: setNewAge,
      firstName,
      lastNameInput,
      setLastName,
      fullName: uName,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>