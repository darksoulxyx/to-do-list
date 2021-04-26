<template>
<div class="toDoListContainer">
    <div class="header">
    <h1>Task List</h1>
    </div>
    <addItemForm v-on:created="getItems()" />
    <list-view :items="items"
    v-on:reloadlist="getItems()"

    />
</div>

</template>

<script>
import addItemForm from "./addItemForm"
import listView from "./listView"
export default {
    components:{
        addItemForm,
        listView
    },
    data() {
        return {
            items:[]
        }
    },methods: {
        getItems(){
            axios.get("api/items").then((response) => {
               this.items = response.data
            }).catch((error) => {
                console.log(error)
            })
        }
    },
    created(){
        this.getItems()
    }
}
</script>
<style scoped>
    .toDoListContainer{
        width: 350px;
        margin:auto;
        background-color:#d3d3d3;
        padding: 20px;

    }
    .header{
    text-align: center;}
</style>
