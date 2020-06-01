<template>
  <div class="dailyRecommend">
    <div class="dailyRecommend-1">
      <aHeader />
    </div>
    <div class="dailyRecommend-2">
      <aContent :musics="musics" :out="out" />
    </div>
    <div class="dailyRecommend-3">
      <aEndButton />
    </div>
  </div>
</template>

<script>
import axios from "axios";

import aHeader from "../components/a-header";
import aContent from "../components/a-content";
import aEndButton from "../components/a-endButton";
export default {
  data() {
    return {
      musics: []
    };
  },
  components: {
    aHeader,
    aContent,
    aEndButton
  },
  methods: {
    axiosGet() {
      return axios.get("http://10.7.10.2:3000");
    },
    up() {},
    out(index) {
      switch (index) {
        case 5:
          this.axiosGet().then(res => {
            this.musics.splice(0, 1);
            this.musics.push(res.data.song[0]);
          });
          break;
      }
    }
  },
  computed: {},
  watch: {},
  created() {
    for (let i = 0; i <= 5; i++) {
      this.axiosGet()
        .then(res => {
          this.musics.push(res.data.song[0]);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style lang="scss">
.dailyRecommend {
  min-width: 1000px;
}
</style>
