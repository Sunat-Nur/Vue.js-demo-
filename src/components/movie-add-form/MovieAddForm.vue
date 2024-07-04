<template>
  <div class="movie-add-form">
    <h3>add new movie</h3>
    <form class="add-form d-flex" @submit.prevent>
      <Input
          class="new-movie-label"
          placeholder="which movie?"
          v-model="name"
      />
      <Input
          class="new-movie-label"
          placeholder="how many time watched?"
          type="number"
          v-model="viewers"
      />

      <PrimaryButton class="btn-outline-dark" type="submit" @click="addMovie">Add</PrimaryButton>
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
      if (!this.name || !this.viewers) return   // bo'sh malumot ketmasligi ucun
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




