<template>
    <div class="addItem">
        <input @keyup.enter="addItem()" type="text" v-model="item.name" />
        <font-awesome-icon

            @click="addItem()"
            icon="plus-square"
            :class="[item.name ? 'active' : 'inactive','icon']"
        />
    </div>
</template>
<script>
export default {
    data(){
        return {
            item:{
                name:""
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name==""){

                return;
            }
            axios.post('api/item/store',{
                item:this.item
            })
            .then(response =>{
                if(response.status == 201){
                    this.item.name=""
                    this.$emit('created')
                }
            })
            .catch(error=>{
                console.log(error)
            })

        }
    }
}
</script>
<style scoped>
    .addItem{
    display: flex;
    justify-content: center;
    align-items: center;
    }
    input{
        background: #f7f7f7;
        border: none;
        outline: none;
        padding: 5px;
        margin-right:10px ;
        width: 100%;
    }
    .icon{
        font-size: 20px;

    }
    .active{
        color: rgb(1, 129, 7);
         cursor: pointer;
    }
    .inactive{
        color: rgb(107, 107, 107);
    }
</style>
