<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
const sheetUrl =
  "https://spreadsheets.google.com/feeds/list/19vLtOLv1MnTfrd1nLvpDk7SrQyIg5EZ_VTAzDOuiHyE/1/public/values?alt=json";

export default {
  name: "app",
  components: {
    HelloWorld
  },
  created: function() {
    this.fetchData();
  },
  data: function() {
    return {
      submissions: []
    };
  },
  methods: {
    fetchData: function() {
      var xhr = new XMLHttpRequest();
      xhr.open("GET", sheetUrl);
      xhr.onload = () => {
        const json = JSON.parse(xhr.responseText);
        const rows = json.feed.entry;
        rows.forEach(row => {
          this.submissions.push({
            name: row.gsx$name ? row.gsx$name.$t : null,
            picture: row.gsx$picture
              ? `https://drive.google.com/uc?export=view&id=${row.gsx$picture.$t
                  .split("id=")
                  .pop()}`
              : null,
            message: row.gsx$message ? row.gsx$message.$t : null
          });
        });
      };
      xhr.send();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
