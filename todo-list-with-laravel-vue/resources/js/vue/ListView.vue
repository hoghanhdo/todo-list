<template>
  <div>
      <div v-for="(item, index) in items" :key="index"></div>
      <list-item :item="item" class="item">
      </list-item>
  </div>
</template>

<script>
import listItem from "./ListItems.vue"
export default {
    props: ['items'],
    components: {
        listItem
    }

}
</script>

<style scoped>

.item {
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}

</style>
