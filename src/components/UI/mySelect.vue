<template>
  <select class="myselect" :value="modelValue" @change="changeOption">
    <option disabled value="">Sort</option>
    <option v-for="option in options" :key="option.value" :value="option.value">
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "my-select",
  props: {
    modelValue: {
      type: String,
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
.myselect {
  background-color: #1a1a1a;
  color: #e3e3e3;
  border-radius: 8px;
  border: 0.5px solid #e3e3e3;
}
</style>
