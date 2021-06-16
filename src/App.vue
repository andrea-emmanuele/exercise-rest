<template>
  <Card :job="this.job"/>
  <div>{{ status }}</div>
</template>

<script>
import Card from "@/components/Card";

export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      endpoint: "https://c5ljdx2w0m.execute-api.eu-central-1.amazonaws.com/recruitment/",
      apiKey: "syaNs11gHB9pev48g5Zrt5p5O4cKX7yU1bUDj7F5", // Storing api key for making requests to the server
      job: {
        name: 'test',
        status: 'Initializing'
      },
      request: "",
      attempts: 0,
    };
  },
  mounted() {
    /*this.requests();*/
  },
  methods: {
    getStatus() {
      fetch(this.endpoint, {
        headers: { "x-api-key": this.apiKey },
      })
        .then((response) => response.json())
        .then((data) => {
          this.job.status = data.status;
          console.log(data);
        })
        .catch((error) => {
          console.error("An error occurred:", error);
          this.attempts++;
        });
    },
    checkStatus() {
      if (this.job.status === "Pending" || this.job.status === "") this.getStatus();
      else clearInterval(this.request);
    },
    checkAttempts(max) {
      if (this.attempts < max) this.checkStatus();
      else clearInterval(this.request);
    },
    requests() {
      this.request = setInterval(() => {
        this.checkAttempts(5);
      }, 5000);
    },
  },
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background: $main_bg;

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
  }
}
</style>
