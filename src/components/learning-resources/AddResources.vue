<template>
  <base-dialog v-if="invalidInput" title="Invaild Input">
    <template #default>
      <p>
        Unfortunatly, one or more input is invalid.
      </p>
      <p>Please provide a valid inputs.</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Confirm</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label>Title</label>
        <input type="text" v-model="title" />
      </div>
      <div class="form-control">
        <label>Description</label>
        <textarea v-model="description" />
      </div>
      <div class="form-control">
        <label>Url</label>
        <input type="text" v-model="url" />
      </div>
      <base-button>
        Add Resource
      </base-button>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      invalidInput: false,
      title: "",
      description: "",
      url: "",
    };
  },
  inject: ["addResource"],
  methods: {
    submitData() {
      if (
        this.title.trim() === "" ||
        this.description.trim() === "" ||
        this.url.trim() === ""
      ) {
        this.invalidInput = true;
        return;
      }
      this.addResource(this.title, this.description, this.url);
      this.resetInputs();
    },
    resetInputs() {
      this.title = "";
      this.description = "";
      this.url = "";
    },
    confirmError() {
      this.invalidInput = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
