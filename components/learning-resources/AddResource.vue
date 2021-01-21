<template>
  <base-card>
    <form>
      <div class="form-control">
        <label for="title"></label>
        <input id="title" ref="titleInput" name="title" type="text" />
      </div>
      <div class="form-control">
        <label for="description"></label>
        <textarea
          id="description"
          ref="descInput"
          name="description"
          rows="3"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link"></label>
        <input id="linkInput" ref="link" name="link" type="url" />
      </div>
      <div>
        <base-button>Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
export default {
  methods: {
    // submitData() {
    //   const enteredTitle = this.$refs.titleInput.value
    //   const enteredDescription = this.$refs.descInput.value
    //   const enteredLink = this.$refs.linkInput.value
    // },
  },
}
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
