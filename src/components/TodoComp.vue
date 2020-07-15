<template>
  <div>
    <ul class="list-unstyled">
      <li v-for="listItem in todoList" :key="listItem">
        <div class="card p-2" :class="cardStyle(listItem)">
          <div class="row">
            <h5 class="col ml-2 mt-2 text-white">{{listItem.title}}</h5>
            <button @click="goToUpdateForm(listItem)" class="col-auto mr-4 mt-2">Edit</button>
          </div>
          <article class="ml-2 mb-2 text-body">{{listItem.description}}</article>
        </div>
        <br />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoComp",
  props: {
    todoList: {
      type: Array
    },
    selectedStatus: {
      type: String
    }
  },
  methods: {
    goToUpdateForm(selectedListItem) {
      this.$emit("onUpdate", selectedListItem);
    },
    cardStyle(listItem) {
      if (listItem.status == "waiting") {
        return "bg-danger";
      } else if (listItem.status == "inProgress") {
        return "bg-primary";
      } else {
        return "bg-success";
      }
    }
  }
};
</script>