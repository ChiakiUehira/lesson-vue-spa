<template>
  <div>
    <div>Indexページです</div>
    <div v-for="book in books" :key="book.id">
      <router-link :to="`/detail/${book.id}`">
        <img :src="book.volumeInfo.imageLinks.thumbnail" alt="">
        <p>タイトル : {{ book.volumeInfo.title }}</p>
        <p>サブタイトル : {{ book.volumeInfo.subtitle }}</p>
      </router-link>
      <hr>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
const ENDPOINT = 'https://www.googleapis.com/books/v1/volumes'
const CONFIG = {
  params: {
    q: 'Vuejs'
  }
}
export default {
  data() {
    return {
      books: []
    }
  },
  created() {
    axios.get(ENDPOINT, CONFIG).then((res) => {
      if (res.data) {
        this.books = res.data.items
      }
    })
  }
}
</script>

<style scoped>

</style>