<template>
  <div class="flip-card-inner">
    <div class="flip-card-front">
      <img v-bind:src="book.cover" class="img-fluid" alt="book cover" />
    </div>
    <div class="flip-card-back d-flex flex-column justify-content-between overflow-auto p-4">
      <h2>{{book.title}}</h2>
      <p>{{book.description}}</p>
      <a v-bind:href="book.detail" v-bind:data-caption="book.title" data-fancybox="gallery">
        <button class="button-style bg-danger text-white rounded">more info</button>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "vSingleBook",
  components: {},
  props: {
    book: {
      type: Object
    }
  },
  data() {
    return {};
  }
};
</script>

<style>
.button-style {
  width: 70%;
}

.flip-card-inner {
  width: 100%;
  height: 100%;
  position: relative;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.flip-card-front {
  color: black;
}

.flip-card-back {
  background-color: rgb(37, 122, 29);
  color: white;
  transform: rotateY(180deg);
}
</style>