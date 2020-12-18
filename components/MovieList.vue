<template>
  <b-container>
    <b-row v-for="movie in movies" :key="movie.id" class="movie-row">
      <b-col lg="4">
        <img
          :src="'https://image.tmdb.org/t/p/original' + movie.poster_path"
          :alt="movie.title"
          class="img-thumbnail"
        />
      </b-col>
      <b-col lg="8">
        <h3>{{ movie.title }}{{ movie.name }}</h3>
        <strong>Дата выхода:</strong
        ><span> {{ movie.release_date }}{{ movie.first_air_date }}</span
        ><br />
        <strong>Оценка:</strong><span> {{ movie.vote_average }}</span
        ><br />
        <strong>Описание:</strong>
        <p>
          {{ movie.overview }}
        </p>
        <button class="btn btn-outline-info" @click="openMovie(movie)">
          Подробнее
        </button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'MovieList',
  props: ['movies', 'href'],
  methods: {
    openMovie(movie) {
      this.$router.push('/' + this.href + '/' + movie.id)
    },
  },
}
</script>

<style scoped>
.poster-img {
  width: 300px;
}

.movie-row {
  margin-top: 40px;
}
</style>
