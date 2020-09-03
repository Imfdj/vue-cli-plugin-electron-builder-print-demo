<template>
  <div class="home">
    <template>
      <div>
        <button class="silentBtn" @click="silentSwitch">{{isSilent? 'close': 'open'}} silent print</button>
      </div>
      <div class="wrap-direction">
        <h3>Image rotation direction</h3>
        <div class="wrap-btn">
          <button @click="rotateTypeChange(0)">normal</button>
          <button @click="rotateTypeChange(1)">Clockwise</button>
          <button @click="rotateTypeChange(2)">Counterclockwise</button>
          <button @click="rotateTypeChange(3)">Upside down</button>
        </div>
      </div>
      <div class="wrap-printer-list">
        <h3>printer list</h3>
        <ol>
          <li v-for="(item, index) in printerList" :key="index">
            <span>{{item.name}}</span>
            <button @click="pitchOn(item)">pitch on</button>
          </li>
        </ol>
      </div>
      <div class="index">
        <electron-vue-printer
          ref="electronVuePrinter"
          :show="true"
          :options="options"
          :rotateType="rotateType"
          :silent="isSilent"
          @webview-ready="webviewReady"
          @get-printer-list="getPrinterList"
        ></electron-vue-printer>
      </div>
    </template>
  </div>
</template>

<script>
import electronVuePrinter from 'electron-vue-printer'
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
    electronVuePrinter
  },
  data () {
    return {
      isSilent: false,
      rotateType: 0,
      printerList: [],
      options: {
        offsetX: 100,
        offsetY: 100,
        imageWidth: 300
      }
    }
  },
  methods: {
    webviewReady () {
      // this.$refs.electronVuePrinter.print('https://cdn.pixabay.com/photo/2017/06/10/07/29/printer-2389244_960_720.png')
    },
    getPrinterList (list) {
      // this.printerList = list
      this.printerList = list.concat([{ name: 'inexistent printer' }])
    },
    rotateTypeChange (value) {
      this.options.offsetX = value * 30
      this.options.imageWidth = 300 + value * 30
      this.rotateType = value
      this.$refs.electronVuePrinter.print('https://cdn.pixabay.com/photo/2017/06/10/07/29/printer-2389244_960_720.png')
    },
    pitchOn (item) {
      this.$refs.electronVuePrinter.setPrinterName(item.name, (err) => {
        if (err) {
          alert(err.message)
        } else {
          alert(`Successfully set the printer name to ${item.name}`)
        }
      })
    },
    silentSwitch () {
      this.isSilent = !this.isSilent
    }
  }
}
</script>

<style lang="less" scoped>
  .home {
    position: relative;
    .silentBtn {
      background-color: #37da3c;
      font-size: 26px;
      margin: 9px;
    }
    .wrap-direction {
      padding: 10px;
      box-shadow: 0px 0px 10px #ccc;
      .wrap-btn {
        display: flex;
        justify-content: space-between;
        width: 600px;
        margin: 0 auto;
      }
    }
    .wrap-printer-list {
      padding: 3px;
      margin-top: 10px;
      box-shadow: 0px 0px 10px #ccc;
      & li {
        margin-top: 3px;
      }
      & button {
        margin-left: 10px;
      }
    }
  }
</style>
