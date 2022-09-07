<template>
<div class="flex justify-center pt-6">
  <div class="">
    <div class="flex justify-center p-2">
      <label for="default-input" class="text-xl font-medium text-gray-900 dark:text-gray-300">Title</label>
    </div>
    <div>
      <input v-model="notes.title" type="text" id="default-input" class="p-2 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-full h-10 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder={{notes.title}}>
    
    </div>
    <div class="flex justify-center p-2">
      <label for="message" class=" mb-2 text-xl font-medium text-gray-900 dark:text-gray-400">Content</label>
    </div>
    <div>
      <textarea v-model="notes.content" id="message" rows="4" class="p-2 resize-none w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder={{notes.content}}></textarea>  
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
    async getPost() {
      var id = (document.location.search.substr(4))
      const res = await axios.get("http://localhost:3000/notes/"+id)
        console.log(res.data);
        this.notes = res.data;
    },
  },
}

</script>
