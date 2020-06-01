<template>
  <div class="dailyRecommend">
    <div class="dailyRecommend-1 content">
      <aHeader />
    </div>
    <div class="dailyRecommend-2 content">
      <aContent :musics="musics" :out="out" :preMusic="preMusic" />
    </div>
    <div class="dailyRecommend-3 content">
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
      musics: [],
      preMusic: []
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
    out() {
      this.musics.splice(0, 1);
      this.musics.push(this.preMusic[0]);
      this.preMusic.splice(0, 1);
      this.axiosGet().then(res => {
        this.preMusic.push(res.data.song[0]);
      });
    }
  },
  computed: {},
  watch: {},
  created() {
    for (let i = 0; i < 5; i++) {
      this.axiosGet()
        .then(res => {
          this.musics.push(res.data.song[0]);
        })
        .catch(err => {
          console.log(err);
        });
    }
    for (let i = 0; i < 5; i++) {
      this.axiosGet().then(res => {
        this.preMusic.push(res.data.song[0]);
      });
    }
  }
};
</script>

<style lang="scss">
.dailyRecommend {
  background: #fafafa;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.content {
  width: 1000px;
}
</style>
