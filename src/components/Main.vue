<template>
  <div>
    <box gap="10px 10px">
      <button-tab>
        <button-tab-item>500m</button-tab-item>
        <button-tab-item selected>1000m</button-tab-item>
        <button-tab-item>2000m</button-tab-item>
      </button-tab>  
    </box>

    <box gap="10px 10px">
      <x-button type="primary" @click="search()">老天开始决定吧</x-button>
      <x-button plain type="primary">已经选出来的记录</x-button>
    </box>

  </div>
</template>

<script>
import { Box, ButtonTab, ButtonTabItem, XButton } from "vux";
import axios from "axios";

export default {
  components: {
    Box,
    ButtonTab,
    ButtonTabItem,
    XButton
  },

  data() {
    return {
      lat: "",
      lng: ""
    };
  },

  mounted() {
    this.getLocation();
  },

  methods: {
    showPosition(position) {
      console.log(position);
      console.log("定位完成");
      this.lat = position.lat;
      this.lng = position.lng;
      console.log(this.lat + "  " + this.lng);
      // if (position.addr) {
      //     addr = position.addr;
      //     saveData();
      //     document.getElementById('location').innerHTML = addr;
      //     search(0, 1, 1000);
      // } else {
      //     document.getElementById('location').innerHTML = "未获取到位置，请重新定位";
      //     showErr();
      // }
    },

    showErr() {
      console.log("定位失败，请刷新重试");
      // $.alert("定位失败，请刷新重试", function() {
      //   //点击确认后的回调函数
      //   // location.reload();
      // });
    },

    getLocation() {
      let geolocation = new qq.maps.Geolocation(
        "OB4BZ-D4W3U-B7VVO-4PJWW-6TKDJ-WPB77",
        "myapp"
      );
      let options = {
        timeout: 8000,
        failTipFlag: true
      };
      geolocation.getLocation(this.showPosition, this.showErr, options);
    },

    search() {
      axios.get("https://apis.map.qq.com/ws/place/v1/search", {
          params: {
            keyword: '餐厅',
            // boundary: 'nearby(' + lat + ',' + lng + ',' + ranges + ')',
            boundary: 'nearby(31.193333,121.435165,1000)',
            orderby: '_distance',
            page_size: 10,
            page_index: 1,
            key: 'd84d6d83e0e51e481e50454ccbe8986b',
          }
        })
        .then(function(res) {
          console.log(response);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>

<style lang="less">

</style>