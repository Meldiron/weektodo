<template>
  <transition name="fade">
    <div
      v-if="show"
      id="splashScreen"
      class="splash-screen d-flex justify-content-center align-items-center"
      ref="splashScreen"
    >
      <div v-if="sponsor !== ''" class="d-flex flex-column align-items-center">
        <div class="d-flex justify-content-center" style="height: 50px">
          <div class="d-flex sponsor-container align-items-center">
            <div class="my-2 mx-2">
              <div class="mx-1 d-inline d-inline" style="text-decoration: unset !important">{{sponsor}}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "splashScreen",
  data() {
    return {
      show: true,
      sponsor: "",
      darkTheme: this.$store.getters.config.darkTheme,
    };
  },
  mounted() {
    const axios = require("axios").default;
    axios
      .get("https://cloud.appwrite.io/v1/databases/main/collections/main/documents/main", {
        headers: {
          'x-appwrite-project': '6601ae689f83edbc5d2b'
        }
      })
      .then((response) => this.renderSponsor(response))
      .catch((error) => console.log(error.message));
  },
  methods: {
    hideSplash: function () {
      this.show = false;
    },
    renderSponsor: function (response) {
      this.sponsor = response.data.message ?? "";
    },
  },
};
</script>

<style scoped>
.sponsor-container {
  height: fit-content;
  width: fit-content;
  padding: 4px 10px 4px 10px;
  font-size: 0.85rem;
  box-sizing: border-box;
  border-radius: 25px;
  -webkit-box-align: start;
  -ms-flex-align: start;
  -webkit-align-items: flex-start;
  -moz-align-items: flex-start;
  align-items: flex-start;
  position: relative;
  background-color: #fefefe;
  box-shadow: 0 2px 20px 0 rgb(0 0 0 / 7%);
  /*border: 1px solid #dbdbdb;*/
  text-decoration: unset;
  color: unset;
  transition: transform 0.4s;
}

.dark-theme .sponsor-container {
  background-color: #102430;
}

.sponsor-container:hover {
  transform: scale(1.04);
}

.sponsor-img {
  width: 32px;
  border-radius: 25px;
}

/*.sponsor-text{*/
/*  text-decoration: unset;*/
/*}*/

.splash-screen {
  width: 100%;
  height: 100%;
  z-index: 1060;
  position: absolute;
  background-color: #fcfcfc;
}

.dark-theme .splash-screen {
  background-color: #13171d;
}

.logo {
  margin-right: 15px;
  width: 25rem;
}

.splash-screen h1 {
  color: #3f0e81;
}

.dark-theme .splash-screen h1 {
  color: #5329a3;
}

.splash-screen h1 {
  letter-spacing: 3px;
  font-size: 3rem;
  margin-bottom: 10px;
}

.splash-screen span {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.4rem;
  color: #79606b;
  margin-bottom: 20px;
}

.sponsor {
  margin-top: 10px;
  font-size: 0.8rem;
  color: #bababa;
}

.dark-theme .splash-screen span {
  color: #c9d1d9;
}

.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
