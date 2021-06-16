<template>
  <Card :job="this.job"/>
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
      endpoint: "https://c5ljdx2w0m.execute-api.eu-central-1.amazonaws.com/recruitment/", // Api endpoint from where retrieve resources
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
    this.requests(); // Start to make requests when app is mounted
  },
  methods: {
    requests() {
      this.request = setInterval(() => { // Set an interval to run checkAttempts() every 5 seconds and to not overload the server
        this.checkAttempts(5); // Passing 5 as the maximum number of request attempts
      }, 5000);
    },
    getStatus() {
      fetch(this.endpoint, { // fetching endpoint with get method
        headers: { "x-api-key": this.apiKey }, // passing our stored api key in the request headers
      })
        .then((response) => response.json()) // extracting the request response and parsing it from text to javascript object
        .then((data) => {
          this.job.status = data.status; // the status value is assigned to job object defined in data()
        })
        .catch((error) => { // if request has failed
          console.error("An error occurred:", error); // Print out an error
          this.attempts++; // and increase the attempts value 'cause we can only do a restricted number of retrieves when request fails
        });
    },
    checkStatus() {
      if (this.job.status !== "Success") this.getStatus(); // Checking if the returned response is "Success" which means the job is completed
      else clearInterval(this.request); // else stop making requests
    },
    checkAttempts(max) {
      if (this.attempts < max) this.checkStatus(); // Checking if we still have attempts for making request and if yes then checking the current status
      else clearInterval(this.request); // else delete  function and stop making requests
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
