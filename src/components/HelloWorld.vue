<template>
  <div class="hello">
    <h1>{{people}}</h1>
    <ul v-for="item in peopleList" :key="item.id">
          <li>{{item.id}}</li>
          <li>{{item.name}}</li>
          <li><img :src="item.avatar" alt=""></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "HelloWorld",
    data() {
      return {
        people: "",
        peopleList: ""
      };
    },
    mounted() {
      this.getAllPeople();
    },
    methods: {
      getAllPeople: function() {
        this.$http
          .get("/api/people", {})
          .then(
            m => this.peopleList = m.data
          );
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2 {
    font-weight: normal;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: inline-block;
    margin: 0 10px;
  }
  
  a {
    color: #42b983;
  }
</style>
