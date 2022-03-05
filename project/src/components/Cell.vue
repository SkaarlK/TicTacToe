<template>
  <div id="cell" @click="$emit('clicked')">{{check ? check : ''}}</div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    check: {
      type: String,
      required: true,
    },
  },
  data: () => ({
  }),
};
</script>

<style scoped>
  #cell {
    width: 116px;
    height: 116px;
    border: 2px solid rgb(75,75,75);
    font-size: 42px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
