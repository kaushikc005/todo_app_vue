<template>
        <input type="text" class="todo-input" v-model="newTodoItem" placeholder="Add your new todo" required @keyup.enter="addTodoItem">
        <button @click="addTodoItem" class="add--btn">Add</button>

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
    padding: 0.85rem;
    color: #000;
    font-weight: 900;  
    font-size: 1.5rem;  
}

.todo-input{
    padding: 0.75rem;
    outline: none;
    border-radius: 0.25rem; 
    margin:0 0.25rem;
    width: 70%;
}
.add--btn{
    background-color: rgba(255,255,255,0.3);
    padding: 0.5rem;
    border-radius: 0.25rem;
    border: 1px solid rgba(255,255,255,0.5);
    width: 20%;
    cursor: pointer;
    font-size: 1rem;
}

.add--btn:hover{
    background-color: transparent;
}
.remove-todoItem{
    cursor: pointer;
    
}


.todo--checkbox{
    cursor: pointer;
    background-color: rgb(202,60,60);
}

.todo-edit--item{
   padding: 0.5rem;
   border-radius: 0.25rem;
   outline: 0;
   
   background: transparent;
}


.mark--completed{
    text-decoration: line-through;
}
.edit--delete{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.5rem;
}

</style>