<template>
  <div class="home">
    <header class="home-header">
      <span>{{ dateFormat(date) }}</span>
    </header>

    <section class="home-section">
      <div class="left">
        <div class="top">
          <div class="lt">{{ ldnc | money }}</div>
          <div class="lb">{{ ldnf | money }}</div>
          <div class="rt">{{ ldlc | money }}</div>
          <div class="rb">{{ ldlf | money }}</div>
        </div>
        <div class="center">
          <Dcclb />
        </div>
        <div class="bottom">
          <Ddlb />
        </div>
      </div>

      <div class="center">
        <div class="top">
          <div class="l1">
            <span>{{ ssyd | money }}</span>
          </div>
          <div class="l2">
            <span>{{ ssfd | money }}</span>
          </div>
          <div class="l3">
            <span>{{ sscn | money }}</span>
          </div>
          <div class="l4">
            <span>{{ ssxd | money }}</span>
          </div>
        </div>
        <div class="center">
          <Electric />
        </div>
        <div class="bottom">
          <div class="b1">
            <span>{{ jybzm | money }}</span>
          </div>
          <div class="b2">
            <span>{{ co2 | money }}</span>
          </div>
          <div class="b3">
            <span>{{ sox | money }}</span>
          </div>
          <div class="b4">
            <span>{{ nox | money }}</span>
          </div>
          <div class="b5">
            <span>{{ tree }}</span>
          </div>
        </div>
      </div>

      <div class="right">
        <div class="top">
          <div class="lt">{{ ylnc | money }}</div>
          <div class="lb">{{ ylnf | money }}</div>
          <div class="rt">{{ yllc | money }}</div>
          <div class="rb">{{ yllf | money }}</div>
        </div>
        <div class="center">
          <Dfc />
        </div>
        <div class="bottom">
          <Dfd />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Electric from '@/components/Electric.vue'
import Dcclb from '@/components/Dcclb.vue'
import Ddlb from '@/components/Ddlb.vue'
import Dfc from '@/components/Dfc.vue'
import Dfd from '@/components/Dfd.vue'

export default {
  components: { Electric, Dcclb, Ddlb, Dfc, Dfd },
  data () {
    return {
      date: new Date(),
      // ??????
      ldnc: 0, // ????????????
      ldnf: 0, // ???????????? 
      ldlc: 0, // ???????????????
      ldlf: 0, // ???????????????
      // ??????
      ylnc: 0, // ????????????
      ylnf: 0, // ????????????
      yllc: 0, // ???????????????
      yllf: 0, // ???????????????
      // ??????
      jybzm: 0,
      co2: 0,
      sox: 0,
      nox: 0,
      tree: 0,
      // ??????
      // ssyd: 0, // ??????????????????
      ssfd: 0, // ?????????????????????
      ssld: 0,
      ssyl: 0,
      // sscn: 0, // ??????????????????
      ssxd: 0 // ?????????????????????
    }
  },
  created() {
    if (this.timer) {
      clearInterval(this.timer)
    }
    this.timer = setInterval(() => {
      this.date = new Date()
    }, 1000)
    this.startInterval()
    this.getData()
  },
  methods: {
    async getData() {
      // ??????
      const ldnc  = await this.$http.get('/cx/cxLdYearElectricIn/getNearYearElectricIn') // ????????????
      this.ldnc = ldnc.data.data
      const ldnf  = await this.$http.get('/cx/cxLdYearElectricOut/getNearYearElectricOut') // ????????????
      this.ldnf = ldnf.data.data
      const ldlc  = await this.$http.get('/cx/cxLdTotalElectricIn/getNearTotalElectricIn') // ???????????????
      this.ldlc = ldlc.data.data
      const ldlf  = await this.$http.get('/cx/cxLdTotalElectricOut/getNearTotalElectricOut') // ???????????????
      this.ldlf = ldlf.data.data
      // ??????
      const ylnc  = await this.$http.get('/cx/cxYlYearElectricIn/getNearYearElectricIn') // ???????????????
      this.ylnc = ylnc.data.data
      const ylnf  = await this.$http.get('/cx/cxYlYearElectricOut/getNearYearElectricOut') // ???????????????
      this.ylnf = ylnf.data.data
      const yllc  = await this.$http.get('/cx/cxYlTotalElectricIn/getNearTotalElectricIn') // ???????????????
      this.yllc = yllc.data.data
      const yllf  = await this.$http.get('/cx/cxYlTotalElectricOut/getNearTotalElectricOut') // ???????????????
      this.yllf = yllf.data.data
      // ??????
      const jybzm  = await this.$http.get('/cx/cxGfSaveStandardCoal/getNearAmount') // ???????????????
      this.jybzm = jybzm.data.data
      const co2  = await this.$http.get('/cx/cxGfBlowdownCo2/getNearAmount') // co2
      this.co2 = co2.data.data
      const sox  = await this.$http.get('/cx/cxGfBlowdownSox/getNearAmount') // sox
      this.sox = sox.data.data
      const nox  = await this.$http.get('/cx/cxGfBlowdownNox/getNearAmount') // nox
      this.nox = nox.data.data
      const tree  = await this.$http.get('/cx/cxGfTotalTreePlanting/getNearAmount') // ??????
      this.tree = tree.data.data
      // ??????
      const ssfd  = await this.$http.get('/cx/cxGfPowerNow/getNearPower') // ?????????????????????
      this.ssfd = ssfd.data.data
      const ssxd  = await this.$http.get('/cx/cxCyPowerNow/getNearPower') // ?????????????????????
      this.ssxd = ssxd.data.data
      const ssld  = await this.$http.get('/cx/cxLdPowerNow/getNearPower') // ????????????
      this.ssld = ssld.data.data
      const ssyl  = await this.$http.get('/cx/cxYlPowerNow/getNearPower') // ????????????
      this.ssyl = ssyl.data.data
    },
    dateFormat(time) {
      var date=new Date(time)
      var year=date.getFullYear()
      var month= date.getMonth() + 1 < 10 ? "0" + (date.getMonth() + 1) : date.getMonth() + 1
      var day=date.getDate() < 10 ? "0" + date.getDate() : date.getDate()
      var hours=date.getHours() < 10 ? "0" + date.getHours() : date.getHours()
      var minutes=date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes()
      var seconds=date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds()
      return year + "-" + month + "-" + day + " " + hours + ":" + minutes + ":" + seconds
    },
    startInterval() {
      if(this.timeData) {
        clearInterval(this.timeData)
      }
      this.timeData = setInterval(() => {
        this.getData()
      }, 5 * 60 * 1000)
    }
  },
  computed: {
    ssyd() {
      return this.ssfd + this.ssld + this.ssyl + this.ssxd
    },
    sscn() {
      return this.ssld + this.ssyl
    }
  },
  beforeDestroy() {
    clearInterval(this.timer)
    clearInterval(this.timeData)
  }
}
</script>

