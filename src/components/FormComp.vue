<template>
  <div>
    <form @submit.prevent="submitOperation" class="card p-3 bg-secondary text-white">
      <div class="form-group">
        <label>Title</label>
        <input
          type="text"
          v-model="formModel.title"
          class="form-control text-dark"
          placeholder="Please enter title"
        />
      </div>
      <div class="form-group">
        <label>Description</label>
        <textarea
          class="form-control text-dark"
          v-model="formModel.description"
          rows="3"
          placeholder="Please enter description"
        ></textarea>
      </div>
      <div class="form-group">
        <label>Status</label>
        <select class="form-control" v-model="formModel.status">
          <option value hidden disabled selected>Please Select</option>
          <option class="bg-danger text-white" value="waiting">Waiting</option>
          <option class="bg-primary text-white" value="inProgress">In Progress</option>
          <option class="bg-success text-white" value="completed">Completed</option>
        </select>
      </div>
      <br />
      <button
        type="submit"
        class="btn text-white"
        :style="isUpdate ? 'background-color:red' : 'background-color:green'"
      >{{isUpdate ? 'Update' : 'Add New'}}</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "FormComp",
  props: {
    isUpdate: {
      type: Boolean
    }
  },
  data() {
    return {
      formModel: {
        title: "",
        description: "",
        status: ""
      }
    };
  },
  methods: {
    submitOperation() {
      this.$emit("formSubmit", { ...this.formModel });
      this.clearForm();
    },
    clearForm() {
      this.formModel = {
        title: "",
        description: "",
        status: ""
      };
    }
  }
};
</script>