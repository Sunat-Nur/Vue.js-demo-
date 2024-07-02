<template>
  <input
      type="text"
      class="form-control search-input"
      placeholder="search movie"
      :value="term"
      @input="changeHandler"
  />
</template>


<script>
export default {
  props: {
    updateTermHandler: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      term: "",
    }
  },
  methods: {
    changeHandler(e) {
      this.term = e.target.value;
      this.updateTermHandler(this.term);
    }
  }
}
</script>


<style>
.search-input {
  margin-top: 2rem;
  margin-bottom: 1rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  border-radius: 5px;
}
</style>