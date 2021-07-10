<template >

  <div class="">
    <form @submit="addOneTodo">
      <input type="text" name="title" v-model="title" placeholder="Add Todo ...">
      <input type="submit" value="Submit" class="btn">
    </form>

  </div>
</template>



<script>
// import uuid from 'uuid';
  export default {
    name: "AddTodo",
    data()  {
      return {
        title: ''
      }
    },

    methods: {

      addOneTodo(e) {
        e.preventDefault();
        const newTodo = {
        //  id: uuid.v4(), // since jsonplaceholder gives an id automatically
          title: this.title,
          completed: false
        }
        // now send it up to parents
        this.$emit('add-todo', newTodo);
        this.title = '';
      }
    }
  }

</script>


<style >

  form {
    display: flex;
  }

  input[type="text"] {
    flex: 10;
    padding: 5px;
  }

  input[type="submit"] {
    flex: 2;
  }




</style>
