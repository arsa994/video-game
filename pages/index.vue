<template>
  <div class="container mx-auto py-16">
    <h1 class="font-heading uppercase mb-8">Popular Games</h1>
    <div class="game-container flex flex-wrap -mx-4">
      <nuxt-link :to="'games/'+ game.id" v-for="game in games" :key="game.id" class="w-full md:w-1/5 px-4 mb-12 no-underline">
        <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover">
        <div class="text-black font-semibold text-lg overflow-hidden whitespace-no-wrap overflow-dots">{{game.name}}</div>
        <div class="text-grey-darker text-base overflow-hidden whitespace-no-wrap overflow-dots pb-1">{{game.genres[0].name}}</div>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
export default {
  components: {
    Logo
  },
  // created() {
  //   games = response.data
  // },
  asyncData ({ params, error }) {
    return axios.get(`https://cors-anywhere.herokuapp.com/https://api-v3.igdb.com/games/?fields=name,cover.url,genres.name,popularity&order=popularity:desc`)
    .then((res) => {
      return { 
        games: res.data 
        }
    })
    .catch((e) => {
      error({
         statusCode: 404, message: 'Post not found' 
         })
    })
  },
  data () {
    return {
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
