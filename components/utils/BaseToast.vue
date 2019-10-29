<template>
  <p class="baseToast">
    {{ description }}
  </p>
</template>

<script>
export default {
  props: {
    description: {
      type: String,
      default: '',
      required: true
    }
  }
}
</script>

<style lang="scss">
.baseToast {
  position: absolute;
  padding: 8px 12px;
  border-radius: 4px;
  background-color: lighten($base-color-dark, 15);
  color: $base-color-light;
  font-size: 14px;
  text-transform: none;
}
</style>
