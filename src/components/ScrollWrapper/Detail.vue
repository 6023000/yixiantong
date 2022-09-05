<template>
   <div class="scroll-wrapper" ref="wrapper">
    <div class="scroll-content">
     <template v-if="!errorShow">
      <detail-swiper
        :pic-datas="detailDatas.pics"
      ></detail-swiper>

      <detail-food 
        v-if="field === 'food'"
        :name="detailDatas.name"
        :star-num="Number(detailDatas.star)"
        :score="detailDatas.score"
        :address="detailDatas.address"
        :price="Number(detailDatas.default_price)"
        :open-date-time="detailDatas.open_datetime"
        :recom="detailDatas.recom"
        :comment-keyword="detailDatas.comment_keyword"
      ></detail-food>

      <detail-view
        v-if="field === 'view'"
        :name="detailDatas.name"
        :star-num="Number(detailDatas.star)"
        :score="detailDatas.score"
        :address="detailDatas.address"
        :price="Number(detailDatas.default_price)"
        :open-date-time="detailDatas.open_datetime"
        :tip="detailDatas.tip"
        :intro="detailDatas.intro"
        :ticket-info="detailDatas.ticket_info"
      ></detail-view>

      <detail-hotel
        v-if="field === 'hotel'"
        :name="detailDatas.name"
        :star-num="Number(detailDatas.star)"
        :score="detailDatas.score"
        :address="detailDatas.address"
        :price="Number(detailDatas.default_price)"
        :service="detailDatas.service"
      ></detail-hotel>

      <detail-massage
        v-if="field === 'massage'"
        :name="detailDatas.name"
        :star-num="Number(detailDatas.star)"
        :score="detailDatas.score"
        :address="detailDatas.address"
        :price="Number(detailDatas.default_price)"
        :open-date-time="detailDatas.open_datetime"
        :comment-keyword="detailDatas.comment_keyword"
        :service="detailDatas.service"
      ></detail-massage>

      <detail-ktv
        v-if="field === 'ktv'"
        :name="detailDatas.name"
        :star-num="Number(detailDatas.star)"
        :score="detailDatas.score"
        :address="detailDatas.address"
        :price="Number(detailDatas.default_price)"
        :service="detailDatas.service"
      ></detail-ktv>
     </template>

     <error
      :errorShow="errorShow"
     ></error>
    </div>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll';
import {DetailModel} from 'models/detail';
import DetailSwiper from './Sub/Swiper.vue';

import DetailFood from './Detail/Food.vue';
import DetailView from './Detail/View.vue';
import DetailHotel from './Detail/Hotel.vue';
import DetailMassage from './Detail/Massage.vue';
import DetailKtv from './Detail/Ktv.vue';

import Error from './Sub/Error.vue';

import tools from 'utils/tools';

export default {
  name: 'DetailScrollWrapper',
  components: {
    DetailSwiper,
    DetailFood,
    DetailView,
    DetailHotel,
    DetailMassage,
    DetailKtv,
    Error
  },
  data() {
    return {
      field: '',
      id: 0,
      detailDatas: {},
      errorShow: false
    }
  },
  mounted() {
    this.scroll = new BetterScroll(this.$refs.wrapper);
    this.field = this.$route.query.field;
    this.id = this.$route.query.id;
    this.getDetail(this.field, this.id);
  },
  activated() {
    this.currentField = this.$route.query.field;
    this.currentId = this.$route.query.id;

    if(this.currentField !== this.field || this.currentId !== this.id) {
      this.field = this.currentField;
      this.id = this.currentId;

      this.getDetail(this.field, this.id);
    }
  },
  methods: {
    getDetail(field, id) {
      const detailModel = new DetailModel();
      
      detailModel.getDetail(field, id).then((res) => {
        if(res && res.status === 0) {
          const data = res.data;
        
          this.errorShow = false;
          data.pics && (data.pics = tools.jsonToArr(data.pics));
          data.comment_keyword && (data.comment_keyword = tools.strToArr(data.comment_keyword));
          data.recom && (data.recom = tools.replaceToSpace(data.recom));
          data.service && (data.service = tools.jsonToArr(data.service));

          this.detailDatas = data;
        } else {
          this.errorShow = true;
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>