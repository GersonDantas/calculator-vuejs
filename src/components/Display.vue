<template>
  <div class="display">
    {{ value }}
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: null
    }
  },
}
</script>

<style>
.display {
  grid-column: span 4;
  background-color: #0000004a;

  display: flex;
  justify-content: right;
  align-items: center;
  padding: 20px;
  font-size: 2.1em;
  overflow: hidden;
}
</style>
