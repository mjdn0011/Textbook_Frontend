// Presentational Component

<template>
  <div>
    <transition-group name="list" tag="ul">
      <!-- v-for="([element], [index])" / v-bind:key="[element]"-->
      <li class="shadow" v-for="(todoItem, index) in this.$store.state.todoItems" v-bind:key="todoItem.item">
        <!-- v-bind:class="{ [className]: boolean }" -->
        <i 
          class="checkBtn fa fa-check" 
          aria-hidden="true" 
          v-bind:class="{ checkBtnCompleted: todoItem.completed }" 
          v-on:click="toggleComplete(todoItem, index)">
        </i>
        <span v-bind:class="{ textCompleted: todoItem.completed }">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fa fa-trash" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ['propsData'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeItem', todoItem, index)    
    },
    toggleComplete(todoItem, index) {
      this.$emit('toggleItem', todoItem, index)
    },
  },
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.removeBtn:hover {
  cursor: pointer;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
/* list item transition effect */
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 0.5s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>