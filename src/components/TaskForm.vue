<template>
  <form @submit.prevent class="form">
    <el-input v-model="task_body"
              type="text"
              placeholder="Новая задача"
              class="form-input"/>
    <my-button @click="createNewBody" class="add-btn">Добавить</my-button>
  </form>
</template>

<script>
import MyInput from "@/components/UI/MyInput";
import MyButton from "@/components/UI/MyButton";

export default {
  name: "TaskForm",
  components: {MyButton, MyInput},
  props: {
    task: {
      type: Object,
      required: false
    }
  },
  data() {
    return {
      task_body: this.task ? this.task.task_body : ''
    }
  },
  methods: {
    createNewBody() {
      this.$emit('create', this.task_body)
      if(this.task) {
        this.task.task_body = this.task_body
        // this.task.isEditing = false
      }
      this.task_body = ''
      this.$emit('completeEdit', this.task)
      console.log("task in formtask", this.task)

    }
  }
}
</script>

<style scoped>
.form {
  display: flex;
  width: 80%;
  justify-content: center;
  /*height: 52%;*/
}

.form-input {
  width: 65%;
}

.add-btn {
}

</style>