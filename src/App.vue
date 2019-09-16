<template>
  <div id="app" class="px-4">
    <vHeader />
    <vLibrary />
  </div>
</template>

<script>
import vHeader from "./components/header.vue";
import vLibrary from "./components/library.vue";
import { bus } from "./main";

export default {
  name: "app",
  components: {
    vHeader,
    vLibrary
  },
  data() {
    return {
      bookList: [],
      searchInput: ""
    };
  }
};
</script>

<style>
#app {
  margin-top: 30px;
}
h2 {
  font-size: calc(10px + 1.5vw);
}
p,
.input-group-text,
.form-control {
  font-size: calc(6px + 1vw);
  line-height: calc(6px + 1.1vw);
}
button {
  font-size: calc(5px + 0.8vw);
}
</style>
