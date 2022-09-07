<template>
<section id="info">
  <div class="row">
    <div v-for="note in noteData.notes" :key='note.id' class="card">
      <div style="display: none;">{{note.id}}</div>
      <h2>{{note.title}}</h2>
      <div v-for="str in note.content">
      {{str}}
      </div>
      <button v-on:click="editPost(note.id)">Edit</button>
      <button v-on:click="deletedPost(note.id)">Delete</button>
    </div>
  </div>
</section>
</template>

<script>

import axios from "axios"

export default{
  
  data() {
    return {
      noteData: {
        notes: [{
          id: 0,
          title: '',
          content: [],  
        }]
      }
    }
  },
  methods: {
    getAllNotes () {
      axios ({
        method: 'get',
        url: 'http://localhost:3000/notes',
      })
      .then(res => {
        console.log(res.data.notes);
        this.noteData.notes = res.data.notes;
      })
      .catch(function (erreur) {
        console.log(erreur);
      })
    },
    deletedPost(id) {
      axios.delete("http://localhost:3000/notes/"+id)
      .then(() => {
        return this.getAllNotes()
      })
      },
    editPost(id) {
      
      location = "/Edit:"+id
    },
  },
  created: function() {
    this.getAllNotes();
  }
}

</script>

<style>

.card{
  margin:2%;
  display: inline-block;
}

.row{
  display: grid;
  grid-template-columns: 500px 500px 500px;
}

</style>