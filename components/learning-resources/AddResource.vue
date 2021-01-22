<template>
  <div>
    <base-modal
      v-if="inputIsInvalid"
      title="Invalid Input"
      @close="confirmError"
    >
      <template>
        <p>입력을 확인해주세요</p>
        <p>대충 에러를 안내하는 내용</p>
      </template>
      <template #actions>
        <base-button @click.native="confirmError">오케이</base-button>
      </template>
    </base-modal>
    <base-card>
      <form @submit.prevent="submitData">
        <div class="form-control">
          <label for="title">title</label>
          <input id="title" ref="titleInput" name="title" type="text" />
        </div>
        <div class="form-control">
          <label for="description">description</label>
          <textarea
            id="description"
            ref="descInput"
            name="description"
            rows="3"
          ></textarea>
        </div>
        <div class="form-control">
          <label for="link">link</label>
          <input id="link" ref="linkInput" name="link" type="url" />
        </div>
        <div>
          <base-button>Add Resource</base-button>
        </div>
      </form>
    </base-card>
  </div>
</template>
<script>
import BaseButton from '../UI/BaseButton.vue'
export default {
  components: { BaseButton },
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    }
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value
      const enteredDescription = this.$refs.descInput.value
      const enteredLink = this.$refs.linkInput.value

      // form check
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true
        return
      }
      this.addResource(enteredTitle, enteredDescription, enteredLink)
    },
    confirmError() {
      this.inputIsInvalid = false
    },
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
