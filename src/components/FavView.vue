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
      <span class="fs-6">Séries em alta</span>
      <span class="fs-6"><i class="bi bi-aspect-ratio"></i></span>
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
  mounted() {
    // Carregar séries favoritas
    fetch(
      "http://localhost:8080/api/favoritos?accountId=20393076&sessionId=f281d9b1bee0ddab6c6a15a6363e1a02b1b669d7"
    )
      .then((response) => response.json())
      .then((data) => {
        console.log("Dados recebidos dos favoritos:", data);
        this.favorites = data.results;
      })
      .catch((error) => {
        console.error("Erro ao carregar favoritos:", error);
      });

    // Carregar séries em alta
    fetch(
      "http://localhost:8080/api/tendencias?accountId=20393076&sessionId=f281d9b1bee0ddab6c6a15a6363e1a02b1b669d7"
    )
      .then((response) => response.json())
      .then((data) => {
        console.log("Dados das tendências:", data);
        this.trendingShows = data; // Assume que o backend retorna a lista completa de tendências
      })
      .catch((error) => {
        console.error("Erro ao carregar as tendências:", error);
      });
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
