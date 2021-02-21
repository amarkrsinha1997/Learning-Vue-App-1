<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>All input field should be valid and not empty</p>
      <p>Please check all the input value</p>
    </template>
    <template #actions>
      <base-button @click="confirmError"> Okay </base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input ref="title" id="title" name="title" type="text" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          ref="description"
          name="description"
          id="description"
          rows="3"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input ref="link" id="link" name="link" type="url" />
      </div>
      <base-button type="submit"> Submit </base-button>
    </form>
  </base-card>
</template>


<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const refs = this.$refs;
      const title = refs.title.value;
      const description = refs.description.value;
      const link = refs.link.value;

      if (
        title.trim() === '' ||
        description.trim() === '' ||
        link.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource({
        title,
        description,
        link,
      });
    },
    confirmError() {
      this.inputIsInvalid = false;
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
  border-radius: 5px;
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