<template>
<div class="content" :class="night ? 'night':'day'">
  <div class="header">
    <div class="today">
      <svg class="icon" aria-hidden="true" @click="alternative">
        <use v-if="night" xlink:href="#icon-yewan"></use>
        <use v-else xlink:href="#icon-qing"></use>
      </svg>
      <div>{{time}}</div>
    </div>
    <div class="menu">
      <h4 :class="selected === 1 ? 'selected' : 'none'" @click="selected = 1">Recommend</h4>
      <h4 :class="selected === 2 ? 'selected' : 'none'" @click="selected = 2">Category</h4>
      <h4 :class="selected === 3 ? 'selected' : 'none'" @click="selected = 3">Other</h4>
    </div>
  </div>

  <div class="job-display">
    <JobCard v-for="(job,idx) in jobShowList" :key="job.id" :job="job"
             :position="positions[idx]"
             :frame-size="{
               width:'910px',
               height:'500px'
             }"></JobCard>
  </div>

  <div class="footer"></div>
</div>


</template>

<script>
import JobCard from "@/components/card/JobCard";
import axios from "axios"

export default {
  name: "Content",
  data() {
    return {
      positions: [
        {
          left: 0,
        },
        {
          left: '330px'
        },
        {
          left: '660px'
        },
      ],
      page: 1,
      jobRecommendList: [
        {
          jobKind: '全职',
          jobName: '神盾局特工',
          jobRequirement: 'test test test test test test test test test test test test test test' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test' +
              'test test test test test test test test test test test test test test' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test test ' +
              'test test test test test test test test test test test test test fuck',
          score: 100
        },
        {
          jobKind: '全职',
          jobName: '神盾局秘书',
          jobRequirement: 'test test test test test test test test test test test test test test',
          score: 100

        },
        {
          jobKind: '全职',
          jobName: '神盾局爸爸',
          jobRequirement: 'test test test test test test test test test test test test test test',
          score: 100
        },
        {
          jobKind: '全职',
          jobName: '灭霸',
          jobRequirement: 'test test test test test test test test test test test test test test',
          score: 100
        },
      ],
      timestamp:new Date(),
      timer:null,
      selected:1,
      night:false
    }
  },
  props:{
    id:String
  },
  watch:{
    id(){
      axios.get(process.env.VUE_APP_URL + "/job/recommend/" + this.id)
          .then((res) => {
            console.log(res.data)
            if (res)
              this.jobRecommendList = res.data
          })
          .catch((err) => {
            console.error(err)
          })
    }
  },
  computed: {
    jobShowList() {
      let start = (this.page - 1) * 3
      return this.jobRecommendList.slice(start, start + 3)
    },
    time(){
      return this.timestamp.toLocaleTimeString()
    }
  },
  mounted() {
    this.timer = setInterval(() => {
      this.timestamp = new Date()
    },1000)

    // axios.get(process.env.VUE_APP_URL + "/job/recommend/" + this.id)
    //     .then((res) => {
    //       if (!res)
    //         this.jobRecommendList = res.data
    //       console.log(this.jobRecommendList)
    //     })
    //     .catch((err) => {
    //       console.error(err)
    //
    //     })
  },
  beforeUnmount() {
    clearInterval(this.timer)
  },
  methods: {
    alternative(){
      this.night = !this.night
      this.$emit('alternative',this.night)
    }
  },


  components: {
    JobCard
  }
}
</script>

<style scoped>


.day{
  background-image: url("../assets/background/moring.png");
  color: black;
}

.night{
  background-image: url("../assets/background/night.png");
  color: white;
}

.content{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-repeat: no-repeat;
  background-size: contain;
  transition: all.5s ease;
}

.job-display{
  position: relative;
  width: 910px;
  height: 60%;
}

.job-display *{
  transition: all .5s ease;
}



.page-box {
  width: 910px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.page-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.page-box > svg {
  width: 50px;
  height: 30px;
}

.page-box > svg:hover {
  transform: scale(120%);
}

.header{
  width: 100%;
  height: 8%;
  display: flex;
  justify-content: space-between;
}
.header > .menu{
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 50%;
}
.header > .menu *{
  transition: all .1s ease;
}

.header > .today{
  margin-left: 40px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 10%;
}
.header > .today > svg{
  width: 30px;
  height: 30px;
}

.header .none::after{
  display: block;
  content: '';
  width: 100%;
  height: 4px;
  background-color: darkslategray;
  opacity: 0;
  border-radius: 2px;
}

.header .selected::after{
  display: block;
  content: '';
  width: 100%;
  height: 4px;
  opacity: 1;
  background-color: darkslategray;
  border-radius: 2px;
}


.footer{
  width: 100%;
  height: 8%;
}


</style>