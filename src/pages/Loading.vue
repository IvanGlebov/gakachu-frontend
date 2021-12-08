<template>
    <Layout class='wrapper'>
        <div>Wait untill robot is free again</div>
        <fade-loader :color="'#110100'"></fade-loader>
        <div class="imgWrapper">
          <div>Here will be an image of current painting</div>
          <img class="currImage" src="/pic.png" alt=""/>
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
            status: ''
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
        }
    },
    mounted() {
        this.startWaterfall()
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
