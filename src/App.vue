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


.app{
  margin:auto;
  max-width: 100%;
  background: rgb(40, 40, 40);
  padding: 40px;
  color:#fff;
}

.header{
  margin:auto;
  max-width: 300px;
  display: grid;
  grid-template-rows: 1fr 1fr 1fr;
  grid-template-columns: 1fr;
  gap: 10px;
  text-align: center;
}
 .logo img{
   max-width: 400px;
   justify-content: center;
 }

.header input{
  height: 40px;
}

.header button{
  height: 40px;
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
 
}

.nome{
  color: #1b1b1b;
  font-weight: 700;
  font-size: 1rem;
  padding: 1rem 0;
  background: #00ff97;
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
}

 .personagens{
   display: flex;
   max-width: 50%;
   border-radius: 1rem;
 }

 h4{
   
   justify-content: center;
   margin: 1rem;
 }

 .informacoes{
   display: table-column;

 }



 /* template { 
    display: flex;
    justify-content: center;
    align-items: center;
    background: #111;
  
  }

  ul {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
  }
  ul li {
    list-style: none;
    width: 180px;
    height: auto;
    padding: 10px;
  }
  img {
    width: 100%;
    height: auto;
  }

 li{
   background: rgb(129, 200, 141);
   margin-bottom: 10px;
   margin-right: 10px;
  border-radius: 10px;
 }*/

</style>
