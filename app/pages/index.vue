<template>
  <div class="container mx-auto p-5">
    <div class="grid">
      <div
        class="card bg-green-500 dark:bg-zinc-700 p-5 text-center"
        v-if="load == null"
      >
        <span class="text-white"> The server is heating up 🔥 </span>
      </div>
      <HomeCam v-else />
    </div>
  </div>
</template>

<script>
import HomeCam from "../components/HomeCam.vue";
export default {
  name: "IndexPage",
  head() {
    return {
      title: "Home",
    };
  },
  data() {
    return {
      load: null,
    };
  },
  mounted() {
    this.$axios.$post(process.env.SOCKET_URL_PORT + "/loading").then((s) => {
      this.load = s;
    });
  },
  components: { HomeCam },
};
</script>
