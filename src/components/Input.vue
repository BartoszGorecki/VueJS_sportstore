<template>
  <div class="m-2 text-left mb-3">
    <div class="form-group m-2 input-container" :class="{ invalid: validation.$error }">
      <label for="name">{{ label }}</label>
      <input
        id="name"
        type="text"
        class="form-control"
        :value="value"
        @input="$emit('input', $event.target.value)"
      >
      <p v-if="validation.$invalid && validation.$dirty">Please enter your {{ label }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["validation", "value", "label"]
};
</script>

