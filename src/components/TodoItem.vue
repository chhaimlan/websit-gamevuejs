<template>
  <div class="container">
    <div class="todo-item" v-bind:class="{'is-complete': todo.completed}">
      <p>
        <input
          type="checkbox"
          v-on:change="markChange"
          v-bind:checked="todo.completed"
        />
        {{ todo.title }}        
        <button @click="update" class="update">Update</button>
        <button @click="$emit('delete-todo',todo.id)" class="del">x</button>                
      </p>
    </div>
    <div v-if="this.flag">
        <form @submit="updateTodo">
            <div class="form-group">
             <input type="text" v-model="updateTitle" required class="form-control" placeholder="Title">
            </div>
            <div class="form-group">
                <button class="btn btn-success btn-block">update</button>
            </div>
        </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props:['todo','todos'],
  methods:{
      markChange(){
          this.todo.completed = !this.todo.completed
      },
      update(){
        this.flag = !this.flag
      },
      updateTodo(e){
          e.preventDefault();
          this.todos.filter((todo) => {
              if(todo.id == this.todo.id){
                  //update the title
                  todo.title = this.updateTitle
              }
          })
          //reset the flag
          this.flag = false
      }
  },
  data(){
      return{
          flag: false,
          updateTitle: ""
      }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 20px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
  
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
.update{
    background: blue;
    color: #fff;
    border: none;
    padding: 5px;
    border-radius: 30px;
    cursor: pointer;
    float:right;
}
</style>
