<!-- COMPONENTE SINGOLO -->
<script>
import AppCard from './AppCard.vue';

import listaCarte from '../../data/store';
// SCRIPT
export default {
  // name: AppBody,
  components: {
    // listaCarte,
    AppCard,
  },
  data() {
    return {
      listaCarte
    }
  },
  methods: {

  },
  mounted() {

  },
}
</script>

<template>
  <div class="gold">
    <div class="container">
      <div class="p-3">
        <!-- SELECT PER TIPO DI CARTA -->
        <select name="role" id="role">
          <option value="Melodious">All</option>
        </select>
      </div>
    </div>
    <div class="container">
    <!-- Sezione principale -->
      <div class="main-section p-5">
        <div class="found p-3">
          <div>Sono state trovate: {{ listaCarte.length - 1 }} carte</div>
        </div>
        <!-- QUA ANDRANNO TUTTE LE CARTE -->
        <!-- CONTENITORE CARD -->
        <div class="d-flex flex-wrap justify-content-between">
              <AppCard v-for="card in listaCarte" :nome="card.name" :imgUrl="card.card_images[0].image_url" :type="card.archetype"/>
        </div>
      </div>
    </div>
  </div>
</template>

<!-- CON SCOPED DICHIARO CSS SOLO AL ATTUALE COMPONENTE/file -->
<style scoped>
/* STILE */
.main-section{
  width: 100%;
  background-color: white;
  min-height: 20rem;
}

.found{
  background-color: #444;
  height: 4rem;
  width: 100%;
}


</style>
