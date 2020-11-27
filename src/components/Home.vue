<template>
  <div class="container">
    <div class="d-flex justify-content-around">
      <h2 class="mb-2">Upcoming Movies</h2>
      <button
        class="btn btn-outline-primary float-right "
        @click="showModal = true"
      >
        User profile
      </button>
    </div>
    <br />
    <ListView v-if="moviesList.length" :moviesList="moviesList"></ListView>

    <b-modal
      id="user-profile"
      title="User Profile"
      size="lg"
      v-model="showModal"
      hide-footer
    >
      <UserProfile
        @show-toaster="showToaster()"
        @hide-modal="showModal = false"
      ></UserProfile>
    </b-modal>
  </div>
</template>
<script>
import axios from "axios";
import ListView from "./ListView";
import UserProfile from "./UserProfile";
export default {
  components: {
    ListView,
    UserProfile,
  },
  data() {
    return {
      name: "movies list",
      moviesList: [],
      showModal: false,
    };
  },
  mounted: function () {
    let url =
      "https://api.themoviedb.org/3/movie/upcoming?api_key=83dc53ab158cb1f4d5bce4b39e7b892e&language=en-US&page=1";
    axios
      .get(url)
      .then((response) => {
        console.log(response.data);
        this.moviesList = response.data.results;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    showToaster() {
      this.$bvToast.toast(`User data saved`, {
        title: "Success",
        variant: "success",
        autoHideDelay: 2500,
      });
    },
  },
};
</script>