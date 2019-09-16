<template>
  <header class="d-flex justify-content-between align-content-center">
    <div>
      <img src="./images/library_logo.png" alt="TGIF logo" class="cstm-logo mr-3" />
    </div>
    <div class="d-flex flex-wrap align-items-center justify-content-end">
      <div>
        <form class="form-inline input-group">
          <div class="input-group-prepend">
            <label for="search-field" class="input-group-text">Search:</label>
          </div>
          <input
            v-on:keyup="changeSearchInput"
            v-model="searchInput"
            id="search-field"
            type="text"
            class="form-control"
          />
        </form>
      </div>
    </div>
  </header>
</template>

<script>
import { bus } from "../main";
export default {
  name: "vHeader",
  components: {},
  data() {
    return {
      searchInput: ""
    };
  },

  methods: {
    changeSearchInput: function() {
      bus.$emit("searchInputModified", this.searchInput);
    }
  }
};
</script>

<style>
.cstm-logo {
  max-width: 50vw;
}
</style>