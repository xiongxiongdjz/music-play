<template>
  <div class="content">
    <div class="content-1">
      二维码
    </div>
    <div class="content-2">
      <p v-text="musics[index].title"></p>
      <p v-text="musics[index].singers[0].name"></p>
      <aplayer
        class="aplayer"
        :music="{
          title: musics[index].title,
          artist: musics[index].singers[0].name,
          src: musics[index].url,
          pic: musics[index].picture
        }"
      />
      <div>
        <button @click="Aup" v-show="index">上一首</button>
        <button @click="Aout">下一首</button>
      </div>
    </div>
    <div class="content-3">
      <img class="content-3-img" :src="musics[index].picture" />
    </div>
  </div>
</template>

<script>
import Aplayer from "vue-aplayer";
export default {
  data() {
    return {
      index: 0
    };
  },
  props: ["musics", "out"],
  components: {
    Aplayer
  },
  methods: {
    Aup() {
      this.index--;
    },
    Aout() {
      switch (this.index) {
        case 5:
          this.out(this.index);
          break;

        default:
          this.index++;
          break;
      }
    }
  }
};
</script>

<style lang="scss">
.content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.content-3-img {
  width: 15rem;
  height: 15rem;
  border-radius: 50%;
}
</style>
