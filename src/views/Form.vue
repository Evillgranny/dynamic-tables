<template>
  <div>
    <h1>Form single</h1>
    <SingleForm
      v-if="data.type === 'single'"
      :data="data.fields"
    />

    <h1>Form Multiple</h1>
    <MultipleForm
      v-if="data2.type === 'multiple'"
      :data="data2.fields"
    />
  </div>
</template>

<script>
import SingleForm from '../components/forms/SingleForm.vue';
import MultipleForm from '../components/forms/MultipleForm.vue';

const data = require('@/data.json');
const data2 = require('@/data2.json');

export default {
  components: { MultipleForm, SingleForm },
  data() {
    return {
      data,
      data2,
    };
  },
};
</script>

<style scoped lang="sass">
</style>
