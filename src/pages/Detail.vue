<template>
  <div v-if="book">
    <img :src="book.volumeInfo.imageLinks.thumbnail" alt="">
    <p>タイトル : {{ book.volumeInfo.title }}</p>
    <p>サブタイトル : {{ book.volumeInfo.subtitle }}</p>
    <p>説明 : {{ book.volumeInfo.description }}</p>
    <a v-if="book.saleInfo.buyLink" target="_blank" :href="book.saleInfo.buyLink">購入ページへ</a>
  </div>
</template>

<script>
import axios from 'axios'
const ENDPOINT = 'https://www.googleapis.com/books/v1/volumes'
export default {
  data() {
    return {
      book: null
    }
  },
  created() {
    const id = this.$route.params.id
    axios.get(`${ENDPOINT}/${id}`).then((res) => {
      if (res.data) {
        this.book = res.data
      }
    })
  }
}
</script>

<style scoped>

</style>