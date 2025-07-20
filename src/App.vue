<!-- Bloc Note de Serigne Abdou Khadre Mbacké SANKHARE -->

<script>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

export default{
  name : 'App',
  data(){
    return{
      newNote : '',
      newCategorie : '',
      notes : [],
      categories : ['Travail', 'Urgent', 'Hater', 'Autre'],
    }
  },

  methods : {
    addNote(){
      // console.log(this.newNote.trim())

      if(this.newNote.trim() === ""){
        // console.log("Note Invalide")
        return false;
      }

      if(this.newNote.length > 100){
        alert("Note trop grande. La note ne doit pas dépasser 100 caractères");
        return false;
      }

      const now = new Date();
      const dateStr = now.toLocaleString();


      this.notes.push({
        text : this.newNote.trim(),
        date : dateStr,
        categorie : this.newCategorie.trim(),
      });
      alert("Note ajoutér avec succès 👍");
      this.newNote = '';
      this.newCategorie = '';
    },

    deleteNote(index){
      if(window.confirm("Voulez-vous vraiment supprier cette note ?")){
        this.notes.splice(index, 1);
      }
    },


  }
}
</script>

<template>
  <div class="container">
    <h1>Mon Block Notes</h1>

    <input type="text" v-model = "newNote" placeholder="Ajoute ta note zeubi ...">
    <select v-model="newCategorie">
      <option value="">Choisir une catégorie</option>
      <option v-for="cat in categories" :key = "cat" :value = "cat">{{ cat }}</option>
    </select><br>
    <button @click="addNote"> Ajouter</button>

    <ul>
      <li v-for="(note, index) in notes" :key = "index">
        <span class="text-note">{{ note.text }}</span><br>
        <span class="date">{{ note.date }}</span><br> <!--  Ajouter du style -->
        <span class="categorie" v-if="note.categorie">
          <p>Catégorie:</p>
          {{ note.categorie }}
        </span><br> <!--  Ajouter du style -->
        <button @click="deleteNote(index)">🗑️</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .container{
    max-width: 600px;
    height: auto;
    margin: 40px auto;
    padding: 24px;
    background: linear-gradient(90deg,rgba(42, 123, 155, 1) 0%, rgba(87, 199, 133, 1) 50%, rgba(237, 221, 83, 1) 100%);    border-radius: 12px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.08);
  }

  h1{
    text-align: center;
    margin-bottom: 24px;
    color: #333;
    font-size: 2rem;
    font-weight: bold;
  }

  input[type="text"]{
    width: 70%;
    padding: 10px;
    margin-right: 10px;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 1rem;
    box-shadow: border-box;
  }
  input{
    margin-bottom: 10px;
  }

  button{
    padding: 10px 20px;
    border-radius: 6px;
    border: none;
    background: #333;
    color: #fff;
    font-size: 1rem;
    cursor: pointer;
    box-shadow: border-box;
    transition: all 0.3s ease-in-out; 
    margin-top: 10px;
  }

  button:hover{
    transform: scale(1.1);
    transition: all 0.3s ease-in-out;
  }


  ul{
    margin-top: 5%;
    list-style: none;
    padding: 0;
    width: auto;
  }

  li{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 10px;
    background: #fff;
    padding: 10px 16px;
    border-radius: 6px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.05);
    font-size: 1rem;
  }

  .date{
    font-size: x-small;
    color: green;
    margin-left: 15px;
    margin-right: 15px;
  }

  .categorie{
    font-size: smaller;
    color: red;
    margin-right: 15px;
  }

  .categorie p{
    color: black;
  }

  @media (max-width: 700px){
    .container{
      padding: 10px;
      max-width: 98vw;
    }

    input[type="text"], select{
      width: 100%;
      margin-right: 0;
      margin-bottom: 10px;
      font-size: 1rem;
    }

    ul{
      width: 100%;
    }
    
    li{
      padding: 8px 8px;
      font-size: 0.95rem;
    }
  }
</style>
