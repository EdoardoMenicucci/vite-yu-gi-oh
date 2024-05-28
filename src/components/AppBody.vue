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
    // FUNZIONE CHE NUMERA LE CARTE SELEZIONATE PER TIPO
      cardNumber(){
        // SVUOTO L'ARRAY CONTENENTE IL TIPO SELEZIONATO
        this.ListaContenuti.cardType = 0
        for (let i = 0; i < ListaContenuti.carteApi.length; i++) {
          const element = ListaContenuti.carteApi[i];
          if (this.select == 'All') {
            this.ListaContenuti.cardType = this.ListaContenuti.carteApi.length
          }else if (element.archetype == this.select){
            this.ListaContenuti.cardType += 1
          }
        }
      } 
  },
  mounted() {
    // QUA BONUS LISTA GENERATA TRAMITE API 50 CARTE
    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=2000&offset=0').then((result) => {
      // this.listaApi = result.data.data,
      this.ListaContenuti.carteApi = result.data.data
      // 
      for (let i = 0; i < this.ListaContenuti.carteApi.length; i++) {
        const element = this.ListaContenuti.carteApi[i];
        // AGGIUNGO GLI ARCHETIPI ALL' SELECT MA NON FACCIO 'DOPPIONI'
        if (this.ListaContenuti.archetype.includes(element.archetype) || this.ListaContenuti.archetype.includes(null)){
          // NON MOSTRO QUELLI NON DEFINITI (PER EVITARE SPAZIO BIANCO NEL SELECT)
        } else if(element.archetype == undefined){
          element.archetype = 'undefined'
        }else { //IL RESTO LI PUSHO DENTRO AL ARRAY CHE CICLA SUL SELECT
          this.ListaContenuti.archetype.push(element.archetype)
          // console.log(element.archetype);
        }
        // TENGO TRACCIA DEL NUMERO DI CARTE DEL TIPO SELEZIONATO (INIZIALMENTE TUTTE)
        this.ListaContenuti.cardType = this.ListaContenuti.carteApi.length
      }
})
// INSERISCO GLI ARCHETIPI TRAMITE API
    axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php').then((r) => {
      this.ListaContenuti.archetypeApi = r.data
      console.log(r.data[0].archetype_name);
    })
  },
}
</script>

<template>
  <div class="gold">
    <div class="container">
      <div class="p-3">
        <!-- SELECT PER TIPO DI CARTA -->
        <select name="role" id="role" v-model="select" @change="cardNumber">
          <option v-for="elemento in ListaContenuti.archetypeApi" :value="elemento.archetype_name">{{ elemento.archetype_name }}</option>
        </select>
      </div>
    </div>
    <div class="container">
    <!-- Sezione principale -->
      <div class="main-section p-5">
        <div class="found p-3">
          <!-- TENGO TRACCIA DELLE CARTE A SCHERMO PER TIPO -->
          <div>Sono state trovate: {{ ListaContenuti.cardType}} carte</div>
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
