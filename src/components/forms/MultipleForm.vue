<template>
  <form @submit.prevent="submitHandler">
    <div
      v-for="(form, idx) in formData"
      :key="idx + 'form'"
      style="margin-bottom: 30px;"
    >
      <button type="button" v-if="formData.length > 1" @click="del(idx)">delete</button>
      <div v-for="(item, itemIdx) in data" :key="itemIdx + 'item'">
        <div v-if="item.type === 'image'">
          {{ item.name }}
          <input
            @input="formData[idx][`${item.name}`] = $event.target.value"
            type="file"
            :placeholder="item.name"
          >
        </div>

        <div v-if="item.type === 'string'">
          {{ item.name }}
          <input v-model="formData[idx][`${item.name}`]" type="text" :placeholder="item.name">
        </div>

        <div v-if="item.type === 'text'">
          {{ item.name }}
          <textarea v-model="formData[idx][`${item.name}`]" :placeholder="item.name"></textarea>
        </div>

        <div v-if="item.type === 'date'">
          {{ item.name }}
          <input v-model="formData[idx][`${item.name}`]" type="date" :placeholder="item.name">
        </div>

        <div v-if="item.type === 'file'">
          {{ item.name }}
          <input
            @input="formData[idx][`${item.name}`] = $event.target.value"
            type="file"
            :placeholder="item.name"
          >
        </div>

        <div v-if="item.type === 'enum'">
          {{ item.name }}
          <select v-model="formData[idx][`${item.name}`]">
            <option
              v-for="(option, idx) in item.options"
              :value="option"
              :key="option + idx"
            >{{option}}</option>
          </select>
        </div>
      </div>
    </div>
    <button type="submit">send</button>
    <button type="button" @click="addForm">add</button>
  </form>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      formData: [],
      formTemplate: {},
    };
  },
  beforeMount() {
    this.addForm();
  },
  methods: {
    submitHandler() {
      console.log(this.formData);
    },
    addForm() {
      const keyArr = this.data.map((i) => i.name);
      const form = {};
      keyArr.forEach((i) => {
        form[i] = '';
      });
      this.formData.push(form);
    },
    del(idx) {
      this.formData.splice(idx, 1);
    },
  },
};
</script>
