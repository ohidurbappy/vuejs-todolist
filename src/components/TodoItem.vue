<template>
    <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
        <p>
            <input v-bind:checked="todo.completed" type="checkbox" v-on:change="markComplete">

            {{todo.title}}
            
            <button class="del" @click="deleteItem">X</button>
            </p>
    </div>
</template>


<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        markComplete: function(){
            this.todo.completed=!this.todo.completed;
        },

        deleteItem(){
            this.$emit('del-todo',this.todo.id);
        }
    }
}
</script>

<style scoped>
.todo-item{
    background : #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}

.is-completed{
    text-decoration:line-through ;
}

.del{
    border:none;
    margin-left: 8px;
    background:#ee0553;
    border-radius: 50%;
    padding: 8px;
    font-weight: bold;
    box-sizing: border-box;
    color: white;
    box-shadow: none;
}
</style>