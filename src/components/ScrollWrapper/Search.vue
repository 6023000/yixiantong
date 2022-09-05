<template>
  <div class="scroll-wrapper" ref="wrapper">
    <div class="scroll-content">
      <template v-if="!data.status">
        <no-data-tip
        v-show="
          (!data.viewDatas || data.viewDatas.length <= 0) &&
          (!data.foodDatas || data.foodDatas.length <= 0) &&
          (!data.hotelDatas || data.hotelDatas.length <= 0) &&
          (!data.massageDatas || data.massageDatas.length <= 0) &&
          (!data.ktvDatas || data.ktvDatas.length <= 0)
        "
      ></no-data-tip>

      <template v-if="data.viewDatas && data.viewDatas.length > 0">
        <home-title title="景点结果： "></home-title>
        <view-list :viewDatas="data.viewDatas"></view-list>
      </template>

      <template v-if="data.foodDatas && data.foodDatas.length > 0">
        <home-title title="美食结果： "></home-title>
        <food-list :foodDatas="data.foodDatas"></food-list>
      </template>

      <template v-if="data.hotelDatas && data.hotelDatas.length > 0">
        <home-title title="酒店结果： "></home-title>
        <hotel-list :hotelDatas="data.hotelDatas"></hotel-list>
      </template>

      <template v-if="data.massageDatas && data.massageDatas.length > 0">
        <home-title title="按摩结果： "></home-title>
        <massage-list :massageDatas="data.massageDatas"></massage-list>
      </template>

      <template v-if="data.ktvDatas && data.ktvDatas.length > 0">
        <home-title title="酒店结果： "></home-title>
        <ktv-list :ktvDatas="data.ktvDatas"></ktv-list>
      </template>

      </template>
      <error :errorShow="data.status === -1"></error>
    </div>
  </div>
</template>

<script>
import BetterScroll from "better-scroll";

import ViewList from "./ViewList";
import HotelList from "./HotelList";
import FoodList from "./FoodList";
import MassageList from "./MassageList";
import KtvList from "./KtvList";
import HomeTitle from "./Sub/HomeTitle.vue";
import NoDataTip from "./Sub/NoDataTip.vue";
import Error from './Sub/Error.vue';

export default {
  name: "SearchScrollWrapper",
  components: {
    ViewList,
    HotelList,
    FoodList,
    MassageList,
    KtvList,
    HomeTitle,
    NoDataTip,
    Error
  },
  props: {
    data: Object,
  },
  mounted() {
    this.scroll = new BetterScroll(this.$refs.wrapper);
  },
};
</script>

<style lang="scss" scoped>
</style>