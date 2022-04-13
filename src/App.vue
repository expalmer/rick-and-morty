<template>
  <div class="app">
    <div class="header"> 
      <div class="logo">
        <img src="./assets/logo.png">
      </div>
      <input v-on:keyup="search" type="text" v-model="name">
      <select v-model="species">
        <option value=""> - </option>
        <option value="Human">Humanos</option>
        <option value="Alien">Alien</option>
      </select>
      <!-- <button v-on:click="search">Search </button>  -->
    </div>
    
    <div class="card">
      <ul>
        <li v-for="personagem in list() " :key="personagem.id">
          <img class="imagemPersonagens" :src="personagem.image">
        <div class="todasInformacoes">
          <h2 class="nome">{{personagem.name}}</h2>
          <h4 class="descricao">{{personagem.species}}</h4>
          <h4 class="descricao">{{personagem.gender}}</h4>
          <h4 class="descricao">{{personagem.status}}</h4>
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
      personagens:[],
      species:""
    };
  },

  mounted() {
    fetch("https://rickandmortyapi.com/api/character")
    .then((response) => response.json())
    .then((data) => (this.personagens = data.results));
    },
  methods:{
   search(){
    console.log(this.name)
    },
    list(){
        return this.personagens.filter(personagem => {
          // return personagem.name.toLowerCase().match(this.name.toLowerCase())
          if (!this.species) return true
          return personagem.species === this.species

        })
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
  border:0;
  padding: 0.6rem;
  margin: 1rem;
  font-weight: 800;
  border-radius: 1rem;
  color: white;
  
}

.header input:hover{
  border: 1px solid #00ff97;
  background: none;
}

.header button{
  height: 40px;
  background: #002128;
  outline: none;
  border: 1px solid #002128;
  padding: 0.6rem;
  margin: 1rem;
  font-weight: 700;
  border-radius: 1rem;
  color: rgb(158, 158, 158);
  margin-bottom: 3rem;
}

.header button:hover{
  background: none;
  color:#00ff97;
  border: 1px solid #00ff97;
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

.card ul li:hover{
        -webkit-transform: scale(1.2);
        -ms-transform: scale(1.2);
        transform: scale(1.2);
        transition: all 0.3s ease;
}

.nome{
  color: #1b1b1b;
  font-weight: bold;
  font-size: 1rem;
  padding: 1rem ;
  background: #00ff97;
  border-radius: 10px;
}

.imagemPersonagens{
   max-width: 50%;
   border-radius: 1rem;
 }

.descricao{
   background: #696161;
   border-radius: 1rem;
   width: 100%;
   padding: 0px;
   margin: 0px;
   margin-bottom: 10px; 
 }
 
 .todasInformacoes {
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

@media  (max-width: 900px) {

 .logo img{
   max-width: 100%;
 }

.card{
   display: flex;
   align-items: center;
   justify-content: center;

}
  .card ul{
  width: 90%;
  grid-template-columns: 1fr;
}

  .nome{
  margin-bottom: 20px;
}
  .descricao{
   width: 96%;
   padding: 7px;
   margin: 0px;
   margin-bottom: 35px; 
 } 
}

@media  (min-width: 1400px) {
  .nome{
  margin-bottom: 10px;
}
  .descricao{
   width: 96%;
   padding: 5px;
   margin: 0;
   margin-bottom: 20px; 
 } 

}

@media  (min-width: 1500px) {
  .descricao{
   padding: 5px;
   margin: 0;
   margin-bottom: 25px; 
 } 

}


</style>

