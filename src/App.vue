<template>
  <div id="app">
    <CarouselContainer :rows="shuffledSubmissions" />
  </div>
</template>

<script>
import CarouselContainer from "./components/CarouselContainer.vue";
const sheetUrl =
  "https://spreadsheets.google.com/feeds/list/19vLtOLv1MnTfrd1nLvpDk7SrQyIg5EZ_VTAzDOuiHyE/1/public/values?alt=json";

export default {
  name: "app",
  components: {
    CarouselContainer
  },
  created: function() {
    this.fetchData();
  },
  data: function() {
    return {
      submissions: []
    };
  },
  computed: {
    shuffledSubmissions: function() {
      return this.submissions.concat().sort(() => Math.random() - 0.5);
    }
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
            picture:
              row.gsx$picture.$t !== ""
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
