<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form></add-item-form>
        </div>
        <list-view></list-view>
    </div>
</template>

<script>
import AddItemForm from "./AddItemForm.vue"
import ListView from "./ListView.vue"
export default {
  name: "App",
  components: {
      AddItemForm,
      ListView,
    },
    data: function() {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then( response => {
                this.items = response.data
            }).catch((err) => {
                console.log(err)
            });
        }
    },
    created
}
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;
}
#title {
    text-align: center;
}
</style>
