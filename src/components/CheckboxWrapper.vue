<template>
  <div>
    <p>Item</p>
    <CheckboxItem
      v-model="localValue"
      :label="label"
      :nativeValue="nativeValue"
      @input="input"
    />
  </div>
</template>

<script setup>
import CheckboxItem from './CheckboxItem.vue';
import { computed, toRefs } from 'vue';

const props = defineProps({
  modelValue: null,
  label: null,
  nativeValue: null,
  input: () => {},
});
const { modelValue, label, nativeValue, input } = toRefs(props);
const emit = defineEmits(['update:modelValue']);
const localValue = computed({
  get: () => modelValue.value,
  set: (value) => {
    emit('update:modelValue', value);
  },
});
</script>

<style scoped></style>
