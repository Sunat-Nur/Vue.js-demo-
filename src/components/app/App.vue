<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
          :allMoviesCount="movies.length"
          :favoriteMoviesCount="movies.filter(c => c.favorite).length"
      />
      <div class="search-panel">
        <SearchPanel/>
        <Appfileter/>
      </div>
      <MovieList :movies="movies" @onLike="onLikeHandler"/>
      <!--      bola div dan ona div ga ma'lumot olyabdi-->
      <MovieAddForm @createMovie="createMovie"/>

    </div>
  </div>
</template>


<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import Appfileter from "@/components/app-filter/Appfileter.vue";
import MovieList from "@/components/movie-list/MovieList.vue";
import MovieAddForm from "@/components/movie-add-form/MovieAddForm.vue";

export default {
  components: {
    MovieAddForm,
    MovieList,
    Appfileter,
    AppInfo,
    SearchPanel,
  },
  data() {
    return {
      movies: [
        {
          name: "our school",
          viewers: 811,
          favorite: false,
          like: true,
          id: 1,
        },
        {
          name: "sweet home",
          viewers: 811,
          favorite: false,
          like: false,
          id: 2,
        },
        {
          name: "Busan train",
          viewers: 811,
          favorite: true,
          like: false,
          id: 3,
        },
      ],
    }
  },
  methods: {
    createMovie(item) { // create movie parameter qabul qiladi. ( argument, sifatida itemni berdik)
      this.movies.push(item); // item larni arrayga push qilyabdi
      console.log(item);
    },
    onLikeHandler(id) {
      this.movies.map(item => {
        if (item.id === id) {
          item.like = !item.like;
        }
        return item;
      })
    },
  },
}
</script>


<style>
.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}

</style>