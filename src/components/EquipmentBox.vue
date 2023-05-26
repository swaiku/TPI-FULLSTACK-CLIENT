<script setup>
import {ref} from "vue";
import EquipmentForm from "@/components/EquipmentForm.vue";

const viewInformationModal = ref(false)
const viewConfirmDeleteModal = ref(false)
const viewEditForm = ref(false)

const emit = defineEmits(["deleteEquipment", "refreshEquipments"])

const props = defineProps({
  id: Number,
  name: String,
  inventoryNumber: String,
  serialNumber: String,
  buyPrice: Number,
  buyDate: String
})

const confirmDeleteEquipment = () => {
  emit('deleteEquipment')
  viewConfirmDeleteModal.value = false
}
</script>

<template>
  <div class="box" @click="viewInformationModal = true">
    <h3 class="title">{{ props.name }}</h3>
    <h2 class="subtitle">Inventory Number : {{ props.inventoryNumber }}</h2>
  </div>
  <div class="modal" :class="{'is-active': viewInformationModal}">
    <div class="modal-background" @click="viewInformationModal = false"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">{{ props.name }}</p>
        <button class="delete is-large" aria-label="close" @click="viewInformationModal = false"></button>
      </header>
      <section class="modal-card-body">
        <table class="table is-fullwidth">
          <tbody>
          <tr>
            <th>Name</th>
            <td>{{ props.name }}</td>
          </tr>
          <tr>
            <th>Inventory number</th>
            <td>{{ props.inventoryNumber }}</td>
          </tr>
          <tr>
            <th>Serial number</th>
            <td>{{ props.serialNumber }}</td>
          </tr>
          <tr>
            <th>Purchase price</th>
            <td>{{ props.buyPrice }} .-</td>
          </tr>
          <tr>
            <th>Purchase date</th>
            <td>{{ props.buyDate }}</td>
          </tr>
          </tbody>
        </table>
      </section>
      <footer class="modal-card-foot">
        <button class="button" @click="viewEditForm = true">Edit</button>
        <button class="button is-danger" @click="viewConfirmDeleteModal = true">Delete</button>
      </footer>
    </div>
  </div>
  <div v-if="viewEditForm" class="modal" :class="{'is-active': viewEditForm}">
    <div class="modal-background" @click="viewEditForm = false"></div>
    <div class="modal-content">
      <EquipmentForm v-bind="props" @closeModal="viewEditForm = false" @refreshEquipments="emit('refreshEquipments')"/>
      <button class="modal-close is-large" aria-label="close"></button>
    </div>
  </div>
  <div class="modal" :class="{'is-active': viewConfirmDeleteModal}">
    <div class="modal-background" @click="viewConfirmDeleteModal = false"></div>
    <div class="modal-content">
      <div class="box">
        <h1 class="title">Confirm Delete ?</h1>
        <button class="modal-close is-large" aria-label="close"></button>
        <div class="buttons">
          <button class="button" @click="viewConfirmDeleteModal = false">Cancel</button>
          <button class="button is-danger" @click="confirmDeleteEquipment">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>