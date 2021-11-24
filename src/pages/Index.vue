<template>
  <Layout class="fullWrapper">
    <h1>Gakachu</h1>
    <a class="devLink" href="/dev">Dev settings</a>

    <div class="mainButtonWrapper">
      <input
        @keydown="validateInput"
        @keyup.enter="sendWord"
        v-model="word"
        class="mainInput"
        ref="email"
        placeholder="Enter a word"
      />
      <div @show="error">{{ error }}</div>
      <div>
        <button class="submitButton" @click="sendWord">Submit</button>
      </div>
    </div>
  </Layout>
</template>

<script>
import axios from "axios";

export default {
  metaInfo: {
    title: "Enter a word",
  },
  data: () => {
    return {
      word: "",
      error: "",
    };
  },
  methods: {
    focusInput() {
      this.$refs.email.focus();
    },
    validateInput() {
      if (this.word !== "") this.error = "";
    },
    sendWord() {
      if (this.word !== "") {
        axios({
          method: "POST",
          url: "http://localhost:5000/send_word",
          data: {
            word: this.word,
          },
        })
          .then((res) => {
            if (res.data.status === "OK")
              window.location.href = "/Loading";
            else {
              this.error = "Something has gone wrong on server. Try again.";
            }
          })
          .catch((e) => {
            this.error = "During request happened error";
          });
      } else {
        this.error = "This field should not be empty";
      }
    },
  },
  mounted() {
    this.focusInput();
  },
};
</script>

<style>
.submitButton {
  margin-top: 50px;
  cursor: pointer;
  font-size: 14pt;
  width: 150px;
  height: 50px;
  border: 0;
  border-radius: 20px;
  background: rgba(129, 177, 235, 0.49);
}

.fullWrapper {
  height: 90vh;
}

.devLink {
  display: block;
  position: fixed;
  right: 15px;
  bottom: 15px;
  text-decoration: none;
  color: #cccccc;
  cursor: default;
}

.mainButtonWrapper {
  height: 70vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.mainInput {
  font-size: 20pt;
  border: solid 1px black;
  padding: 15px;
  border-radius: 20px;
}
</style>
