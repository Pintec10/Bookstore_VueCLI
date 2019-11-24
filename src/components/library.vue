<template>
  <div>
    <div v-if="bookList.length === 0" class="load-container">
      <div class="dash uno"></div>
      <div class="dash dos"></div>
      <div class="dash tres"></div>
      <div class="dash cuatro"></div>
    </div>
    <div id="bookcase" class="d-flex flex-wrap align-items-center justify-content-center mt-4">
      <div v-for="(book, index) in filterBooks" v-bind:key="index" class="flip-card">
        <vSingleBook v-bind:book="book" />
      </div>
    </div>
  </div>
</template>

<script>
import vSingleBook from "./singlebook.vue";
import { bus } from "../main";
export default {
  name: "vLibrary",
  components: {
    vSingleBook
  },

  data() {
    return {
      bookList: [],
      searchInput: ""
    };
  },

  props: {},

  methods: {
    fetchData() {
      return fetch("https://api.myjson.com/bins/zyv02", { method: "GET" })
        .then(function(resp) {
          return resp.json();
        })
        .then(json => {
          this.bookList = json.books;
          setTimeout(() => {
            //timeout ensures correct displaying if first page load is slow
            //first, shorter timer allows a more seamless transition on slightly slow loading
            this.assignHeight();
          }, 500);
          setTimeout(() => {
            //second, longer timer works for really slow loading
            this.assignHeight();
          }, 2000);
          window.addEventListener("resize", () => {
            setTimeout(() => {
              //timeout ensures correct displaying
              this.assignHeight();
            }, 250);
          });
          //-----
          bus.$on("searchInputModified", updatedSearchInput => {
            this.searchInput = updatedSearchInput;
            setTimeout(() => {
              //timeout ensures correct displaying
              this.assignHeight();
            }, 250);
          });
        });
    },
    assignHeight() {
      console.log("assignHeight has been called");
      let covers = document.querySelectorAll(".img-fluid");
      let flipInners = document.querySelectorAll(".flip-card-inner");
      for (let elem = 0; elem < covers.length; elem++) {
        flipInners[elem].style.height = covers[elem].height + "px";
      }
    }
  },

  computed: {
    filterBooks() {
      return this.bookList.filter(
        x =>
          x.title.toLowerCase().includes(this.searchInput) ||
          x.description.toLowerCase().includes(this.searchInput)
      );
    }
  },

  created() {
    this.fetchData();
  }
};
</script>

<style>
.flip-card {
  background-color: transparent;
  width: 27%;
  perspective: 1000px;
}

/* --- LOADER --- */

.load-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
}

.dash {
  margin: 0 15px;
  width: 35px;
  height: 15px;
  border-radius: 8px;
  background: rgb(37, 122, 29);
  box-shadow: 0 0 10px 0 #fecdff;
}

.uno {
  margin-right: -18px;
  transform-origin: center left;
  animation: spin 3s linear infinite;
}

.dos {
  transform-origin: center right;
  animation: spin2 3s linear infinite;
  animation-delay: 0.2s;
}

.tres {
  transform-origin: center right;
  animation: spin3 3s linear infinite;
  animation-delay: 0.3s;
}

.cuatro {
  transform-origin: center right;
  animation: spin4 3s linear infinite;
  animation-delay: 0.4s;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(360deg);
  }
  30% {
    transform: rotate(370deg);
  }
  35% {
    transform: rotate(360deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes spin2 {
  0% {
    transform: rotate(0deg);
  }
  20% {
    transform: rotate(0deg);
  }
  30% {
    transform: rotate(-180deg);
  }
  35% {
    transform: rotate(-190deg);
  }
  40% {
    transform: rotate(-180deg);
  }
  78% {
    transform: rotate(-180deg);
  }
  95% {
    transform: rotate(-360deg);
  }
  98% {
    transform: rotate(-370deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}

@keyframes spin3 {
  0% {
    transform: rotate(0deg);
  }
  27% {
    transform: rotate(0deg);
  }
  40% {
    transform: rotate(180deg);
  }
  45% {
    transform: rotate(190deg);
  }
  50% {
    transform: rotate(180deg);
  }
  62% {
    transform: rotate(180deg);
  }
  75% {
    transform: rotate(360deg);
  }
  80% {
    transform: rotate(370deg);
  }
  85% {
    transform: rotate(360deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes spin4 {
  0% {
    transform: rotate(0deg);
  }
  38% {
    transform: rotate(0deg);
  }
  60% {
    transform: rotate(-360deg);
  }
  65% {
    transform: rotate(-370deg);
  }
  75% {
    transform: rotate(-360deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}
</style>