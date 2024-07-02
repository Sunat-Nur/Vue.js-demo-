<template>
  <div class="movie-add-form">
    <h3>add new movie</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
          type="text" class="form-control new-movie-label"
          placeholder="which movie" :value="name"
          @:input="name = $event.target.value"
      />
      <input
          type="text" class="form-control new-movie-label"
          placeholder="how many time watched" :value="viewers"
          @:input="viewers = $event.target.value"
      />
      <button class="btn btn-outline-dark" type="submit" @click="addMovie">Add</button>
    </form>
  </div>
</template>
<script>


export default {
  data() {
    return {
      name: "",
      viewers: "",
    }
  },
  methods: {         // methodni yaratik
    addMovie() {           // methodni ichida addMoview yangi method yaratyabmiz
      if ( !this.name || !this.viewers  ) return   // bo'sh malumot ketmasligi ucun
      const newMovie = {    // addMovie methodni ichida yangi obyekt yaratyabmiz
        name: this.name,    // yuqordagi datalarni qiymatini this bilan olib olyabmiz
        viewers: this.viewers,
        favorite: false,
        like: false,
        id: Date.now(),
      }

      // $emit bola div dan ona div ga ma'lumot yuborish uchun ishlatiladi
      this.$emit("createMovie", newMovie) // argument sifadtida Movie ni beryabman
      this.name = ""
      this.viewers = ""
    },
  },
}
</script>


<style scoped>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>




