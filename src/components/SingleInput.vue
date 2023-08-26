<script setup>
// defineProps(["modelValue"]);
// defineEmits(["update:modelValue"]);
defineProps(["modelValue", "type", "placeholder"]);
defineEmits(["update:modelValue"]);
</script>
<template>
  <input
    :type="type"
    class="fieldStyle"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
