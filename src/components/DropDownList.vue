<template>
    <div class="dropdown-list">
      <label>{{ label }}</label>
      <select :required="required" @change="updateValue($event.target.value)">
        <option v-for="(item, index) in itens" :key="index">{{ item }}</option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      label: String,
      required: Boolean,
      itens: Array,
      updateValue: Function,
    },
  };
  </script>
  
  <style scoped>
  </style>