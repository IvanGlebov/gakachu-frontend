<template>
  <div class="wrapper">
    <div class="header">
      Drawing finished
    </div>
    <div>
      <g-link to='/' class="submitButton">Go to main</g-link>
    </div>
    <div>Scan QR code to find out more</div>
    <g-image class="qrCode" src="/qr.png"/>
  </div>
</template>

<script>
export default {
  name: "drawingFinished.vue",
  methods: {
    goHome() {
      window.location.href = '/'
    }
  }
}
</script>

<style scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    gap: 50px;
  }
  .header {
    font-size: 30px;
  }
  .qrCode {
    width: 700px;
    max-height: 500px;
  }
  .submitButton {
    display: block;
    text-decoration: none;
    color: black;
    text-align: center;
    margin-top: 50px;
    cursor: pointer;
    font-size: 14pt;
    line-height: 48px;
    width: 150px;
    height: 50px;
    border: 0;
    border-radius: 20px;
    background: rgba(129, 177, 235, 0.49);
}
</style>