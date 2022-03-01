<template>
  <div>
    <div class="input_flex">
      <i class="material-icons input_icon">{{ icon }}</i>
      <!-- @input="$emit('input', $event.target.value)" -->

      <input
        @input="validationcheck == 'yes' ? v.$touch() : ''"
        v-model="email"
        :placeholder="placeholder"
        :type="InputType"
        :class="has_icon"
        style="border: unset"
      />
    </div>
    <div
      v-if="validationcheck == 'yes' && v.$error"
      style="
        display: flex;
        padding: 0px 12px;
        color: #ff5252;
        font-size: 12px;
        margin-top: 3px;
      "
    >
      <span>Enter Valid Email ID</span>
      <!-- <pre>{{v}}</pre> -->
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({}),
  props: {
    validationcheck: {
      type: String,
      required: false,
      default: "no",
    },
    value: { type: String, required: false, default: "" },
    placeholder: { type: String, required: false, default: "" },
    InputType: { type: String, required: true, default: "text" },
    icon: { type: String, required: false, default: "" },
    v: {
      type: Object,
      required: false,
    },
  },
  computed: {
    has_icon() {
      if (this.icon) {
        return "input__has_icon";
      }
      return "";
    },
    email: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("input", value);
      },
    },
  },
};
</script>
<style scoped>
.input_flex {
  display: flex;
  align-items: center;
  /* justify-content: center; */
  border: 2px solid #b1b1b4;
  border-radius: 4px;
  margin-top: 20px;
  padding: 10px;
}
.input__has_icon {
  padding-left: 16px !important;
}
.input_icon {
  color: orange;
}
*:focus {
  outline: none;
}
</style>