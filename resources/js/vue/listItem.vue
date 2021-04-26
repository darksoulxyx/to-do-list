<template>
    <div class="itemList">
    <div  class="item">
    <div class="form">
     <input type="checkbox"
        @change="updateCheck()"
        v-model="item.completed"
    />
        <strong :class="[item.completed ? 'completed' : '','itemText']">{{ item.name }}</strong>
    </div>
    <div style="display:flex;align-items:center;">
     <span class="done">{{item.completed_at!=null ? new Date(item.completed_at.toString()).toISOString().split('T')[0] :""}}</span>
    <button>
         <font-awesome-icon
            icon="trash"
            class="trashcan"
            @click="removeItem()"
        />
        </button>
    </div>
    </div>
    </div>
</template>
<script>
export default {
    props:['item'],
    methods: {
        updateCheck(){
            axios.put('api/item/'+this.item.id,{
                item:this.item
            }).then((response) => {
                if(response.status==200){
                    this.$emit('itemchanged')
                }
            }).catch((error) => {
                    console.log(error)
                })
        },
        removeItem(){
            axios.delete('api/item/'+this.item.id).then((response) => {
                if(response.status == 200){
                    this.$emit("itemchanged")
                }
            }).catch((error) => {
                console.log(error)
            })
        }
    },
}
</script>
<style scoped>
    .form{
        display: flex;
        align-items: center;
        width: 100%;

    }
    .item{
        display: flex;
        width: 100%;
        align-items: center;
        justify-content: space-between;
    }
    .trashcan{
    color: red;
    border: none;

    outline: none;
    cursor: pointer;

    }
    button{
    padding-left: 2px;
    background: none;
    }
    .itemText{
        margin-left: 2px;
    }
    .completed{
        text-decoration:line-through;

        color: rgb(124, 124, 124);
    }
    span{
    font-size: 16px;
    display: flex;
    width: 90px;
    margin-right: 5px;
    }
</style>
