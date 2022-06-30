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
  item: null,
  label: null,
  nativeValue: null,
  input: () => {},
});
const { item, label, nativeValue, input } = toRefs(props);
const emit = defineEmits(['update:item']);
const localValue = computed({
  get: () => item.value,
  set: (value) => {
    emit('update:item', value);
  },
});
</script>

<style scoped></style>
