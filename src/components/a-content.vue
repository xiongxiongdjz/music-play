<template>
  <div class="content">
    <div class="content-1">
      二维码
      {{ index }}
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
      <div class="content-2-button">
        <button @click="Aup" v-show="index">上一首</button>
        <button @click="Aout">下一首</button>
      </div>
    </div>
    <div class="content-3">
      <img class="content-3-img current" :src="musics[index].picture" />
      <img
        class="content-3-img advance"
        v-if="index <= 3"
        :src="musics[index + 1].picture"
      />
      <img class="content-3-img advance" v-else :src="preMusic[0].picture" />
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
  props: ["musics", "out", "preMusic"],
  components: {
    Aplayer
  },
  methods: {
    Aup() {
      this.index--;
    },
    Aout() {
      switch (this.index) {
        case 4:
          this.out();
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

.content-2 {
  width: 50%;
}

.content-2-button {
  display: flex;
  justify-content: flex-end;
}

.current {
  width: 15rem;
  height: 15rem;
  border-radius: 50%;
}

.advance {
  width: 5rem;
  height: 5rem;
  border-radius: 50%;
}
</style>
