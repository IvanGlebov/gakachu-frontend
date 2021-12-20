<template>
    <Layout class='wrapper'>
        <div>Wait until robot is free again</div>
        <fade-loader :color="'#110100'"></fade-loader>
        <div class="imgWrapper">
          <div v-if="!imgStatus">Here will be an image of current painting</div>
          <img v-if="imgStatus" class="currImage" src="http://localhost:5000/picture" alt=""/>
        </div>
    </Layout>
</template>

<script>
import axios from 'axios'
import FadeLoader from 'vue-spinner/src/FadeLoader.vue'
export default {
    components: {
        FadeLoader
    },
    data: () => {
        return ({
            timerID: '',
            imgTimer: '',
            imgStatus: '',
        })
    },
    methods: {
        startWaterfall() {
            this.timerID =  setInterval(() => {
                axios({
                    method: 'GET',
                    url: 'http://localhost:5000/status'
                })
                .then((res) => {
                    if (res.data.status === 'available'){
                        clearInterval(this.timerID)
                        window.location.href='/drawing-finished'
                    }
                })
            }, 1000)
        },
        checkIfImageExists(url) {
          const img = new Image()
          img.src = url
          if (img.complete) {
            this.$data.imgStatus = true
            clearInterval(this.$data.imgTimer)
          } else {
            this.$data.imgStatus = false
          }
        }
    },
    mounted() {
      this.startWaterfall()
      setInterval(() => {
        this.checkIfImageExists('http://localhost:5000/picture')
      },500)
    },
    beforeUnmount() {
        clearInterval(this.timerID)
    }
}
</script>
<style scoped>
    .wrapper {
        height: 100vh;
        gap: 100px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .imgWrapper {
      display: flex;
      flex-direction: column;
      gap: 25px;
      justify-content: center;
      align-items: center;
    }
    img {
      border: none;
    }
    .currImage {
      width: 700px;
      max-height: 500px;
    }
</style>
