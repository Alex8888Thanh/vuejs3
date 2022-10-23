<template>
  <div class="container">
    <div id="app">
      <h1>Input Json</h1>
      <input v-model="inputDataJson" @keyup.enter="process" type="text" /><br />
      <button @click="process()">process</button>
    </div>
    <h1>Output Json</h1>
    <ul>
      <li
        v-for="item of jsons"
        :key="item.id"
      >
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      jsons: [],
      inputDataJson: "",
    };
  },
  methods: {
    async process() {
      const res = await axios.post(`http://localhost:3000/jsons`, {
        name: this.inputDataJson,
      });
      this.jsons = [...this.jsons, res.data];
      this.inputDataJson = "";
    },
  },
};
</script>
