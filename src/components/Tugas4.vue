<template>
  <div class="layar">
    <iframe src="https://tugas4pbkdivano.netlify.app/" frameborder="0" width="100%" height="100%"></iframe>
  </div>
</template>

<script setup>
defineOptions({
  name: 'Tugas4'
});
</script>

<style scoped>
.layar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: white;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

iframe {
  border: none;
}
</style>
