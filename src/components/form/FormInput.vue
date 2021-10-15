<template>
  <div class="form-group">
    <label class="d-block">
      <div class="mb-2">{{ param.header }}</div>
      <textarea
        class="form-control"
        v-if="param.inputType === 'textarea'"
      ></textarea>
      <input
        v-else
        :type="param.inputType"
        class="form-control"
        :class="{ 'is-invalid': param.isInvalid }"
        v-model="value"
        @input="bindValue(param.typeValue)"
      />
      <div class="invalid-feedback" v-if="param.isInvalid">
        {{ changeError }}
      </div>
    </label>
  </div>
</template>

<script>
export default {
  props: ["param", "errors"],
  data() {
    return {
      value: ""
    };
  },
  computed: {
    changeError() {
      const type = this.param.typeValue;

      return this.errors[type];
    }
  },
  methods: {
    bindValue(typeValue) {
      this.$emit("bindValue", typeValue, this.value);
      this.param.isInvalid = false;
    }
  }
};
</script>