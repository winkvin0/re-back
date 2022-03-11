<template>
  <div class="profile" :class="night ? 'night':'day'">
    <div class="img-box">
      <div class="img"></div>
    </div>
    <div class="text-box">
      <p>name</p>
      <h2>{{ profile.resJobCategoryCn1 }}</h2>
      <p>money</p>
      <h2>{{ profile.resMoney }} k</h2>
      <p>intro</p>
      <h4>{{ profile.resSelfIntro }}</h4>
    </div>
    <div class="bottom-box" @mouseleave="status.searchShow=false">
      <div class="instruct-area" @mouseenter="status.searchShow = true">
        <div class="instruct"></div>
      </div>
      <transition name="slide">
        <div v-show="status.searchShow" class="search-area">
          <form @submit.prevent="getResume">
            <input type="text" v-model="id" placeholder="input id then press enter">
          </form>
        </div>
      </transition>

    </div>


  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Profile",
  data() {
    return {
      id: null,
      status: {
        searchShow: false
      },
      profile:{
        resMoney:'1000',
        resJobCategoryCn1:'null',
        resSelfIntro: 'null null null null null null'
      }
    }
  },
  props: {
    night: {
      type: Boolean,
      default:false
    }
  },
  methods:{
    getResume(){
      this.$emit('getId',this.id)
      axios.get(process.env.VUE_APP_URL + "/resume/get/" + this.id)
          .then((res) => {
            console.log(res.data)
            if (res)
              this.profile = res.data
          })
          .catch((err) => {
            console.error(err)
          })
    }
  }
}
</script>

<style scoped>

.day{
  background: #FFBECA;
  color: black;
}

.night{
  background: #2C3053;
  color: white;
}


.profile {
  box-shadow: 0 0 33px rgba(0, 0, 0, 0.25);
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  transition: all .5s ease;
  z-index: 1;
}

.img-box {
  flex: 1 0;
}

.img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background-image: url("../assets/profile/1.png");
  background-size: 100px 100px;
  margin-top: 50px;
}

.text-box {
  flex: 4 0;
}
.text-box *{
  transition: all .1s ease !important;
}

.text-box {
  display: flex;
  flex-direction: column;
  place-content: start;
  place-items: center;
  text-align: center;
}

.text-box > p {
  font-size: 15px;
  color: #8C8282;
}

.text-box > h2 {
  font-size: 30px;
}

.text-box > h4 {
  padding: 0 20px;
  overflow: auto;
}

.bottom-box {
  flex: 1 0;
  display: flex;
  justify-content: center;
  align-items: end;
  width: 100%;
  position: relative;
}

.instruct-area {
  padding-bottom: 10px;
}

.instruct {
  width: 150px;
  height: 4px;
  background-color: black;
  border-radius: 5px;
}

.search-area {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  border-radius: 10px;
  box-shadow: -10px 4px 33px rgba(0, 0, 0, 0.25);
}

.search-area input {
  width: 200px;
  height: 2em;
  display: block;
  background: none;
  outline: none;
  border: none;
  box-shadow: 0 0 10px 3px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  padding-left: 10px;
}


.slide-enter-active,
.slide-leave-active {
  transition: opacity .5s ease;
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
}

</style>