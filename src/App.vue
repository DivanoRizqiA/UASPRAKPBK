<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-black text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img :src="logo" alt="Logo" />
          </q-avatar>
          LaporCuaca
        </q-toolbar-title>


        <q-btn-dropdown flat icon="menu" class="text-white">
          <q-list>
            <q-item clickable tag="router-link" to="/cuaca">
              <q-item-section>
                <q-item-label>LaporCuaca</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas1">
              <q-item-section>
                <q-item-label>Tugas 1</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas2">
              <q-item-section>
                <q-item-label>Tugas 2</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas3">
              <q-item-section>
                <q-item-label>Tugas 3</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas4">
              <q-item-section>
                <q-item-label>Tugas 4</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas5">
              <q-item-section>
                <q-item-label>Tugas 5</q-item-label>
              </q-item-section>
            </q-item>
            <q-item clickable tag="router-link" to="/tugas6">
              <q-item-section>
                <q-item-label>Tugas 6</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </q-toolbar>
    </q-header>

    <router-view></router-view>

    <q-footer elevated class="bg-black text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar></q-avatar>
        </q-toolbar-title>
        <div class="text-center q-ml-auto">
          <div>Divano Rizqi Anandra</div>
        </div>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import logoImage from './assets/Logo.png';

const router = useRouter();

const logo = ref(logoImage);
const dropdownLinks = ref([
  { label: 'Tugas 1', path: '/tugas1' },
  { label: 'Tugas 2', path: '/tugas2' },
  { label: 'Tugas 3 (FREE)', path: '/tugas3' },
  { label: 'Tugas 4', path: '/tugas4' },
  { label: 'Tugas 5', path: '/tugas5' },
  { label: 'Tugas 6', path: '/tugas6' },
  { label: 'Cuaca', path: '/cuaca'},
]);

const navigate = (path) => {
  router.push(path);
};
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
}

.no-scroll {
  overflow: hidden;
}
.text-center {
  text-align: left;
}
.q-page-container {
  overflow: hidden;
}
</style>
