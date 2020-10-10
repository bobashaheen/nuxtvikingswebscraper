<template>
  <div>
    <navbar></navbar>
    <b-container fluid class="mt-4">
      <b-row>
        <b-col cols="12" sm="12" md="4" lg="4" xl="4">
          <div class="mb-2">
            <img
              class="w-100"
              alt="Vikings Poster"
              title="Vikings Poster"
              src="https://m.media-amazon.com/images/M/MV5BNjIzZjljZmQtOGNiYi00YmY2LWE1MGYtN2VlMmEyZDBlMzRmXkEyXkFqcGdeQXVyMTkxNjUyNQ@@._V1_UY1200_CR84,0,630,1200_AL_.jpg"
            />
          </div>
        </b-col>
        <b-col cols="12" sm="12" md="8" lg="8" xl="8">
          <div class="video-container mb-3">
            <iframe
              width="853"
              height="480"
              src="https://www.youtube.com/embed/dKf-nmEzecA"
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
          <div class="plot_summary">
            <div class="summary_text ready">
              <div class="localized-plot">
                <div class="plot-text">
                  <div class="ipc-html-content ipc-html-content--base">
                    <div>
                      Vikings transports us to the brutal and mysterious world
                      of Ragnar Lothbrok, a Viking warrior and farmer who yearns
                      to explore - and raid - the distant shores across the
                      ocean.
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div>
              <h6 class="inline">Creator:</h6>
              <a href="#">Michael Hirst</a>
            </div>
            <div>
              <h6>Stars:</h6>
              <a href="#">Katheryn Winnick</a>,
              <a href="#">Alexander Ludwig</a>,
              <a href="#">Gustaf Skarsgård</a>
            </div>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  },
}
</script>

<style>
.video-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 */
  height: 0;
}
.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
