<template>
        <input type="text" class="todo-input" v-model="newTodoItem" placeholder="Add your new todo" required @keyup.enter="addTodoItem">
        <button @click="addTodoItem">Add</button>

    <div class="todo-item" v-for="(todo,index) in todoList" :key="todo.id">
        
        
        <div>
            <div v-if="!todo.isEditing" :class="todo.todoCompleted && 'mark--completed'">
                <input type="checkbox" class="todo--checkbox" @click="toggleTodoItemComplete(todo)">
                {{ todo.desc }}</div>
            <input v-else type="text" class="todo-edit--item" v-model="todo.desc"
            @keyup.enter="updateTodoItem(todo)">
        </div>
        <div class="edit--delete">
            <div class="remove-todoItem" @click="toggleTodoEditable(todo)">&#9997;</div>
            <div class="remove-todoItem" @click="removeTodoItem(index)">&#10060;</div>
        </div>
        

    </div>
</template>

<script>
 export default{
    name:'todo-list',
    data(){
        return {

            newTodoItem:'',
            todoList:[
                {
                    id:0,
                    desc:'Lets learn Vue',
                    isEditing:false,
                    todoCompleted:false
                },
                {
                    id:1,
                    desc:'Complete the assignment',
                    isEditing:false,
                    todoCompleted:false
                }
            ]
        }
    },
    methods:{
        addTodoItem(){
            if(this.newTodoItem.trim().length == 0)
             return
            this.todoList.push({
                'id':this.todoList.length,
                'desc':this.newTodoItem,
                'isEditing':false,
                'todoCompleted':false
            })
            this.newTodoItem=""
        },
        toggleTodoEditable(todoItem){
           todoItem.isEditing=!todoItem.isEditing
           todoItem.todoCompleted=false
           
        },
        updateTodoItem(todoItem){
            todoItem.isEditing=false
            
        },
        removeTodoItem(index){
            this.todoList.splice(index,1)
        },
        toggleTodoItemComplete(todoItem){
            todoItem.todoCompleted=!todoItem.todoCompleted
        }
    }
 }
</script>

<style >

.todo-item{
    display: flex;
    justify-content: space-between;
}
.remove-todoItem{
    cursor: pointer;
    
}


.todo--checkbox{
    cursor: pointer;
    background-color: rgb(202,60,60);
}

.todo-edit--item{

}


.mark--completed{
    text-decoration: line-through;
}
.edit--delete{
    display: flex;
    align-items: center;
    justify-content: center;
}

</style>