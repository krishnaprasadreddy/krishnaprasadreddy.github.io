<template>
  <div>
    <b-sidebar
      id="sidebar-rightt"
      :title="movieData.title"
      right
      shadow
      backdrop
      no-header
      v-model="visible"
      width="750px"
    >
      <template #footer>
        <div class="d-flex justify-content-end">
          <b-button
            size="sm"
            variant="outline-secondary"
            @click="visible = false"
            >Close</b-button
          >
        </div>
      </template>

      <div class="p-3 py-2">
        <h3>{{ movieData.title }}</h3>

        <br />
        <p>
          {{ movieData.overview }}
        </p>
        <b-img :src="getImageURL()" fluid thumbnail></b-img>
        <br />
        <br />
        <strong>Ratting:</strong>{{ movieData.vote_average }}
      </div>
    </b-sidebar>
  </div>
</template>
<script>
export default {
  props: { movieData: Object },

  data() {
    return {
      visible: true,
    };
  },
  mounted: function () {
    // alert("show slideout");
  },
  methods: {
    getImageURL: function () {
      let url = `http://image.tmdb.org/t/p/w300/${this.movieData.poster_path}`;
      console.log(url);
      return url;
    },
  },
  watch: {
    movieData: function () {
      //alert("data changed");
      this.visible = true;
    },
  },
};
</script>

