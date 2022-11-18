<template>
  <!-- <header>this is {{ title }}</header>
    {{ text }} -->
  <input v-model="text" @click="this.$emit('texts', text)" />
  <div>{{ text }}</div>
</template>

<script>
export default {
  props: {
    title: String,
  },
  data() {
    return {
      text: "",
    };
  },
  methods: {
    Clicked() {
      console.log(this.text);
    },
  },
};
</script>

<style></style>
