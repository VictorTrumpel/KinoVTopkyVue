<template>
  <div>
    <div class="btn-group">
      <button class="btn btn-success" @click="handlerResizeScroll()">
        <strong>{{ title }}</strong>
      </button>
      <button
        class="btn btn-secondary"
        :disabled="lIdx === 0"
        @click="scrollLeft"
      >
        &#10094;
      </button>
      <button
        :disabled="
          rIdx === items.length - Math.floor(scrollWidth / itemWidth) ||
          items.length === 0
        "
        class="btn btn-secondary"
        @click="scrollRight"
      >
        &#10095;
      </button>
    </div>
    <div class="carusel-content d-flex flex-row" style="height: 370px">
      <slot :activeItems="activeItems" :itemWidth="itemWidth"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Scroller',
  props: {
    items: {
      type: Array,
    },
    title: {
      type: String,
    },
  },
  data() {
    return {
      lIdx: 0,
      rIdx: 0,
      itemWidth: 175,
      scrollWidth: 0,
    }
  },
  computed: {
    activeItems() {
      return this.items.slice(
        this.lIdx,
        Math.floor(this.scrollWidth / this.itemWidth + this.rIdx)
      )
    },
  },
  mounted() {
    this.scrollWidth = document.querySelector('.scroll-container').clientWidth
  },
  beforeMount() {
    window.addEventListener('resize', this.handlerResizeScroll)
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handlerResizeScroll)
  },
  methods: {
    scrollRight() {
      if (this.rIdx !== this.items.length) {
        this.lIdx++
        this.rIdx++
      }
    },
    scrollLeft() {
      if (this.lIdx !== 0) {
        this.lIdx--
        this.rIdx--
      }
    },
    handlerResizeScroll() {
      this.scrollWidth = document.querySelector('.carusel-content').clientWidth
    },
  },
}
</script>

<style scoped>
.carusel-content {
  position: relative;
  margin-top: 20px;
  margin-bottom: 20px;
}

.carusel-btn {
  outline: none;
  position: absolute;
  width: 50px;
  height: 100%;
  border: none;
  background: lightgray;
}

.next-btn {
  right: 0;
}

.prev-btn {
  left: -50px;
}
</style>
