<!-- GRANDE CONTENITORE IN CUI VERRANNO INSERITI UNO AD UNO TUTTTI I COMPONENTI -->
<script>
// COME IMPORTARE COMPONENTI IMPORT - NOME - FROM - PERCORSO
import AppBody from './components/AppBody.vue';
import AppHeader from './components/AppHeader.vue';

// SCRIPT
export default {
  // QUA DICHIARO I COMPONENTI IMPORTATI
  components: {
    // ESEMPIO DI INPORT COMPONENTE
    AppHeader,
    AppBody,
  },
  data() {
    return {

    }
  },
  methods: {
    //PER PRENDERE FILE DA ASSETS
    getImg(path) {
        let risultato = new URL("../assets/img/" + path, import.meta.url);
        return risultato.href;
    },
  },
  mounted() {

  },
}
</script>

<template>
  <!-- TEMPLATE html-->
  <AppHeader />
  <AppBody />
</template>

<style>
/* STILE */
</style>
