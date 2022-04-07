<template>
  <div class="app">
    <div class="header"> 
      <div class="logo">
        <img src="https://logosmarcas.net/wp-content/uploads/2022/01/Rick-And-Morty-Logo.png">
      </div>
      <input type="text" v-model="name">
      <button v-on:click="search">Pesquisar </button> 
    </div>
    
    <div class="card">
      <ul>
        <li v-for="personagem in personagens" :key="personagem.id">
          <img class="personagens" :src="personagem.image">
        <div class="informacoes">
          <h2 class="nome">{{personagem.name}}</h2>
          <h4>{{personagem.species}}</h4>
          <h4>{{personagem.gender}}</h4>
          <h4>{{personagem.status}}</h4>
        </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      personagens:[]
    };
  },

  mounted() {
    fetch("https://rickandmortyapi.com/api/character")
    .then((response) => response.json())
    .then((data) => (this.personagens = data.results));
    },
  methods:{
    search(){
    fetch(`https://rickandmortyapi.com/api/character?name=${this.name}`)
    .then((response) => response.json())
    .then((data) => (this.personagens = data.results));
    }
  }
  
};
</script>

<style>

body{
 background: rgb(40, 40, 40);
}

.app{
  margin:auto;
  max-width: 100%;
  padding: 40px;
  color:#fff;
}

.header{
  margin:auto;
  max-width: 300px;
  gap: 10px;
  display: flex;
  flex-direction: column;
}
 .logo img{
   max-width: 400px;
   justify-content: center;
 }

.header input{
  height: 30px;
  background: #002128;
  outline: none;
  border: 0;
  padding: 0.6rem;
  margin: 1rem;
  font-weight: 800;
  border-radius: 1rem;
  color: white;
  
}

.header button{
   height: 40px;
  background: #002128;
  outline: none;
  border: 0;
  padding: 0.6rem;
  margin: 1rem;
  font-weight: 700;
  border-radius: 1rem;
  color: rgb(158, 158, 158);
}



.card ul{
  margin: 0px;
  padding: 0px;
  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: 1fr 1fr 1fr;
  flex-wrap: wrap;
  gap: 20px 20px;
  
}

.card ul li{
 background: #002128;
 padding: 1rem;
 border-radius: 1rem;
 list-style: none;
 display: flex;
 margin: 0px;
 font-family: Arial, Helvetica, sans-serif;
 text-align: center;

}

.nome{
  color: #1b1b1b;
  font-weight: bold;
  font-size: 1rem;
  padding: 1rem ;
  background: #00ff97;
  border-radius: 10px;
}

.personagens{
   max-width: 50%;
   border-radius: 1rem;
 }

h4{
   background: #696161;
   border-radius: 1rem;
   width: 100%;
   padding: 0px;
   margin: 0px;
   margin-bottom: 10px;
  
   
 }
 
 .informacoes {
   padding: 0.4rem;
   text-align:center;
   color: white;
   border-radius: 1rem;
   display: table-column;
   justify-content: center;
   margin: 0 auto;
   font-weight: inherit;
   width: 100%;
 }

</style>