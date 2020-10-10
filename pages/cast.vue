<template>
  <div>
    <navbar></navbar>
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">photo</th>
          <th scope="col">actor</th>
          <th scope="col">character</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(actor, indx) in actors" :key="indx">
          <td>
            <a href="#"
              ><img
                height="44"
                width="32"
                :alt="actor.title"
                :title="actor.title"
                :src="actor.srcImg"
            /></a>
          </td>
          <td>
            <a href="#"> {{ actor.title }} </a>
          </td>
          <td>
            <a href="#"> {{ actor.character }} </a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
import cheerio from 'cheerio'

export default {
  data() {
    return {
      actors: [],
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  },
  beforeMount() {
    this.getActors()
  },
  methods: {
    async getActors() {
      const api = 'https://cors-anywhere.herokuapp.com/'
      const url =
        'https://www.imdb.com/title/tt2306299/fullcredits?ref_=tt_ql_dt_1'
      const html = await axios.get(api + url)

      const $ = await cheerio.load(html.data)

      $('.cast_list > tbody  > tr').each((i, el) => {
        if (i % 2 !== 0) {
          const title = $(el).children('td').find('img').attr('title')
          const srcImg = $(el).children('td').find('img').attr('loadlate')
          const character = $(el).children('.character').text()
          const date = $(el)
            .children('.character')
            .find('a:nth-child(2)')
            .text()
          this.actors.push({ title, srcImg, character, date })
        }
      })
    },
  },
  head() {
    return {
      title: 'Vikings - cast',
      meta: [{ name: 'description', content: 'cast of Vikings series' }],
    }
  },
  fetchOnServer: false,
}
</script>

<style></style>
