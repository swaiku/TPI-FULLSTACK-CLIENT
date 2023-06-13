<script setup>
import Main from "@/components/EquipmentBox.vue";
import EquipmentBox from "@/components/EquipmentBox.vue";
import {computed, onMounted, ref} from "vue";
import EquipmentForm from "@/components/EquipmentForm.vue";
import axios from "axios";

const viewAddEquipmentFormModal = ref(false);
const equipments = ref([])
const searchBar = ref("")

const filteredEquipments = computed(() => {
  return equipments.value.filter((equipment) => {
      if (searchBar.value !== "") {
        if (!equipment.name.toLowerCase().includes(searchBar.value.toLowerCase()) &&
            !equipment.inventoryNumber.toLowerCase().includes(searchBar.value.toLowerCase())) {
          return false;
        }
      }
      return true;
  })
})

const deleteEquipment = (id) => {
  axios.delete(import.meta.env.VITE_SERVER_URL +'/equipments/' + id).then(() => {
    getAllEquipments()
  })
}

const getAllEquipments = () => {
  axios.get(import.meta.env.VITE_SERVER_URL + "/equipments").then((response) => {
    equipments.value = response.data
  })
}

onMounted(() => {
  getAllEquipments()
})
</script>

<template>
  <main class="section">
    <h2 class="title is-2">Demo Client TPI 2023 : FullStack sur OVH</h2>
    <div class="columns is-desktop">
      <div class="column">
        <input v-model="searchBar" class="input" type="text" placeholder="Search a Equipment">
      </div>
      <div class="column is-narrow-desktop">
        <button class="button is-warning" @click="viewAddEquipmentFormModal = true">Add equipment</button>
      </div>
    </div>
    <div v-if="equipments" class="">
      <EquipmentBox v-for="equipment in filteredEquipments" v-bind="equipment" @deleteEquipment="deleteEquipment(equipment.id)" @refreshEquipments="getAllEquipments()"/>
    </div>
    <div v-if="viewAddEquipmentFormModal" class="modal" :class="{'is-active': viewAddEquipmentFormModal}">
      <div class="modal-background" @click="viewAddEquipmentFormModal = false"></div>
      <div class="modal-content">
        <EquipmentForm @closeModal="viewAddEquipmentFormModal = false" @refreshEquipments="getAllEquipments()"/>
        <button class="modal-close is-large" aria-label="close"></button>
      </div>
    </div>
  </main>
</template>
