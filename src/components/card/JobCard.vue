<template>
  <div :style="[position,expend ? frameSize:'']"
       @click="expend=true"
       @mouseleave="expend=false"
       class="profile-wrapper"
       :class="expend ? 'expend' : 'normal'">
    <div class="image-box">
      <div class="img"></div>
    </div>
    <div class="text-box">
      <h1>{{ job.jobName }}</h1>
      <p>上海</p>
      <p>{{ job.jobKind }}</p>
      <h2>{{ job.score }}</h2>
      <p class="detail">{{ job.jobRequirement }}</p>
    </div>
    <div class="bottom-box">
      <div class="button" @click="contact">Contact</div>
    </div>
  </div>

</template>

<script>


export default {
  name: "jobCard",
  data() {
    return {
      expend: false
    }
  },
  props: {
    job: Object,
    position: Object,
    frameSize:Object
  },
  watch: {},
  methods: {
    contact() {
      console.log("get it")
    },
    doExpend(){

    },
    backNormal(){

    }
  }

}
</script>

<style scoped>
*{
  transition: all .5s ease;
}

/*外边距重叠解决*/
.profile-wrapper::before {
  content: '';
  display: table;
}


.profile-wrapper {
  color: darkslategray;
  position: absolute;
  top: 60px;
  width: 250px;
  height: 350px;
  background: #FFFFFF;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
  padding: 20px 25px;
  border-radius: 10px;
}


/*风格样式*/
.expend {
  left: 0 !important;
  top: 0 !important;
  z-index: 1;
}

.expend > .image-box > * {
  margin-left: 0;
}

.expend > .text-box > * {
  text-align: start;
  margin-left: 0;
}

.expend > .text-box > .detail {
  width: 860px;
  height: 200px;
}


.expend > .bottom-box {
  width: 100%;
  margin-left: 0;
  margin-top: 10px;
  display: flex;
  justify-content: end;
}

/*元素间距部分*/
.normal > .image-box {
  margin-left: 75px;
}

.normal > .text-box {
  margin-top: 10px
}

.normal > .text-box > * {
  text-align: center;
}

.normal > .text-box > .detail {
  width: 0;
  height: 0;
}

.normal > .bottom-box {
  width: 120px;
  margin-top: 20px;
  margin-left: 40px;
  display: flex;
  justify-content: center;
}


/*-------------整体局部布局分界线-------------*/


.image-box {
  width: 50px;
}

.img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-image: url("../../assets/profile/1.png");
  background-size: 50px 50px;
}


.text-box > * {
  line-height: 2em;
}


.text-box > :not(:last-child) {
  width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}


.text-box p {
  font-size: 15px;
}

.text-box h1 {
  font-size: 25px;
}

.detail {
  overflow: auto;
}


::-webkit-scrollbar-thumb {
  background-color: rgba(184, 183, 177, 80%);
  border-radius: 20px;
  max-height: 5px;
}

::-webkit-scrollbar {
  width: 5px;
}


.button {
  width: 120px;
  height: 40px;
  border-radius: 60px;
  background-color: #0093FE;
  line-height: 40px;
  text-align: center;
  color: white;
  font-family: "SF Pro Text Regular", serif;
}


.button:hover {
  background-color: #FF558E;
  transition: none !important;
}


</style>