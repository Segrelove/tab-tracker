<template>
  <v-layout>
    <v-flex xs6>
      <panel title="Song Metadata">
      <v-text-field
      label="Title"
      :rules="[rules.required]"
      v-model="song.title"/>

      <v-text-field
      label="Artiste"
      :rules="[rules.required]"
      v-model="song.artist"/>

      <v-text-field
      label="Genre"
      :rules="[rules.required]"
      v-model="song.genre"/>

      <v-text-field
      label="Album"
      :rules="[rules.required]"
      v-model="song.album"/>

      <v-text-field
      label="Album Image Url"
      :rules="[rules.required]"
      v-model="song.albumImageUrl"/>

      <v-text-field
      label="Youtube Id"
      :rules="[rules.required]"
      v-model="song.youtubeId"/>
      </panel>
    </v-flex>

    <v-flex xs8>
      <panel title="Song Structure" class="ml-4">
        <v-textarea
        label="Tab"
        :rules="[rules.required]"
        v-model="song.tab"/>

        <v-textarea
        multiline
        label="Lyrics"
        :rules="[rules.required]"
        v-model="song.lyrics"/>
      </panel>

      <div class="danger-alert" v-if="error">{{error}}</div>
      <v-btn @click="create" class="cyan" dark>Create Song</v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      error: null,
      rules: {
        required: value => !!value || 'Required.'
      }
    }
  },
  methods: {
    async create () {
      this.error = null
      const areAllFiledsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])
      if (!areAllFiledsFilledIn) {
        this.error = 'Please fill in all the required fields'
        return
      }

      try {
        await SongsService.post(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (err) {
        console.log(err)
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<style scoped>
</style>
