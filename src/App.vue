<template>
  <div class="content_map">
    <div id="map"></div>
  </div>
</template>

<script>
// import 'leaflet/dist/leaflet.css';
// import './leaflet/L.Control.MousePosition';
// import './leaflet/L.Control.MousePosition.css';
import { cloneDeep } from 'lodash';
// import 'leaflet-measure-ex/dist/leaflet-measure';
// import 'leaflet-measure-ex/dist/leaflet-measure.css';
// import './leaflet/leaflet-measure.css';
// import './leaflet/leaflet-measure.cn';

let map = null;
let basemap = null;
let scaleControl = null;
let zoomControl = null;
let mapBounds = null;
const basemapUrl =
  'https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}';
const basemapProp = {};
const L = window.L;
export default {
  name: 'ContentMap',
  data() {
    return {};
  },
  computed: {},
  watch: {},
  mounted() {
    this.initDate();
  },
  beforeDestroy() {
    map.remove();
  },
  methods: {
    initDate() {
      map = L.map('map', {
        center: [39.077514, 117.713544], // 地图中心
        zoom: 18, //缩放比列
        scrollWheelZoom: true, // 允许鼠标滚轮缩放地图
        positionControl: true, // 左下角显示当前位置
      });

      // 初始化地图图层 缩放比例等
      const tileProps = cloneDeep(basemapProp);
      basemap = L.tileLayer(basemapUrl, tileProps);
      basemap.addTo(map);
      L.control.measure().addTo(map);
    },
  },
};
</script>
<style lang="scss">
.leaflet-bar a,
.leaflet-control > a {
  background-color: #999 !important;
  border-color: #000 !important;
  color: #f6e5bd !important;

  &:hover {
    background-color: #555 !important;
  }
}
.leaflet-control-scale-line {
  border: 2px solid #444 !important;
  background: #999 !important;
  text-shadow: none !important;
  color: #f6e5bd !important;
}
</style>
<style lang="scss">
.content_map {
  position: relative;
  width: 100%;
  height: 100%;
  #map {
    position: absolute;
    // width: 100%;
    // height: 100%;
    height: 800px;
    width: 800px;
    z-index: 1;
  }
}
</style>
