<template>
  <span class="todo-count">
    <strong>{{ nb }} item{{ nb > 1 ? 's' : ''}}</strong> left
  </span>
</template>

<script>
export default {
  props: {
    nb: {
      type: Number,
      required: true
    }
  }  
}
</script>