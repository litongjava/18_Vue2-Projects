<template>
<div>
  <p class="title"><i></i>疫情地图</p>
  <div id="map" class="map"></div>
</div>
</template>

<script>
import api from "../api"

export default {
  name: "covidMap",
  mounted() {
    api.getprovinceNcov().then(res => {
      //console.log(res.data);
      let allCities = [];
      for (let i = 0; i < res.data.retdata.length; i++) {
        var temp = {
          name: res.data.retdata[i].xArea,
          value: res.data.retdata[i].curConfirm
        }
        allCities.push(temp);
      }
      this.$charts.chinaMap("map",allCities)
    }).catch(error => {
      console.log(error)
    });
  }
}
</script>

<style scoped>
.map {
  width: 375px;
  height: 400px;
}

.title {
  border-top: 0.005rem solid #ebebeb;
  border-bottom: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  height: 0.44rem;
  padding: 0 0.16rem;
  font-weight: 500;
  font-size: 0.17rem;
  line-height: 0.44rem;
  background: #fff;
}

.title::before {
  content: "";
  width: 5px;
  height: 20px;
  background: #4169e2;
  margin-right: 10px;
}
</style>
