<template>
  <base-card>
    <template #default>
      <teleport to="body">
        <base-dialog v-if="isInputInvalid" title="Invalid Input" @close="closeDialog">
          <template #default>
            <p>Unfortunatly, at least one input value is invalid.</p>
            <p>
              Please check all inputs and make sure you enter at least a few
              characters into each input field.
            </p>
          </template>
          <template #actions>
            <base-button @click="closeDialog">Okay</base-button>
          </template>
        </base-dialog>
      </teleport>
      <form @submit.prevent="fetchData">
        <div class="form-control">
          <label for="title">Title</label>
          <input type="text" name="title" id="title" ref="inputTitle" />
        </div>
        <div class="form-control">
          <label for="description">Description</label>
          <textarea
            name="description"
            id="description"
            rows="3"
            ref="inputDescription"
          ></textarea>
        </div>
        <div class="form-control">
          <label for="link">Link</label>
          <input type="url" name="link" id="link" ref="inputLink" />
        </div>
        <base-button type="submit">Submit</base-button>
      </form>
    </template>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      isInputInvalid: false,
    };
  },

  inject: ['addResource'],

  methods: {
    fetchData() {
      const newId = Math.floor(Math.random() * (100 - 3) + 3);
      const enteredTitle = this.$refs.inputTitle.value;
      const enteredDescription = this.$refs.inputDescription.value;
      const enteredLink = this.$refs.inputLink.value;
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        return (this.isInputInvalid = true);
      }
      this.addResource(newId, enteredTitle, enteredDescription, enteredLink);

      this.$refs.inputTitle.value = '';
      this.$refs.inputDescription.value = '';
      this.$refs.inputLink.value = '';
    },

    closeDialog() {
      return (this.isInputInvalid = false);
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
