<template>
  <div>
    <slot> </slot>
  </div>
</template>



<script>
export default {
  componentName: "SelectorContainer",
  props: {
    value: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      form: {},
    };
  },
  methods: {
    setFieldsValue(key, value) {
      this.$set(this.form, key, value);
    },
  },
  watch: {
    form(value) {
      this.$emit("input", value);
    },
    value(value) {
      this.form = value;
    },
  },
};
</script>