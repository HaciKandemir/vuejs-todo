<template>
  <div class="row" v-bind:id="todo.id">
    <div class="mx-auto col-md-7 border d-flex justify-content-between align-items-center py-2">
      <span>{{ todo.text }}</span>

      <div>
        <button class="btn btn-success mx-2" v-on:click="$emit('changeUpdateButton', todo)">Düzenle</button>
        <button class="btn btn-danger" v-on:click="$emit('deleteTodo', todo.id)">Sil</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  data: function () {
    return {
      inputText : "asd"
    }
  }
}
</script>

<style scoped>

</style>
