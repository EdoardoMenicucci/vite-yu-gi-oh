<!-- COMPONENTE SINGOLO -->
<script>
// import listaCarte from '../../data/store';
// SCRIPT
export default {
  props:{
    nome : String,
    imgUrl : String,
    type : String,
    select : String
  },
  // name: AppCard,
  components:{
    // listaCarte,
  },
  data() {
    return {

    }
  },
  methods: {

  },
  mounted() {

  },
}
</script>

<template>
  <!-- TEMPLATE html-->
  <div v-if="select == 'All'" class="box-card gold mb-3">
     <img :src="imgUrl" alt="">
     <div>{{ nome }}</div>
     <div class="smaller">{{ type }}</div>
  </div>
  <div v-else-if="select == type" class="box-card gold mb-3">
     <img :src="imgUrl" alt="">
     <div>{{ nome }}</div>
     <div class="smaller">{{ type }}</div>
  </div>
</template>

<!-- CON SCOPED DICHIARO CSS SOLO AL ATTUALE COMPONENTE/file -->
<style scoped>
/* STILE */
img{
  width:100%;
}

.box-card{
  width: calc(100% / 4 - 6rem);
  height: 25rem;
  font-size: 1.1rem;
  font-weight: 700;
  text-align: center;
}

.smaller{
  font-size: 1rem;
  color: black;
}



</style>
