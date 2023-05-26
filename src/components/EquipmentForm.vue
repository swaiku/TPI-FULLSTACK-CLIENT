<script setup>
import {onMounted, ref} from "vue";

const nameInput = ref()
const dateInput = ref(new Date().toISOString().substring(10,0))
const inventoryNumberInput = ref()
const serialNumberInput = ref()
const buyPriceInput = ref(100)
const errors = ref([])
const responseError = ref()
import axios from "axios";

const emit = defineEmits(["closeModal", "refreshEquipments"])
const props = defineProps({
  id: Number,
  name: String,
  inventoryNumber: String,
  serialNumber: String,
  buyPrice: Number,
  buyDate: String
})

const isEdit = ref(false)

onMounted(() => {
  if(props.id !== undefined) {
    isEdit.value = true
    nameInput.value = props.name
    inventoryNumberInput.value = props.inventoryNumber
    serialNumberInput.value = props.serialNumber
    buyPriceInput.value = props.buyPrice
    dateInput.value = props.buyDate
  }
})
const submitForm = () => {
  errors.value = []
  if (!nameInput.value) {
    errors.value.push("name invalid : cannot be empty");
  }
  if (!inventoryNumberInput.value) {
    errors.value.push("inventoryNumber invalid : cannot be empty");
  }
  if (errors.value.length === 0) {
    if (isEdit.value) {
      axios.put("http://localhost:8181/equipments/" + props.id, {
        name: nameInput.value,
        inventoryNumber: inventoryNumberInput.value,
        serialNumber: serialNumberInput.value ? serialNumberInput.value : null,
        buyPrice: buyPriceInput.value,
        buyDate: dateInput.value
      }).then(() => {
        emit("refreshEquipments")
        emit('closeModal')
      }).catch((error) => {
        console.log(error)
        responseError.value = error
      })
    } else {
      axios.post("http://localhost:8181/equipments", {
        name: nameInput.value,
        inventoryNumber: inventoryNumberInput.value,
        serialNumber: serialNumberInput.value ? serialNumberInput.value : null,
        buyPrice: buyPriceInput.value,
        buyDate: dateInput.value
      }).then(() => {
        emit("refreshEquipments")
        emit('closeModal')
      }).catch((error) => {
        console.log(error)
        responseError.value = error
      })
    }
  }
}
</script>

<template>
  <div class="box">
    <h1 class="title">{{ isEdit ? "Edit" : "Add"}} equipment</h1>
    <article v-if="responseError" class="message is-small is-danger">
      <div class="message-body">
        {{ responseError }} : {{ responseError.response.data.message }}
      </div>
    </article>
    <article v-if="errors.length" class="message is-small is-danger">
      <div class="message-body">
        <p v-for="error in errors">{{ error }}</p>
      </div>
    </article>
    <form class="block">
      <div class="field">
        <label class="label">Name *</label>
        <div class="control">
          <input v-model="nameInput" class="input" maxlength="45" type="text" placeholder="e.g. Access Point Cisco"
                 required>
        </div>
      </div>
      <div class="field">
        <label class="label">Inventory number *</label>
        <div class="control">
          <input v-model="inventoryNumberInput" class="input" maxlength="45" type="text" placeholder="e.g. EMF-INFO-1234"
                 required :disabled="isEdit">
        </div>
      </div>
      <div class="field">
        <label class="label">Serial number</label>
        <div class="control">
          <input class="input" v-model="serialNumberInput" maxlength="50" type="text" placeholder="e.g. ABC12345678">
        </div>
      </div>
      <div class="field">
        <label class="label">Purchase price</label>
        <div class="control">
          <input v-model="buyPriceInput" class="input" step="1" min="0" type="number" placeholder="e.g. 100">
        </div>
      </div>
      <div class="field">
        <label class="label">Purchase date</label>
        <div class="control">
          <input v-model="dateInput" class="input" type="date" :max="new Date().toISOString().substring(10,0)">
        </div>
      </div>
    </form>
    <div class="buttons">
      <button class="button is-primary" @click="submitForm">{{ isEdit ? "Edit" : "Add"}} equipment</button>
      <button class="button" @click="emit('closeModal')">Cancel</button>
    </div>
  </div>
</template>