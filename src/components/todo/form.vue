<template>
  <div>
    <h1>{{ question }}</h1>
    <p class="errorText" v-if="error"> {{ error }} <p>
    <p>Tasks: {{ this.toDoArr.length }}</p>
    <p>Completed: {{ completed }}</p>
    <form>
      <input v-model="toDoInput" placeholder="" />
      <button v-on:click="handleSubmit">Submit</button>
      <button v-if="toDoArr[0]" v-on:click="clearList">Clear ToDo's</button>
    </form>
    <div>
      <ul>
        <!-- To do go here.. -->
        <li v-for="(element, index) in toDoArr" v-bind:key="index">
          <input type="checkbox" v-model="element.completed" v-on:click="markDone" v-bind:id="index"> {{ element.item }} <br />
        </li>
      </ul>
    </div>
  </div>
</template>
  
<script>
  export default {
    data() {
      return {
        error: "",
        question: "What would you like to get done today?",
        toDoInput: "",
        toDoArr: [],
        completed: 0
      }
    },
    created() {
      let local = localStorage.getItem("toDos");
      if(local) this.toDoArr = JSON.parse(local); 
    },
    methods: {
      handleSubmit: function(event) {
        event.preventDefault();
        if(this.toDoInput === null || this.toDoInput === "") return this.error = "Task cannot be empty!";

        this.toDoArr.push({
          "item":this.toDoInput,
          "completed": false 
        });
        this.toDoInput = "";
        this.error = "";
        this.writeToStorage();
      },
      writeToStorage: function() {
        localStorage.setItem("toDos", JSON.stringify(this.toDoArr)); 
      },
      clearList: function(event) {
        event.preventDefault();
        this.completed = 0;
        localStorage.removeItem("toDos");
        this.toDoArr = [];
      },
      markDone: function(event) {
        if( event.target.checked == true ) { 
          this.completed++ 
        } else { 
          this.completed-- 
        }
        
        this.toDoArr[event.target.id] = {
          item: this.toDoArr[event.target.id].item,
          completed : event.target.checked
        };

        this.writeToStorage();
      }
    },
  }
</script>
  
<style> 
  .errorText {
    color: red;
  }

  ul {
    list-style-type: none;
  }

  li {
    margin-left: -43px;
    padding-bottom: 10px;
  }
</style>
