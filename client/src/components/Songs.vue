<template>
  <v-layout row wrap>
      <v-flex xs6 offset-xs3 class="mt-2">
        <panel title="Songs">
            <v-btn class="cyan accent-4"  slot="action" @click="navigateTo({name: 'songs-create'})" dark small absolute right fab>
              <v-icon>add</v-icon>
            </v-btn>

          <div v-for="song in songs" class="song"
            :key="song.id">

            <v-layout>
              <v-flex xs6>
                <div class="song-title">
                  {{song.title}}
                </div>
                <div class="song-artist">
                  {{song.artist}}
                </div>
                <div class="song-genre">
                  {{song.genre}}
                </div>
                <v-btn @click="navigateTo({
                  name: 'song',
                  params: {
                    songId: song.id
                    }
                    })"
                    class="cyan" dark>
                  View
                </v-btn>

              </v-flex>

              <v-flex xs6>
                <img class="album-image" :src="song.albumImageUrl"/>
              </v-flex>
            </v-layout>
          </div>
        </panel>
      </v-flex>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/Panel'
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  },
  components: {
    Panel
  },
  data () {
    return {
      songs: null
    }
  },
  async mounted () {
    // do a request to the backend for all the songs
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 30px;
}
.song-artist {
  font-size: 24px;
}
.song-genre {
  font-size: 18px;
}

.album-image {
  width: 70%;
  margin: 0 auto;
}
</style>
