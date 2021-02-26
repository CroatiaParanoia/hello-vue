<template>
  <div id="app">
    <SelectorContainer v-model="form">
      <Selector value-key="demo1" :multiply="false" />
      <Selector value-key="demo2" />
      form: {{ form }}
      <div @click="form = {}">RESET form</div>
    </SelectorContainer>

    <Selector v-model="selectedValues" />
    selectedValues: {{ selectedValues }}
    <div @click="selectedValues = []">RESET selectedValues</div>
  </div>
</template>

<script>
import SelectorContainer from "./components/Selector/SelectorContainer";
import Selector from "./components/Selector/Selector";
export default {
  name: "App",
  components: {
    SelectorContainer,
    Selector,
  },
  data() {
    return {
      selectedValues: [],
      form: {},
    };
  },
  methods: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
