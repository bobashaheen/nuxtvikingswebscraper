<template>
  <div>
    <navbar></navbar>
    <div>{{ err }}</div>
    <b-container class="mt-5">
      <b-row class="row_gallery">
        <b-col
          v-for="(photo, inx) in photos"
          :key="inx"
          cols="6"
          sm="6"
          md="4"
          lg="3"
          xl="2"
          class="mb-4"
          ><a href="#" :title="photo.title"
            ><img
              crossorigin="anonymous"
              height="100"
              width="100"
              :alt="photo.imgSrc"
              :src="photo.imgSrc" /></a
        ></b-col>
      </b-row>
    </b-container>
    <div>
      <div>
        <div class="text-center">
          <div v-if="isHave === true" class="spinner-border" role="status">
            <span class="sr-only">Loading...</span>
          </div>
          <p v-if="isHave === false">Photos is finish</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import cheerio from 'cheerio'

export default {
  data() {
    return {
      photos: [],
      err: null,
      page: 1,
      pageIsFinish: false,
      isHave: true,
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
    window.onscroll = () => {
      if (
        document.documentElement.scrollTop + window.innerHeight ===
        document.documentElement.offsetHeight
      ) {
        this.page++
        if (!this.pageIsFinish) {
          this.isHave = true
          this.getPhotos()
        }
      }
    }
  },
  beforeMount() {
    this.getPhotos()
  },
  methods: {
    async getPhotos() {
      const api = 'https://cors-anywhere.herokuapp.com/'
      const url =
        'https://www.imdb.com/title/tt2306299/mediaindex?page=' +
        this.page +
        '&ref_=ttmi_mi_sm'
      const html = await axios.get(api + url)

      const $ = await cheerio.load(html.data)
      if (Object.entries($('.media_index_thumb_list')).length !== 4) {
        $('.media_index_thumb_list')
          .children('a')
          .each((i, el) => {
            const title = $(el).attr('title')
            const imgSrc = $(el).find('img').attr('src')
            this.photos.push({ title, imgSrc })
          })
      } else {
        this.isHave = false
        this.pageIsFinish = true
      }
    },
  },
  head() {
    return {
      title: 'Vikings - gallery',
      meta: [{ name: 'description', content: 'gallery of Vikings series' }],
    }
  },
  fetchOnServer: false,
}
</script>

<style>
.row_gallery > div > a {
  position: relative;
  display: flex;
  justify-content: center;
}
</style>
