<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">To do List</h2>
            <add-item-form v-on:reloadlist="getList()" />
        </div>
        <list-view :items="items" v-on:reloadlist="getList()" />
    </div>
</template>

<script>
import addItemForm from "./addItemForm"
import listView from "./listView"

    export default{
        components: {
            addItemForm,
            listView
        },
        data: function() {
            return{
                items: []
            }
        },
        methods: {
            getList (){
                axios.get('api/items')
                .then(response => {
                    this.items = response.data
                })
                .catch(error => {
                    console.log(error)
                })
            }
        },
        created(){
            this.getList();
        }
    }
</script>

<style scoped>
.todoListContainer{
    width: 100%;
    max-width: 550px;
    margin: auto;
}

.heading{
    padding: 10px;
    border: 2px solid #000;
}

#title{
    text-align: center;
    text-transform: uppercase;
    font-family: 'Nunito';
    font-weight: 700;
}

</style>