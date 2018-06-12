<template>
  <div>
    <h1> Resultados para {{$route.params.id}}</h1>

    <div v-if="albumExists">
      <div v-for="(album, index) in albumData">
         <card
            :title="album.collectionCensoredName"
            :image="album.artworkUrl100"
            :artistName="album.artistName"
            :url="album.artistViewUrl"
            :color="picker(index)"
            >
         </card>
     </div>

    </div>
  <div v-else>
      <h1>Não achei esse ser</h1>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import card from '~/components/card.vue';
export default {
  asyncData ({params}){

  return axios.get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
    .then((response) => {
      return {albumData: response.data.results}
    });
  },
  components:{
    card
  },
  methods:{
    picker(index){
      return index % 2 == 0 ? 'red' : 'blue';
    }
  },
  middleware: 'search',
  computed: {
    albumExists(){
      return this.albumData.length > 0;

    }
  }
}
</script>
