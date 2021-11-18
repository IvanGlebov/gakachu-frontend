<template>
  <Layout>
    <div class="wrapper">
      <div class="devHeader">
        <a class="iconLink" href="/">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="leftArrow h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z"
              clip-rule="evenodd"
            />
          </svg>
        </a>

        <h1>Dev | Brush position</h1>
      </div>

      <div class="buttons">
        <div class="buttonWithDescription">
          <button @click="moveUp">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 10l7-7m0 0l7 7m-7-7v18"
              />
            </svg>
            <div>Up</div>
          </button>
          <div>+0,01</div>
        </div>
        <div class="buttonWithDescription">
          <button @click="moveDown">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 14l-7 7m0 0l-7-7m7 7V3"
              />
            </svg>
            <div>Down</div>
          </button>
          <div>-0,01</div>
        </div>
        <div class="buttonWithDescription buttonMoveLeft">
          <button @click="testPosition">
            <div>Test</div>
          </button>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script>
import axios from "axios";
export default {
  setup() {},
  methods: {
    moveUp() {
      axios({
        method: "GET",
        url: "http://localhost:5000/brush_raise",
      })
        .then((res) => console.log(res))
        .catch((e) => console.log(e));
    },
    moveDown() {
      axios({
        method: "GET",
        url: "http://localhost:5000/brush_lower",
      })
        .then((res) => console.log(res))
        .catch((e) => console.log(e));
    },
    testPosition() {
      axios({
        method: "GET",
        url:"http://localhost:5000/test_brush_position"
      })
      .then(res => console.log(res))
      .catch(e => console.log(e))
    }
  },
  metaInfo: {
    title: "Dev",
  },
};
</script>

<style lang="css" scoped>
h1 {
  margin: 0;
}

.wrapper {
  height: calc(100vh - 150px);
  padding-top: 150px;
}

.buttons {
  display: flex;
  flex-direction: column;
  gap: 30px;
  align-items: center;
  justify-content: center;
  height: 50vh;
}

button {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 20px;
  padding-left: 20px;
  flex-direction: row;
  cursor: pointer;
  font-size: 14pt;
  width: 150px;
  height: 50px;
  border: 0;
  border-radius: 20px;
  background: rgba(129, 177, 235, 0.49);
}
button svg {
  width: 20px;
}

.buttonWithDescription {
  display: flex;
  align-items: center;
  gap: 30px;
}
.buttonMoveLeft {
  margin-left: -80px;
}

.buttonMoveLeft button {
  justify-content: center;
  margin: 0;
  padding: 0;
}

.devHeader {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 30px;
}

.iconLink {
  display: flex;
  justify-content: center;
  align-items: center;
}

.leftArrow {
  color: black;
  width: 30px;
}
</style>