<template>
  <Carousel :autoplay="true" :autoplayTimeout="5000" :perPage="1">
    <Slide :key="index" v-for="(row, index) in rows" class="slide">
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
  align-items: center;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 100%;
}

img {
  max-height: 400px;
  width: auto;
  max-width: 100%;
}

p {
  max-width: 80vh;
  margin: 0 auto;
  padding-top: 15px;
}
</style>
