<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
          :allMoviesCount="movies.length"
          :favoriteMoviesCount="movies.filter(c => c.favorite).length"
      />
      <div class="search-panel">
        <SearchPanel
            :updateTermHandler="updateTermHandler"
        />
        <Appfileter
            :updateFilterHandler="updateFilterHandler"
            :filterName="filter"
        />
      </div>
      <MovieList
          :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
          @onToggle="onToggleHandler"
          @onRemove="onRemoveHandler"
      />
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
          viewers: 711,
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
          viewers: 911,
          favorite: true,
          like: false,
          id: 3,
        },
      ],
      term: "",
      filter: "all",
    }
  },
  methods: {
    createMovie(item) { // create movie parameter qabul qiladi. ( argument, sifatida itemni berdik)
      this.movies.push(item); // item larni arrayga push qilyabdi
    },
    onToggleHandler({id, prop}) {
      this.movies = this.movies.map(item => {
        if (item.id === id) {
          return {...item, [prop]: !item [prop]}
        }
        return item;
      })
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(movie => movie.id !== id)
    },

    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter(movie => movie.like)
        case "mostViewers":
          return arr.filter(movie => movie.viewers > 500)
        default:
          return arr
      }
    },
    updateTermHandler(term) {
      this.term = term;
    },
    updateFilterHandler(filter) {
      this.filter = filter;
    }
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