<template>
  <div class="item">
      <input 
      type="checkbox"
      @change="updateCheck"
      v-model="item.completed" />
      <span :class="[item.completed ? 'completed' : '', 'itemText']">
        {{ item.name}}
      </span>
      <button @click="removeItem()" class="trashcan">
          <font-awesome-icon icon="trash" class="trash" />
      </button>
  </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put(`api/item/${this.item.id}`, {
                item: this.item
            })
            .then( response => {
                if(response.status == 201){
                    this.$emit('itemChanged');
                }
            })
            .catch(error => {
                console.log(error);
            })
        },
        removeItem(){
            axios.delete(`api/item/${this.item.id}`, {
                item: this.item
            })
            .then(response => {
                if(response.status == 200){
                    this.$emit('itemChanged');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color: #999999;
}
.itemText{
    width: 100%;
    margin-left: 20px;
    font-family: 'Nunito';
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
}
.trashcan{
    border: none;
    color: #FF0000;
    background: none;
}
.trash{
    font-size: 22px;
}
</style>