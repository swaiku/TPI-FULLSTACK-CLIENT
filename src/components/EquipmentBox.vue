<script setup>
import {ref} from "vue";

const viewInformationModal = ref(false);
const viewConfirmDeleteModal = ref(false);
</script>

<template>
  <div class="box" @click="viewInformationModal = true">
    <h3 class="title">Equipment1</h3>
    <h2 class="subtitle">Inventory Number : 1234</h2>
  </div>
  <div class="modal" :class="{'is-active': viewInformationModal}">
    <div class="modal-background" @click="viewInformationModal = false"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Equipment 1</p>
        <button class="delete is-large" aria-label="close" @click="viewInformationModal = false"></button>
      </header>
      <section class="modal-card-body">
        <!-- Content ... -->
      </section>
      <footer class="modal-card-foot">
        <button class="button">Edit</button>
        <button class="button is-danger" @click="viewConfirmDeleteModal = true">Delete</button>
      </footer>
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
          <button class="button is-danger" @click="viewConfirmDeleteModal = false">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>