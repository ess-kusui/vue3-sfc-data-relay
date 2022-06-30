<template>
  <div>
    <label>
      <input v-model="localValue" :value="nativeValue" type="checkbox" />
      <span v-if="label"> {{ label }} </span>
    </label>
  </div>
</template>

<script setup>
import { computed, toRefs } from 'vue';

const props = defineProps({
  modelValue: { default: null },
  nativeValue: { default: null },
  label: { default: '' },
});
const { modelValue } = toRefs(props);

const localValue = computed({
  get: () => modelValue.value,
  set: (value) => {
    if (!value) {
      emit('update:modelValue', null);
      return;
    }
    input(value);
    change(value);
    emit('update:modelValue', value);
  },
});

const classes = computed(() => (props.col ? [`col-${props.col}`] : []));

const emit = defineEmits(['input', 'check', 'update:modelValue']);
const input = (value) => emit('input', value);
const change = (value) => emit('check', value);
</script>

<style scoped></style>
