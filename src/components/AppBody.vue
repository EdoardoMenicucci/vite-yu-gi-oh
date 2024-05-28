<!-- COMPONENTE SINGOLO -->
<script>
import AppCard from './AppCard.vue';
// QUA ESERCIZIO SVOLTO TRAMITE UNA VARIABILE ESPORTATA DA UN FILE JS CLASSICO
// import listaCarte from '../../data/store';
import ListaContenuti from '../../data/store';
// SCRIPT
export default {
  // name: AppBody,
  components: {
    // listaCarte,
    AppCard,
  },
  data() {
    return {
      ListaContenuti,
      select :'All'
    }
  },
  methods: {

  },
  computed: {
        
  },
  mounted() {
    // QUA BONUS LISTA GENERATA TRAMITE API 50 CARTE
    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=50&offset=0').then((result) => {
      // this.listaApi = result.data.data,
      this.ListaContenuti.carteApi = result.data.data
      for (let i = 0; i < this.ListaContenuti.carteApi.length; i++) {
        const element = this.ListaContenuti.carteApi[i];
        // console.log(element.archetype);
        if (this.ListaContenuti.archetype.includes(element.archetype) || this.ListaContenuti.archetype.includes(null)){
          // console.log(element.archetype,'gia contenuto');
        } else if(element.archetype == NaN){
          element.archetype = 'undefined'
        }else {
          this.ListaContenuti.archetype.push(element.archetype)
          console.log(element.archetype);
        }
        
      }
})
    // this.selectArche()
  },
}
</script>

<template>
  <div class="gold">
    <div class="container">
      <div class="p-3">
        <!-- SELECT PER TIPO DI CARTA -->
        <select name="role" id="role" v-model="select">
          <option v-for="elemento in ListaContenuti.archetype" :value="elemento">{{ elemento }}</option>
        </select>
      </div>
    </div>
    <div class="container">
    <!-- Sezione principale -->
      <div class="main-section p-5">
        <div class="found p-3">
          <div>Sono state trovate: {{ ListaContenuti.carteApi.length}} carte</div>
        </div>
        <!-- QUA ANDRANNO TUTTE LE CARTE -->
        <!-- CONTENITORE CARD -->
        <div class="d-flex flex-wrap justify-content-between">
          <!-- LISTA API LISTA TRAMITE AXIOS CON 50 CARTE LISTACARTE LISTA SU FOGLIO JS -->
            <AppCard v-for="card in ListaContenuti.carteApi" :nome="card.name" :imgUrl="card.card_images[0].image_url" :type="card.archetype" :select="select"/>
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
  font-weight: 700;
}


</style>
