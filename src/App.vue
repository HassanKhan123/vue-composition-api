<template>
  <section class="container">
    <h2>{{ fullName }}</h2>
    <h3>{{ userAge }}</h3>
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Name" @input="setFirstName" />
      <input type="text" placeholder="Last Name" @input="setLastName" />
    </div>
  </section>
</template>

<script>
import { reactive, toRefs, ref, computed } from 'vue';

export default {
  setup() {
    const firstName = ref('');
    const lastName = ref('');

    const user = reactive({
      name: 'Hassan',
      age: 21,
    });

    const userRefs = toRefs(user);

    function setNewAge() {
      user.age = 32;
    }

    function setFirstName(e) {
      firstName.value = e.target.value;
    }

    function setLastName(e) {
      lastName.value = e.target.value;
    }

    const uName = computed(() => {
      return firstName.value + ' ' + lastName.value;
    });

    return {
      user,
      userName: userRefs.name,
      userAge: userRefs.age,
      setAge: setNewAge,
      setFirstName,
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