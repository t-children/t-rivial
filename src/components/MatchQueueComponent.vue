<template>
  <div class="main-container-queue">
    <!-- Row header -->
    <div class="row-header">
      <p>Matches in coming!</p>
    </div>
    <!-- Row matches from API -->
    <div class="loading-gif-container" v-if="loading">
      <img
        class="loading-gif"
        src="../assets/img/loading-gif.gif"
        alt="Loading"
      />
    </div>
    <div v-else>
      <div v-for="queue in queueMatches" :key="queue">
        <div class="row-match">
          <p>{{ queue.player1 }} - {{ queue.player2 }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MatchHistory",
  data() {
    return {
      queueMatches: [],
      loading: true
    };
  },
  async created() {
    await this.axios
      .get("/queue")
      .then((response) => {
        this.queueMatches = response.data.queue;
        this.loading = false;
      })
      .catch((error) => {
        console.error(error);
      });
  }
};
</script>

<style scoped lang="scss">
.main-container-queue {
  height: 215px;
  overflow-y: scroll;

  .loading-gif-container {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 100%;
    height: calc(215px - 60px);
    .loading-gif {
      width: 50px;
      height: 50px;
    }
  }
  .row-header p {
    font-size: 1.7rem;
    margin: 10px 0px;
    text-align: center;
  }
  .row-match {
    padding: 7px 0px;

    p {
      font-size: 1.2rem;
      text-align: center;
    }
  }
}
</style>
