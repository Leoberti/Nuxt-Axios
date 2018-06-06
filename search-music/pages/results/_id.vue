<template>
  <div>
    <h1> Resultados para {{$route.params.id}}</h1>
    <div v-if="albumExists">
  {{albumData}}
    </div>
  <div v-else>
      <h1>Não achei esse ser</h1>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  asyncData ({params}){

  return axios.get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
    .then((response) => {
      return {albumData: response.data.results}
    });
  },
  middleware: 'search',
  computed: {
    albumExists(){
      return this.albumData.length > 0;

    }
  }
}
</script>
