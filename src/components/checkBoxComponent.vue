<template>
  <!-- <div style="display: flex; align-items: center" class="container">
    <input
      type="checkbox"
      :checked="value"
      @change="$emit('input', $event.target.checked)"
      style="margin-right: 10px; font-weight: 500"
    />
    <slot></slot>
  </div> -->

  <label class="container">
    <slot></slot>
    <input
      type="checkbox"
      :checked="value"
      @change="$emit('input', $event.target.checked)"
    />
    <span class="checkmark"></span>
  </label>
</template>

<script>
export default {
  data: () => ({}),
  props: ["value"],
};
</script>
<style>
/* The container */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  padding-top: 1px;

  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0px;
  height: 17px;
  width: 17px;
  background-color: #fff;
  border: 2px solid #b1b1b4;
  border-radius: 3px;
}

/* On mouse-over, add a grey background color */
/* .container:hover input ~ .checkmark {
  background-color: #ccc;
} */

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #fff;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 6px;
  top: 2px;
  width: 4px;
  height: 8px;
  border: solid #b1b1b4;
  border-width: 0 2px 2px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>