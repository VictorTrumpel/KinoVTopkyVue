<template>
  <div class="d-flex flex-column justify-content-center">
    <button class="btn btn-dark" type="submit" @click="getFilms">
      Отфильтровать по году выпуска<input v-model="releaseYear" type="text" />
    </button>
    <MovieList :movies="movies" :href="'movies'" />
  </div>
</template>

<script>
import MovieList from '../../components/MovieList'
import {
  API_KEY,
  SORT_BY,
  RELEASE_YEAR,
  VOTE_COUNT_GTE,
  PAGE,
} from '../../static/StartConsts'

export default {
  components: { MovieList },
  async asyncData({ $axios }) {
    const response = await $axios.$get(
      'https://api.themoviedb.org/3/discover/movie?api_key=' +
        API_KEY +
        '&language=en-US&sort_by=' +
        SORT_BY +
        '&page=' +
        PAGE +
        '&primary_release_year=' +
        RELEASE_YEAR +
        '&vote_count.gte=' +
        VOTE_COUNT_GTE
    )
    return { movies: response.results }
  },
  data: () => ({
    movies: [],
    apiKey: API_KEY,
    voteCountGte: VOTE_COUNT_GTE,
    page: PAGE,
    sortBy: SORT_BY,
    releaseYear: RELEASE_YEAR,
  }),
  methods: {
    async getFilms() {
      const response = await this.$axios.$get(
        'https://api.themoviedb.org/3/discover/movie?api_key=' +
          this.apiKey +
          '&language=en-US&sort_by=' +
          this.sortBy +
          '&page=' +
          this.page +
          '&primary_release_year=' +
          this.releaseYear +
          '&vote_count.gte=' +
          this.voteCountGte
      )
      this.movies = response.results
    },
  },
}
</script>

<style scoped></style>
