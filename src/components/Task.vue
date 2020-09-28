<template>
  <div class="task">
    <div class="list">
      <s v-if="task.done">{{ task.content }}</s>
      <span v-else>{{ task.content }}</span>
    </div>
    <div class="buttons">
      <button @click="remove(index)">Remove</button>
      <button @click="done(index)"><span v-if="!task.done">Done</span><span v-else>Undone</span></button>
    </div>
  </div>
  <div style="clear: both;"></div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
    index: Number
  },
  methods:{
    remove(index){
      this.$emit('remove', index);
    },
    done(index){
      this.$emit('done', index);
    }
  }
}
</script>

<style scoped>
 .task{
   border-bottom: black solid 1px;
   background-color: white;
   padding: 5px;
   width: 98%;
   text-align: right;
 }
 .list{
   padding-top: 5px;
   float: left;
   margin-right: auto;
 }
 s{
    color: darkgray;
 }
 .buttons{
   display: inline;
 }
 .buttons > button{
   height: 25px;
 }
</style>