<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref, computed } from 'vue';
import CheckboxWrapper from './components/CheckboxWrapper.vue';
import CheckboxItem from './components/CheckboxItem.vue';

const checkList = ref([]);
const items = ref([
  { id: 1, label: 'label1' },
  { id: 2, label: 'label2' },
  { id: 3, label: 'label3' },
]);
const checkAll = computed({
  get: () => checkList.value.length === items.value.length,
  set: (values) => {
    values
      ? (checkList.value = items.value.map((item) => item))
      : (checkList.value.length = 0);
  },
});
const input = (value) => console.log(value);
</script>

<template>
  <div>
    <CheckboxItem v-model="checkAll" label="check all" />
    <CheckboxWrapper
      v-for="item in items"
      :key="item.id"
      v-model:item="checkList"
      :label="item.label"
      :nativeValue="item"
      @input="input"
    />
    <CheckboxItem v-model="checkAll" label="check all" />
    {{ checkList }}
  </div>
</template>

<style scoped></style>
