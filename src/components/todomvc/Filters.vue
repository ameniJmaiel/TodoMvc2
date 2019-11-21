<template>
  <ul class="filters">
    <li v-for="filter in filters" :key="filter">
      <a :href="'#/' + filter" @click.prevent="$emit('update:current', filter)" :class="{selected: current === filter}" style="text-transform: capitalize;">
        {{ filter }}
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    current: {
      type: String,
      required: true
    },
    filters: {
      type: Array,
      required: true
    }
  }
}
</script>