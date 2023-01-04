<template>
  <div class="my-2">
    <h1 class="text-center text-gray-700 font-bold text-xl">Describe Your Images</h1>
    <form class="flex flex-col w-[70%] md:max-w-[40%] mx-auto gap-4 py-3">
        <input v-model="text" class="px-3 py-2 border border-gray-400 rounded" type="text" placeholder="Enter Text">
        <select v-model="size" class="px-3 py-2 border border-gray-400 rounded" name="size">
            <option disabled value="">Size</option>
            <option value="small">Small</option>
            <option value="medium">Medium</option>
            <option value="large">Large</option>
        </select>
        <button @click="submit" class="bg-gray-400 text-white px-2 py-1 rounded hover:bg-white hover:text-gray-400 border border-gray-400">Generate</button>
    </form>

    <div v-if="!error" class="flex justify-center my-3 max-w-[90%] mx-auto">
        <img :src="`data:image/jpeg;base64,${img}`" alt="">
    </div>
    <h1 class="text-center text-xl font-bold">{{ error }}</h1>
  </div>
  <div v-show="loading">
      <Loading/>
  </div>
</template>

<script>
import axios from 'axios'
import Loading from './Loading.vue'

export default {
    components : {
        Loading
    },
    data() {
        return {
            text : '',
            size : '',
            img : '',
            loading : false,
            error : null
        }
    },
    methods : {
        submit(e) {
            e.preventDefault()
            this.loading = true
            this.error = ''
            axios.post('https://excited-hare-belt.cyclic.app/openai/generateImage', {
                prompt : this.text,
                size : this.size
            }).then((response) => {
                this.img = response.data.data
                this.loading = false
            }).catch((response)=> {
                this.error =response.response.data.error
                this.loading = false
            })
        }
    }
}
</script>

<style>

</style>