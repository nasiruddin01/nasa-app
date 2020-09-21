<template>
  <div class="search">
    <h2>Nasa Api Project</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Type in your search" v-model="query" />
      <button class="btn">Submit</button>
    </form>
    <div class="container" v-if="results">
      <div class="sub-container" v-for="(result, index) in results" :key="index">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>
    <p>Copyright &copy; Nasiruddin 2020.</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "search",
  data() {
    return {
      msg: "Search",
      query: "",
      results: ""
    };
  },
  methods: {
    getResult(query) {
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" + query + "&media_type=image"
        )
        .then(response => {
          console.log(response.data.collection.items);
          this.results = response.data.collection.items;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,600;0,700;0,900;1,100;1,200;1,400;1,500;1,600;1,800&display=swap");
.search {
  max-width: 1280px;
  margin: auto;
  text-align: center;
  font-family: "Montserrat", sans-serif;
  background: rgba(192, 236, 224, 1);
  h2 {
    font-size: 2rem;
  }
  form {
    input {
      margin-right: 0.5rem;
      padding: 6px 4px;
    }
    .btn {
      box-shadow: 0px 1px 0px 0px #fff6af;
      background: linear-gradient(to bottom, #ffec64 5%, #ffab23 100%);
      background-color: #ffec64;
      border-radius: 4px;
      border: 1px solid #ffaa22;
      display: inline-block;
      cursor: pointer;
      color: #333333;
      font-family: Arial;
      font-size: 15px;
      font-weight: bold;
      padding: 6px 24px;
      text-decoration: none;
      text-shadow: 0px 1px 0px #ffee66;
    }
    .btn:hover {
      background: linear-gradient(to bottom, #ffab23 5%, #ffec64 100%);
      background-color: #ffab23;
    }
    .btn:active {
      position: relative;
      top: 1px;
    }
    margin-bottom: 2rem;
  }
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 15px;
    .sub-container {
      // display: grid;
      // grid-template-columns: 1fr 1fr 1fr 1fr 1fr;

      img {
        width: 18rem;
        height: 18rem;
        margin-bottom: 18px;
        border: 2px solid #00aeff;
        border-radius: 4px;
      }
    }
  }
}
</style>
