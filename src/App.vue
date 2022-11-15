<template>
  <el-container>

    <el-header>
      <div class="mt-4">
        <el-input v-model="input" placeholder="Please input" class="input-with-select">
          <template #prepend>
            <el-select v-model="select" placeholder="Select" style="width: 115px">
              <el-option label="网易云" value="1" />
              <el-option label="咪咕" value="2" />
            </el-select>
          </template>
          <template #append>
            <el-button icon="Search" @click="fetchData" />
          </template>
        </el-input>
      </div>
    </el-header>

    <el-main>
      <el-scrollbar height="400px">

        <el-row v-for="todo in todoData">
          <el-col :span="8">
            {{ todo.Name }}
          </el-col>
          <el-col :span="8">
            {{ todo.Singer }}
          </el-col>
          <el-col :span="8">
            <el-button @click="playMusic(todo)" icon="VideoPlay" plain />
          </el-col>
        </el-row>
      </el-scrollbar>
    </el-main>

    <el-footer>
      <audio controls="controls" :src="curMusicSrc" autoplay="autoplay">
      </audio>
    </el-footer>
  </el-container>

</template>

<script>
export default {
  data() {
    return {
      input: '周杰伦',
      select: '1',
      todoData: [{ AlbumName: null, AlbumPic: null, Alia: null, Audio: null, Flac: null, ID: null, Lyric: null, Name: null, Singer: null, Size: null, Time: null }],
      curMusicSrc: ''
    }
  },
  methods: {
    async fetchData() {
      this.todoData = null
      let url = 'http://www.youthsweet.com:3800/migu/api?keyword=' + this.input
      const res = await fetch(url)
      this.todoData = await res.json()
      this.curMusicSrc = this.todoData[0].Audio
    },
    playMusic(todo) {
      this.curMusicSrc = todo.Audio
    }
  },
  mounted() {
    this.fetchData()
  }
}
</script>

<style>

</style>
