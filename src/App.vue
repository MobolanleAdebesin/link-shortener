<template>
  <div class="grid grid-cols-6 grid-rows-2 pt-10">
    <div class="col-start-3 flex flex-col items-center row-start-1 mt-[25%]">
      <LinkForm
        @submit-link="(url) => this.shortenLink(url)"
        labelText="URL"
        placeholderText="Enter URL here"
        buttonText="Generate Link"
      />
      <LinkDisplay :shortLink="shortLink" />
    </div>
    <div class="flex items-center justify-center p-3 col-span-full row-start-1">
      <LinkBackgroundSVG />
    </div>
  </div>
</template>

<script>
import LinkForm from "./components/LinkForm.vue";
import LinkDisplay from "./components/LinkDisplay.vue";
import LinkBackgroundSVG from "./components/LinkBackgroundSVG.vue";
export default {
  name: "App",
  components: {
    LinkForm,
    LinkDisplay,
    LinkBackgroundSVG,
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
