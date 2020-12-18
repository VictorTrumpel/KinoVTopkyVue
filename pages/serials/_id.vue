<template>
  <b-container class="p-4">
    <BackBtn />
    <Scroller
      v-slot="{ activeItems, itemWidth }"
      :items="cast"
      :title="'Cast'"
      class="scroll-container"
    >
      <div
        v-for="actor in activeItems"
        :key="actor.cast_id"
        class="card"
        style="font-size: 0.9rem"
      >
        <img
          :src="'https://image.tmdb.org/t/p/original' + actor.profile_path"
          class="card-img-top"
          :alt="actor.name"
          style="width: 175px"
          :width="itemWidth"
        />
        <div class="card-body">
          <h6 class="card-title">{{ actor.original_name }}</h6>
          <p class="card-text">Character: {{ actor.character }}</p>
        </div>
      </div>
    </Scroller>
    <Scroller v-slot="{ activeItems, itemWidth }" :items="crew" :title="'Crew'">
      <div
        v-for="member in activeItems"
        :key="member.credit_id"
        class="card"
        style="font-size: 0.9rem"
      >
        <img
          :src="'https://image.tmdb.org/t/p/original' + member.profile_path"
          class="card-img-top"
          :alt="member.name"
          style="width: 175px"
          :width="itemWidth"
        />
        <div class="card-body">
          <h6 class="card-title">{{ member.name }}</h6>
          <p class="card-text">Job: {{ member.job }}</p>
        </div>
      </div>
    </Scroller>
  </b-container>
</template>

<script>
import BackBtn from '../../components/BackBtn'
import { API_KEY } from '../../static/StartConsts'
import Scroller from '../../components/Scroller'

export default {
  name: 'Id',
  components: { BackBtn, Scroller },
  validate({ params }) {
    return /^\d+$/.test(params.id)
  },
  async asyncData({ $axios, params }) {
    const response = await $axios.$get(
      'https://api.themoviedb.org/3/tv/' +
        params.id +
        '/credits?api_key=' +
        API_KEY
    )
    return {
      cast: response.cast,
      crew: response.crew,
    }
  },
  data() {
    return {
      cast: [],
      crew: [],
    }
  },
}
</script>

<style scoped>
.scroll-container {
  margin-top: 40px;
}
</style>
