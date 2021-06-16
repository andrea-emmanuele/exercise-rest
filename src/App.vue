<template>
  <div>{{ status }}</div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      endpoint: "https://c5ljdx2w0m.execute-api.eu-central-1.amazonaws.com/recruitment/",
      apiKey: "syaNs11gHB9pev48g5Zrt5p5O4cKX7yU1bUDj7F5", // Storing api key for making requests to the server
      status: "",
      request: "",
    };
  },
  mounted() {
    this.getStatus();
  },
  methods: {
    getStatus() {
      fetch(this.endpoint, {
        headers: { "x-api-key": this.apiKey },
      })
        .then((response) => response.json())
        .then((data) => {
          this.status = data.status;
        })
        .catch((error) => {
          console.error("An error occurred:", error);
        });
    },
    requests() {
      this.request = setInterval(() => {
        this.getStatus();
      }, 5000);
    }
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
