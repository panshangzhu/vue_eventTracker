<template>
    <button :style="{ background: color }" class="btn" @click="toggleShowAdd">{{ text }}</button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String,
        toggleShowAdd: Function
    }
}
</script>

<style scoped>
  .btn {
      border: none;
      outline: none;
      padding: 8px;
      color:#f5f6fa;
      cursor: pointer;
  }
</style>