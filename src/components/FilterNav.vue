<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')">
        View All
    </button>
    <button @click="updateFilter('done')">
        Done
    </button>
    <button @click="updateFilter('toDo')">
        To do
    </button>
  </nav>
</template>

<script>
export default {
    methods: {
        updateFilter(by) {
            this.$emit('filterChange', by)
        }
    }
}
</script>

<style>
.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }

</style>