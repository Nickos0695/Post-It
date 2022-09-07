<template>
<div class="flex justify-center pt-6 pb-6">
  <div class="block p-6 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700">
    <div class="flex justify-center p-2">
      <label for="default-input" class="text-xl font-medium text-gray-900 dark:text-gray-300">Title</label>
    </div>
    <div>
      <input v-model="notes.title" type="text" id="default-input" class="p-2 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-full h-10 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Edit note title...">
    
    </div>
    <div class="flex justify-center p-2">
      <label for="message" class=" mb-2 text-xl font-medium text-gray-900 dark:text-gray-400">Content</label>
    </div>
    <div>
      <textarea v-model="notes.content" id="message" rows="4" class="p-2 resize-none w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Edit note content..."></textarea>  
    </div>
    <div class="pt-2 flex justify-between">
      <button @click="editPost()" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 h-12 w-36 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Edit</button>
      <button @click="Home()" class="text-white bg-gray-800 hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 w-36 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700">Back</button>
    </div>
  </div>
</div>
</template>


<script>
import axios from "axios"

export default{

  data() {
    return {
      notes: {
        title: '',
        content: '',
      }
    }
  },

  methods:{
    editPost(id) {
      var id = (document.location.search.substr(4))
      const editNote = {
      title : this.notes.title,
      content : [this.notes.content],
      }
      if (this.notes.title === ""){
        alert("Right a note title !")
        }
      else {
        axios.put("http://localhost:3000/notes/"+id, editNote).then(res => console.log(res.data)),
        alert("Your note has been edited !")
        location = "/";
        }
    },
    Home(){
      location = "/";
    }
  },
}

</script>

<style scoped>
</style>