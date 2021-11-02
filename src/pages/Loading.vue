<template>
    <Layout class='wrapper'>
        <div>Wait untill robot is free again</div>
        <fade-loader :color="'#110100'"></fade-loader>
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
                        window.location.href='http://localhost/'
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
        height: 80vh;
        gap: 100px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
</style>