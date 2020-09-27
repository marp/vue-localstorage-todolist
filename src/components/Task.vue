<template>
  <li>
    <s v-if="task.done">{{ task.content }}</s>
    <span v-else>{{ task.content }}</span>
    <button @click="remove(index)">Remove</button>
    <button @click="done(index)"><span v-if="!task.done">Done</span><span v-else>Undone</span></button>
  </li>
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

</style>