<template>
  <div class="scroll-wrapper" ref="wrapper">
    <div class="scroll-content">
     <template v-if="!errorShow">
       <view-list
        v-if="field === 'view'"
        :viewDatas="listDatas[cityId]"
      ></view-list>
      <food-list
        v-if="field === 'food'"
        :foodDatas="listDatas[cityId]"
      ></food-list>
      <hotel-list
        v-if="field === 'hotel'"
        :hotelDatas="listDatas[cityId]"
      ></hotel-list>
      <massage-list
        v-if="field === 'massage'"
        :massageDatas="listDatas[cityId]"
      ></massage-list>
      <ktv-list
        v-if="field === 'ktv'"
        :ktvDatas="listDatas[cityId]"
      ></ktv-list>

      <loading :loadingShow="loadingShow"></loading>

     </template>
     <error :errorShow="errorShow"></error>
    </div>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll';
import {mapState} from 'vuex';

import ViewList from './ViewList';
import HotelList from './HotelList';
import FoodList from './FoodList';
import MassageList from './MassageList';
import KtvList from './KtvList';
import Loading from './Sub/Loading';
import Error from './Sub/Error.vue';

import {ListModel} from 'models/list';
import tools from 'utils/tools';


export default {
  name: 'ListScrollWrapper',
  components: {
    ViewList,
    HotelList,
    FoodList,
    MassageList,
    KtvList,
    Loading,
    Error
  },
  data() {
    return {
      loadingShow: true,
      listDatas: {},
      errorShow: false
    }
  },
  computed: {
    ...mapState(['cityId', 'field'])
  },
  mounted() {
    this.scroll = new BetterScroll(this.$refs.wrapper);
    this.getListDatas(this.cityId, this.field);
  },
  methods: {
    getListDatas(cityId, field) {
      if(!this.listDatas[cityId]) {
        const listModel = new ListModel();

        this.loadingShow = true;

        listModel.getListDatas(cityId, field).then((res) => {
          if(res && res.status == 0) {
            const data = tools.formatJSON(res.data, 'keyword');
            this.errorShow = false;

            setTimeout(() => {
              this.listDatas[cityId] = data;
              this.loadingShow = false;
            }, 500)

          } else {
            this.errorShow = true;
          }
        })
      }
    }
  },

  watch: {
    cityId () {
      this.getListDatas(this.cityId, this.field);
    }
  }
}
</script>

<style lang="scss" scoped>

</style>