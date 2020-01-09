<template>
  <Carousel :autoplay="true" :autoplayTimeout="5000" :perPage="1" class="carousel">
    <Slide
      :key="index"
      v-for="(row, index) in rows"
      class="slide"
      :class="[!row.picture ? 'only-message' : '' ]"
    >
      <div>
        <img v-if="row.picture" :src="row.picture" />
        <div class="caption">
          <p v-if="row.message">{{ row.message }}</p>
          <p v-if="row.name">From: {{ row.name }}</p>
        </div>
      </div>
    </Slide>
  </Carousel>
</template>

<script>
import { Carousel, Slide } from "vue-carousel";

export default {
  name: "CarouselContainer",
  components: {
    Carousel,
    Slide
  },
  props: {
    rows: Array
  }
};
</script>

<style>
.slide {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 100%;
  height: 100vh;
}

.only-message {
  align-items: center;
}
.only-message p {
  padding-top: 0;
}

.carousel {
  height: 100vh;
}
img {
  max-height: 70vh;
  width: auto;
  max-width: 100%;
  padding-top: 20px;
}

p {
  max-width: 90vw;
  margin: 0 auto;
  padding-top: 15px;
}
</style>
