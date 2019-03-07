<template>
  <div>
    <form @submit.prevent="submit">
      <input v-model="text">
      <button type="submit">submit</button>
    </form>
  </div>
</template>
<<script>
export default {
  data(){
    return{
      text :''
    };
  },
  methods: {
    submit(){
      this.$emit("addTodoItem",this.text);
      this.text='';
    }
  },
}
</script>