<template>
  <div>
    <input
      @blur="v.$touch()"
      :maxLength="maxLength"
      @input="emitInputValue"
      type="text"
      placeholder="e.g. Amazing Course in Flutter!"
      class="input is-large"
    />
    <span class="icon is-small is-right"> {{ 50 - inputLength }} </span>
  </div>
</template>

<script>
export default {
  props: ["maxLength", "v"],
  data() {
    return {
      currentValue: "",
    };
  },
  computed: {
    inputLength() {
      return this.currentValue.length || 0;
    },
  },

  methods: {
    emitInputValue($event) {
      this.currentValue = $event.target.value;
      this.$emit("input", this.currentValue);
    },
  },
};
</script>

<style></style>
