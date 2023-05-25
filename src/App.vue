<script setup>
import Main from "@/components/EquipmentBox.vue";
import EquipmentBox from "@/components/EquipmentBox.vue";
import {ref} from "vue";
import EquipmentForm from "@/components/EquipmentForm.vue";

const viewAddEquipmentFormModal = ref(false);
</script>

<template>
  <main class="section">
    <h2 class="title is-2">Demo Client TPI 2023 : FullStack sur OVH</h2>
    <div class="columns is-desktop">
      <div class="column">
        <input class="input" type="text" placeholder="Search a Equipment">
      </div>
      <div class="column is-narrow-desktop">
        <button class="button is-success" @click="viewAddEquipmentFormModal = true">Add equipment</button>
      </div>
    </div>
    <div class="">
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
      <EquipmentBox/>
    </div>
    <div class="modal" :class="{'is-active': viewAddEquipmentFormModal}">
      <div class="modal-background" @click="viewAddEquipmentFormModal = false"></div>
      <div class="modal-content">
        <EquipmentForm/>
        <button class="modal-close is-large" aria-label="close"></button>
      </div>
    </div>
  </main>
</template>

<style scoped>

</style>
