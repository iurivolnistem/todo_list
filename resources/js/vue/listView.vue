<template>
  <div>
      <div v-for="(item, index) in items" :key="index">
          <list-item :item="item" class="item" v-on:itemChanged="$emit('reloadlist')" />
      </div>
  </div>
</template>

<script>
import listItem from './listItem'

export default {
    props: ['items'],
    components: {
        listItem
    }
}
</script>

<style scoped>
.item{
    padding: 10px;
    margin-top: 5px;
    border: 2px solid #000;
}

</style>