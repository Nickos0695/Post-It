<template>
<div class="flex flex-wrap justify-center pb-4">
  <div v-for="note in noteData.notes" :key='note.id' class="m-5 block p-6 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700">
    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{note.title}}</h5>
    <p v-for="str in note.content" class="font-normal text-gray-700 dark:text-gray-400">{{str}}</p>
    <div class="flex justify-between">
      <button  @click="deletedPost(note.id)" type="button" class="mt-5 focus:outline-none text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-900">Delete</button>
      <button @click="editPost(note.id)" type="button" class="mt-5 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Edit</button>
    </div>
  </div>
</div>

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
      if (confirm('Are you sure you want to delete this post ?')) {     
        axios.delete("http://localhost:3000/notes/"+id)
        .then(() => {
            alert('Note deleted !');
            location.reload();
      })
        .catch(function (erreur) {
            console.log(erreur);
      })}
    },
    editPost(id) {
        location = "/Edit?id="+id
        },
  },
  created: function() {
    this.getAllNotes();
  }
}

</script>

<style>
</style>