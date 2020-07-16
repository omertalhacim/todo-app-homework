<template>
  <div>
    <ValidationObserver v-slot="{ invalid }">
      <form @submit.prevent="submitOperation" class="card p-3 bg-secondary text-white">
        <div class="form-group">
          <label>Title</label>
          <ValidationProvider rules="required" v-slot="{ errors }">
            <input
              type="text"
              v-model="formModel.title"
              class="form-control text-dark"
              placeholder="Please enter title"
            />
            <span style="color: red">{{ errors[0] }}</span>
          </ValidationProvider>
        </div>
        <div class="form-group">
          <label>Description</label>
          <ValidationProvider rules="required" v-slot="{ errors }">
            <textarea
              class="form-control text-dark"
              v-model="formModel.description"
              rows="3"
              placeholder="Please enter description"
            ></textarea>
            <span style="color: red">{{ errors[0] }}</span>
          </ValidationProvider>
        </div>
        <div class="form-group">
          <label>Status</label>
          <ValidationProvider rules="required" v-slot="{ errors }">
            <select class="form-control" v-model="formModel.status">
              <option value hidden disabled selected>Please Select</option>
              <option class="bg-danger text-white" value="waiting">Waiting</option>
              <option class="bg-primary text-white" value="inProgress">In Progress</option>
              <option class="bg-success text-white" value="completed">Completed</option>
            </select>
            <span style="color: red">{{ errors[0] }}</span>
          </ValidationProvider>
        </div>
        <br />
        <button
          :disabled="invalid"
          type="submit"
          class="btn text-white"
          :style="isUpdate ? 'background-color:red' : 'background-color:green'"
        >{{isUpdate ? 'Update' : 'Add New'}}</button>
      </form>
    </ValidationObserver>
  </div>
</template>

<script>
import { ValidationProvider, extend, ValidationObserver } from "vee-validate";
import { required } from "vee-validate/dist/rules";

extend("required", {
  ...required,
  message: "*This field is required"
});

export default {
  name: "FormComp",
  components: {
    ValidationProvider,
    ValidationObserver
  },
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