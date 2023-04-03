<template>
  <div>
    <p id="item">{{ todoProps }}</p>
  </div>
</template>

<script>
export default {
  name: 'TodoItem-component',
  props: ['todoProps']
}
</script>

<style>
#item {
  background-color: pink;
}
</style>
