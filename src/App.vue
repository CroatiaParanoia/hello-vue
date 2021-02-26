<template>
  <div id="app">
    <SelectorContainer v-model="form1">
      <Selector value-key="demo1" :multiply="false" />
      <Selector value-key="demo2" />
      <JsonView keyName="form1" :jsonValue="form1" />
      <button @click="form1 = {}">RESET form</button>
    </SelectorContainer>

    <UnderLine />

    <SelectorContainer v-model="form2">
      <Selector value-key="demo1" :multiply="false" />
      <Selector value-key="demo2" />
      <JsonView keyName="form2" :jsonValue="form2" />
      <button @click="form2 = {}">RESET form</button>
    </SelectorContainer>

    <UnderLine />

    <Selector v-model="selectedValues" />
    <JsonView keyName="selectedValues" :jsonValue="selectedValues" />
    <button @click="selectedValues = []">RESET selectedValues</button>
  </div>
</template>

<script>
import SelectorContainer from "./components/Selector/SelectorContainer";
import Selector from "./components/Selector/Selector";

const UnderLine = {
  render(createElement) {
    return createElement("div", {
      style: "width: 100%; height: 1px; background-color: #ccc; margin: 24px 0",
    });
  },
};
const JsonView = {
  render(createElement) {
    return createElement("div", {}, [
      this.keyName,
      createElement("pre", {}, JSON.stringify(this.jsonValue, null, 2)),
    ]);
  },
  props: {
    keyName: String,
    jsonValue: Object,
  },
};
export default {
  name: "App",
  components: {
    SelectorContainer,
    Selector,
    UnderLine,
    JsonView,
  },
  data() {
    return {
      selectedValues: [],
      form1: {},
      form2: {},
    };
  },
  methods: {},
};
</script>

<style>
</style>
