<template>
  <div>
    <span class="row">
      <span class="col"></span>
      <b-input-group size="sm" class="col-md-4">
        <b-form-input
          v-model="filter"
          type="search"
          id="filterInput"
          placeholder="Type to Search"
        ></b-form-input>
        <!-- <b-input-group-append>
          <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
        </b-input-group-append> -->
      </b-input-group>
  
    </span>
    <br>
    <b-table
      striped
      hover
      :filter="filter"
      :items="moviesList"
      :fields="fields"
      @row-clicked="openDetail($event)"
    ></b-table>
    <MovieDetail v-if="showDetails" :movieData="movieData"></MovieDetail>
  </div>
</template>

<script>
import MovieDetail from "./MovieDetail.vue";

export default {
  props: { moviesList: Array },
  components: {
    MovieDetail,
  },
  data() {
    return {
      // Note `isActive` is left out and will not appear in the rendered table
      fields: [
        {
          key: "title",
          label: "Title ",
        },
        {
          key: "vote_average",
          label: "Ratting",
          sortable: true,
        },
        {
          key: "original_language",
          label: "Language ",
        },
        {
          key: "release_date",
          label: "Relese Date ",
        },
      ],
      showDetails: false,
      movieData: {},
      filter: "",
    };
  },
  mounted: function () {},
  methods: {
    openDetail: function (item) {
      console.log(item);
      this.movieData = {...item};
      this.showDetails = true;
    },
  },
};
</script>