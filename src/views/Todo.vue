<template>
  <div class="row">
    <div class="col-md-8 offset-md-2 text-center">
      <h3 class="mt-5"> Todo List </h3>
      <hr>

      <div class="row">
        <div class="col-md-12 d-flex justify-content-center">
          <input type="text" class="mx-3" v-model="inputText" >
          <button v-on:click="isActionEdit ? updateTodo() : addTodo()" class="btn btn-primary"
                  v-text=" isActionEdit ? 'Güncelle': 'Ekle'"></button>
        </div>
      </div>
      <hr>

      <div class="todo-container">
        <TodoItem v-on:deleteTodo="deleteTodo($event)" v-on:changeUpdateButton="changeUpdateButton($event)"
                  v-for="todo in todoList" v-bind:key="todo.id" v-bind:todo="todo"/>
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "@/views/TodoItem";
export default {
  name: "Todo",
  components: {
    TodoItem
  },
  data: function () {
    return {
      inputText : '',
      updatedItemId : null,
      isActionEdit : false,
      todoList: [
        {
          id: 1,
          text: "bunu bitir"
        },
        {
          id: 2,
          text: "bunu da tamamla"
        }
      ]
    }
  },
  methods: {
    addTodo(){
      if (this.inputText){
        this.todoList.push({id: (this.todoList.length+1), text: this.inputText})
        this.inputText = ''
      }
      console.log("add todo")
    },
    deleteTodo: function (todoId) {
      let item = this.todoList.map(x => {
        return x.id;
      }).indexOf(todoId);
      this.todoList.splice(item,1)
    },
    updateTodo: function () {
      if (this.inputText){
        let todoIndis = this.todoList.findIndex((x => x.id === this.updatedItemId))
        this.todoList[todoIndis].text = this.inputText
        this.inputText = ''
        this.isActionEdit = false
        this.updatedItemId = null
      }
    },
    changeUpdateButton: function (todo) {
      let item = this.todoList.find(x=>x.id === todo.id)
      this.updatedItemId = todo.id
      this.inputText = item.text
      this.isActionEdit = true
    }
  }
}
</script>

<style scoped>

</style>
