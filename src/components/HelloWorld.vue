<template>
  <div class="hello">
    <ul v-for="item in peopleList" :key="item.id">
          <li>{{item.id}}</li>
          <li>{{item.title}}</li>
          <li>{{item.author}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "HelloWorld",
    data() {
      return {
        peopleList: ""
      };
    },
    mounted() {
      this.getAllPeople();
    },
    methods: {
      getAllPeople: function() {
        this.$http
          .get(BASE_URL + "/posts", {})
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