<style lang="scss" scoped>
  .home {
    position: relative;
    .home-header {
      span {
        position: absolute;
        font-size: 34px;
        top: 118px;
        left: 826px;
        color: #fff;
        font-family: monoMMM-5-1;
      }
    }
    .home-section {
      .left {
        .top {
          font-size: 26px;
          font-family: monoMMM-5-1;
          color: #fff;
          .lt {
            position: absolute;
            top: 236px;
            left: 80px;
          }
          .lb {
            position: absolute;
            top: 330px;
            left: 80px;
          }
          .rt {
            position: absolute;
            top: 236px;
            left: 298px;
          }
          .rb {
            position: absolute;
            top: 330px;
            left: 298px;
          }
        }
        .center {
          position: absolute;
          top: 452px;
          left: 40px;
        }
        .bottom {
          position: absolute;
          top: 770px;
          left: 40px;
        }
      }
      .center {
        .top {
          font-size: 36px;
          font-family: monoMMM-5-1;
          div {
            width: 220px;
            height: 110px;
            line-height: 110px;
            text-align: center;
          }
          .l1 {
            color: rgb(180, 244, 148);
            position: absolute;
            top: 244px;
            left: 502px;
            text-shadow: 0 0 15px #b8ff98,
                         0 0 15px #48ff4c;
          }
          .l2 {
            color: rgb(132, 216, 221);
            position: absolute;
            top: 244px;
            left: 734px;
            text-shadow: 0 0 15px #98fff9,
                         0 0 15px #48f9ff;
          }
          .l3 {
            color: rgb(159, 172, 255);
            position: absolute;
            top: 244px;
            left: 966px;
            text-shadow: 0 0 15px #98a4ff,
                         0 0 15px #4873ff;
          }
          .l4 {
            color: rgb(244, 161, 255);
            position: absolute;
            top: 244px;
            left: 1200px;
            text-shadow: 0 0 15px #e898ff,
                         0 0 15px #e748ff;
          }
        }
        .center {
          position: absolute;
          top: 452px;
          left: 500px;
        }
        .bottom {
          font-size: 24px;
          font-family: monoMMM-5-1;
          color: #fff;
          div {
            width: 98px;
            height: 30px;
            line-height: 30px;
            text-align: center;
          }
          .b1 {
            position: absolute;
            top: 924px;
            left: 538px;
          }
          .b2 {
            position: absolute;
            top: 924px;
            left: 724px;
          }
          .b3 {
            position: absolute;
            top: 924px;
            left: 914px;
          }
          .b4 {
            position: absolute;
            top: 924px;
            left: 1102px;
          }
          .b5 {
            width: 90px;
            position: absolute;
            top: 924px;
            left: 1290px;
          }
        }
      }
      .right {
        .top {
          font-size: 26px;
          font-family: monoMMM-5-1;
          color: #fff;
          .lt {
            position: absolute;
            top: 236px;
            left: 1498px;
          }
          .lb {
            position: absolute;
            top: 330px;
            left: 1498px;
          }
          .rt {
            position: absolute;
            top: 236px;
            left: 1714px;
          }
          .rb {
            position: absolute;
            top: 330px;
            left: 1714px;
          }
        }
        .center {
          position: absolute;
          top: 452px;
          right: 30px;
        }
        .bottom {
          position: absolute;
          top: 770px;
          right: 30px;
        }
      }
    }
  }
</style>