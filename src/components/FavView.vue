<template>
  <div class="container">
    <div class="py-2 d-flex justify-content-between">
      <span class="fs-6">Suas séries favoritas</span>
      <span class="fs-6"><i class="bi bi-aspect-ratio"></i></span>
    </div>
    <div class="scroll-container">
      <img
        v-for="(serie, index) in favorites"
        :key="index"
        class="imgPoster"
        :src="imageBaseUrl + serie.poster_path"
        :alt="serie.name"
      />
    </div>

    <div class="py-2 d-flex justify-content-between">
      <span class="fs-6">Séries em alta hoje</span>
      <router-link to="/trendingSeries"><span class="fs-6"><i class="bi bi-aspect-ratio"></i></span></router-link>
    </div>
    <div class="scroll-container">
      <img
        v-for="serie in trendingShows.slice(0, 10)"
        :key="serie.id"
        class="imgPoster"
        :src="imageBaseUrl + serie.poster_path"
        :alt="serie.name"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      favorites: [],
      trendingShows: [],
      imageBaseUrl: "https://image.tmdb.org/t/p/w500",
    };
  },
  methods: {
    async loadData() {
      try {
        await Promise.all([this.loadFavorites(), this.loadTrending()]);
      } catch (error) {
        console.error("Erro ao carregar dados:", error);
      }
    },
    async loadFavorites() {
      const res = await fetch(
        "http://localhost:8080/api/favoritos?accountId=20393076&sessionId=f281d9b1bee0ddab6c6a15a6363e1a02b1b669d7"
      );
      const data = await res.json();
      // console.log("Dados recebidos dos favoritos:", data);
      this.favorites = data;
    },
    async loadTrending() {
      const res = await fetch(
        "http://localhost:8080/api/tendencias?accountId=20393076&sessionId=f281d9b1bee0ddab6c6a15a6363e1a02b1b669d7"
      );
      const data = await res.json();
      // console.log("Dados das tendências:", data);
      this.trendingShows = data;
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style>
.scroll-container {
  display: flex;
  overflow-x: auto;
  padding: 0 0 10px 0;
  gap: 10px;
  scrollbar-width: thin;
}
.imgPoster {
  width: 100px;
  height: auto;
  flex-shrink: 0;
  border-radius: 8px;
}
</style>
