<template>
  <button class="square" @click="$emit('on-click')">{{ value }}</button>
</template>

<script setup>
defineProps({
  value: {
    type: Number,
    required: true
  },
})
</script>
