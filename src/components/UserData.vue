<template>
  <h2>{{ userName }}</h2>
</template>

<script>
export default {
  props: ['userName'],
  setup(props, context) {
    console.log(context);
    context.emit('save-data', 1);
    console.log(props.userName);
  },
};
</script>