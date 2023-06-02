<template>
  <div class="flex flex-col justify-center items-center">
      <LinkForm
        @submit-link="(url) => this.shortenLink(url)"
        labelText="URL"
        placeholderText="Enter URL here"
        buttonText="Generate Link"
      />
      <LinkDisplay :shortLink="shortLink" />
  </div>
</template>

<script>
import LinkForm from "./components/LinkForm.vue";
import LinkDisplay from "./components/LinkDisplay.vue";

export default {
  name: "App",
  components: {
    LinkForm,
    LinkDisplay,

  },
  data() {
    return {
      shortLink: "",
    };
  },
  methods: {
    async shortenLink(url) {
      let token = process.env.VUE_APP_BITLY_TOKEN;
      let data = await fetch("https://api-ssl.bitly.com/v4/shorten", {
        method: "POST",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ long_url: `${url}`, domain: "bit.ly" }),
      });
      let result = await data.json();
      this.shortLink = result.link;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
