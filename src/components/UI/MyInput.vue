<template>
  <input :value="modelValue" @input="updateInput" class="input" type="text" />
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
.input {
  width: 100%;
  border: 0.5mm solid #e3e3e3;
  border-radius: 8px;
  padding: 10px 15px;
  margin-top: 15px;
  color: #e3e3e3;
}
</style>
