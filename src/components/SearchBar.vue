<template>
  <div>
    <input @input="onInput" class="form-control" placeholder="Search for..." />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    onInput: function(event) {
      this.$emit("termChange", event.target.value);
    }
  }
};
</script>

<style scoped>
input {
  width: 60%;
  margin: auto;
}
div {
  text-align: center;
  margin: 20px;
}
</style>