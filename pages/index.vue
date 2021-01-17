<template>
  <div class="container">
    <div class="row mt-4">
      <b-form-input
      autocomplete="off"
        id="input-1"
        v-model="form.query"
        type="text"
        placeholder="Search"
      ></b-form-input>
    </div>
    <div class="row mt-2">
      <b-table  bordered :items="search"> </b-table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {},
      categories: []
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        let res = await this.$axios.get(
          "https://api.publicapis.org/categories"
        );
        res.data.map(x => {
          this.categories.push({ catagory: x });
        });
      } catch (error) {}
    }
  },
  computed: {
    search: function() {
      if(this.form.query){
        return this.categories.filter(x =>{
          return this.form.query.toLowerCase().split(' ').every(v => x.catagory.toLowerCase().includes(v))
        })
      } else{
        return this.categories;
      }
    }
  }
};
</script>

<style>
/* .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
} */

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
