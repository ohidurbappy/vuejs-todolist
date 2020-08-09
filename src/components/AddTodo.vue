<template>
    <div>
        <form @submit="addTodo">
            <input name="title" v-model="title" type="text" placeholder="Add New todo">
            <button class="btn" type="submit">Add</button>
        </form>
    </div>
</template>


<script>

// import {v4 as uuidv4} from 'uuid';

export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },

    methods: {
        addTodo(e){
            e.preventDefault();
            
            const newTodo={
                // id: uuidv4('12'),
                title:this.title,
                completed: false
            }

            this.$emit('add-todo',newTodo);

            this.title='';

        }
    }

}
</script>

<style scoped>
form{
    background: #f1f1f1;
    padding: 20px;
    display: flex;
}
input{
    width: 80%;
    padding:8px;
    margin-right: 4px;
}

.btn{
    width: 20%;
}

</style>