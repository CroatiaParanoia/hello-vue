<template>
  <div class="selector">
    <div class="selector-title">{{ title }}</div>
    <div class="selector-list">
      <div
        class="selector-item"
        v-for="{ value: itemValue, label, disabled } in innerOptions"
        :key="itemValue"
        :class="{
          active: !disabled && realSelectedValues.includes(itemValue),
          disabled,
        }"
        @click="onBoxItemClick(itemValue)"
      >
        {{ label }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    valueKey: {
      type: String,
    },
    multiply: {
      type: Boolean,
      default: true,
    },
    title: {
      type: String,
      default: "默认标题",
    },
    options: {
      type: Array,
      default: () => [
        { label: "分类1", value: "001" },
        { label: "分类2", value: "002" },
        { label: "分类3", value: "003" },
        { label: "分类4", value: "004" },
        { label: "分类5", value: "005" },
        { label: "分类6", value: "006" },
      ],
    },
    value: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    const innerOptions =
      typeof this.options[0] === "string"
        ? this.options.map((v) => ({ label: v, value: v }))
        : this.options;
    return {
      innerOptions,
      selectedValues: [],
    };
  },
  methods: {
    onBoxItemClick(value) {
      const isSelected = this.realSelectedValues.includes(value);
      if (isSelected) {
        this.clearBoxItemActive(value);
      } else {
        this.setBoxItemActive(value);
      }
    },

    setBoxItemActive(value) {
      this.selectedValues = this.multiply
        ? [...this.realSelectedValues, value]
        : [value];
    },

    clearBoxItemActive(value) {
      this.selectedValues = this.realSelectedValues.filter((v) => v !== value);
    },
  },
  watch: {
    selectedValues(value) {
      this.$emit("input", value);
      if (this.valueKey) {
        this.$container.setFieldsValue(this.valueKey, value);
      }
    },
    value(value) {
      this.selectedValues = value;
    },
    realSelectedValues(value) {
      if (this.isInContainer) {
        this.selectedValues = value;
      }
    },
  },
  computed: {
    realSelectedValues() {
      if (this.isInContainer) {
        return this.$container.$data.form[this.valueKey] || [];
      }
      return this.selectedValues;
    },
    $container: function () {
      let parent = this.$parent;

      while (
        parent &&
        parent !== this.$root &&
        parent.$options._componentTag !== "SelectorContainer"
      ) {
        parent = parent.$parent || this.$root;
      }

      return parent;
    },
    isInContainer() {
      return this.$container !== this.$root;
    },
  },
};
</script>
<style  scoped>
.selector-title {
  margin-bottom: 10px;
}
.selector-list {
  display: flex;
  flex-wrap: wrap;
}

.selector-item {
  width: 200px;
  height: 40px;

  margin-right: 10px;
  margin-bottom: 10px;
  background-color: #ccc;
  color: #000;

  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.selector-item.active {
  background-color: red;
  color: #fff;
}
</style>