<template>
  <div>
    <FormComp @formSubmit="formOperation" ref="updateForm" :isUpdate="isUpdate" class="p-4" />
    <label class="ml-4">Show:</label>
    <select v-model="selectedStatus" class="ml-2">
      <option value="all" selected>All</option>
      <option value="waiting">Waiting</option>
      <option value="inProgress">In Progress</option>
      <option value="completed">Completed</option>
    </select>
    <TodoComp
      @onUpdate="updateTodoItem"
      :todoList="getFilteredList"
      :selectedStatus="selectedStatus"
      class="p-4"
    />
  </div>
</template>

<script>
import FormComp from "./components/FormComp.vue";
import TodoComp from "./components/TodoComp.vue";

export default {
  name: "App",
  components: {
    FormComp,
    TodoComp
  },
  data() {
    return {
      todoList: [],
      selectedStatus: "all",
      updateIndex: null,
      isUpdate: false
    };
  },
  methods: {
    formOperation(formValues) {
      if (!this.isUpdate) {
        this.todoList.push(formValues);
      } else {
        this.todoList.splice(this.updateIndex, 1, formValues);
        this.isUpdate = false;
      }
    },
    updateTodoItem(data) {
      this.isUpdate = true;
      this.updateIndex = this.todoList.indexOf(data);
      this.$refs.updateForm.formModel = { ...data };
    }
  },
  computed: {
    getFilteredList() {
      if (this.selectedStatus != "all") {
        return this.todoList.filter(item => item.status == this.selectedStatus);
      } else {
        return this.todoList;
      }
    }
  }
};
</script>