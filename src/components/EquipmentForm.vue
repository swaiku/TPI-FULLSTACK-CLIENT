<script setup>
import {computed, ref} from "vue";

const nameInput = ref()
const inventoryNumber = ref()

const nameError = computed(() => {
  let result = "";
  if (nameInput.value === "") {
    result.concat(this,"name invalid : cannot be empty \n")
  }
  if (inventoryNumber.value === "") {
    result.concat(this,"inventoryNumber invalid : cannot be empty \n")
  }
  if (result === "") {
  } else {
    return result;
  }
})
</script>

<template>
  <div class="box">
    <h1 class="title">Add equipment</h1>
    <article v-if="nameError" class="message is-danger">
      <div class="message-body">
        <h5 class="title is-5">Invalid Values</h5>
        {{ nameError }}
      </div>
    </article>
    <form>
      <div class="field">
        <label class="label">Name *</label>
        <div class="control">
          <input v-model="nameInput" class="input" :class="{'is-danger': nameError}" maxlength="45" type="text" placeholder="e.g. Access Point Cisco" required>
        </div>
      </div>
      <div class="field">
        <label class="label">Inventory number *</label>
        <div class="control">
          <input v-model="inventoryNumber" class="input" maxlength="45" type="text" placeholder="e.g. EMF-INFO-1234" required>
        </div>
      </div>
      <div class="field">
        <label class="label">Serial number</label>
        <div class="control">
          <input class="input" maxlength="50" type="text" placeholder="e.g. ABC12345678">
        </div>
      </div>
      <div class="field">
        <label class="label">Purchase price</label>
        <div class="control">
          <input class="input" step=".05" type="number" placeholder="e.g. 100.00">
        </div>
      </div>
      <div class="field">
        <label class="label">Purchase date</label>
        <div class="control">
          <input class="input" type="date">
        </div>
      </div>
      <div class="buttons">
        <button class="button is-primary">Add equipment</button>
        <button class="button">Cancel</button>
      </div>
    </form>
  </div>
</template>

<style scoped>

</style>