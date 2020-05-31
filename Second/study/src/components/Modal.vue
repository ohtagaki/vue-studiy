<template>
    <div id = "overlay">
        <div id = "content">
            <p>これがモーダルウインドウです。</p>
            <button @click="selectCity({cityId: '474010', cityName:'石垣島'})">熊本の天気予報を表示</button>
            <br>
            <button @click="closeModal">Close</button>
            <ResultModal v-if="showResultModal" v-on:from-child="closeResultModal" v-bind:cityInfo="cityInfo" />
        </div>
    </div>
</template>

<script>
import ResultModal from './ResultModal'
export default {
  name: 'Modal',
  components: {
      ResultModal
  },
  data() {
    return {
      showResultModal: false,
      cityInfo: {
        cityId: String,
        cityName: String
      }
    }
  },
  methods: {
    closeModal(){
            this.$emit('from-child')
    },
    selectCity(cityInfo) {
      this.showResultModal = true
      this.cityInfo.cityId = cityInfo.cityId
      this.cityInfo.cityName = cityInfo.cityName
    },
    closeResultModal () {
      this.showResultModal = false
    }
  }
}
</script>

<style>
#overlay{
  /* 要素を重ねた時の順番 */
  z-index:1;

  /* 画面全体を覆う設定 */
  position:fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  background-color:rgba(0,0,0,0.5);

  /* 画面の中央に要素を表示させる設定 */
  display: flex;
  align-items: center;
  justify-content: center;

}
#content{
  z-index:2;
  width:50%;
  padding: 1em;
  background:#fff;
}
</style>
