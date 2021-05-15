<template>
  <form @submit.prevent="submitHandler">
    <div
      v-for="(item, idx) in data"
      :key="idx"
    >
      <div v-if="item.type === 'image'">
        {{ item.name }}
        <input
          @input="formData[`${item.name}`] = $event.target.value"
          type="file"
          :placeholder="item.name"
        >
      </div>

      <div v-if="item.type === 'string'">
        {{ item.name }}
        <input v-model="formData[`${item.name}`]" type="text" :placeholder="item.name">
      </div>

      <div v-if="item.type === 'text'">
        {{ item.name }}
        <textarea v-model="formData[`${item.name}`]" :placeholder="item.name"></textarea>
      </div>

      <div v-if="item.type === 'date'">
        {{ item.name }}
        <input v-model="formData[`${item.name}`]" type="date" :placeholder="item.name">
      </div>

      <div v-if="item.type === 'file'">
        {{ item.name }}
        <input
          @input="formData[`${item.name}`] = $event.target.value"
          type="file"
          :placeholder="item.name"
        >
      </div>

      <div v-if="item.type === 'enum'">
        {{ item.name }}
        <select v-model="formData[`${item.name}`]">
          <option
            v-for="(option, idx) in item.options"
            :value="option"
            :key="option + idx"
          >{{option}}</option>
        </select>
      </div>
    </div>

    <button>send</button>
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
      formData: {},
    };
  },
  beforeMount() {
    const keyArr = this.data.map((i) => i.name);
    keyArr.forEach((i) => {
      this.formData[i] = '';
    });
  },
  methods: {
    submitHandler() {
      console.log(this.formData);
    },
  },
};
</script>
