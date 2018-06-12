<template>
  <div>
    <h1>Pesquise seu Artista</h1>
    <br>

    <form @submit.prevent="submit">
      <input  size="30" placeholder="Entre com o nome do Artista" v-model="search" autofocus />
    </form>
  </div>
</template>

<script>


export default {
  components: {
  },
  data(){
    return{
      search:''
    }
  },
  methods: {
    submit(event){
      this.$router.push(`results/${this.search}`);
    }
  }
}
</script>

<style>

* {
  text-align: center;
}

h1 {
  padding: 20px;
}
</style>
