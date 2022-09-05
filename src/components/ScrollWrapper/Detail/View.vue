<template>
  <div class="detail-wrapper">
    <detail-name :name="name"></detail-name>

    <detail-stars 
      :star-num="starNum"
      :score="score"
    ></detail-stars>

    <detail-address
      :address="address"
    >
    </detail-address>

    <detail-price :price="price"></detail-price>

    <detail-open-date-time :open-date-time="openDateTime"></detail-open-date-time>

    <detail-tip :tip="tip"></detail-tip>

    <detail-intro
      :intro="intro"
    ></detail-intro>

    <detail-ticket-info
      :ticket-info="ticketInfo"
    ></detail-ticket-info>
  </div>
</template>

<script>
import DetailName from './Sub/Name.vue';
import DetailStars from './Sub/Stars.vue';
import DetailAddress from './Sub/Address.vue';
import DetailPrice from './Sub/Price.vue';
import DetailOpenDateTime from './Sub/OpenDateTime.vue';
import DetailTip from './Sub/Tip.vue';
import DetailIntro from './Sub/Intro.vue';
import DetailTicketInfo from './Sub/TicketInfo.vue';

export default {
  name: 'DetailView',
  components: {
    DetailName,
    DetailStars,
    DetailAddress,
    DetailPrice,
    DetailOpenDateTime,
    DetailTip,
    DetailIntro,
    DetailTicketInfo
  },
  props: {
    name: String,
    starNum: Number,
    score: String,
    address: String,
    price: Number,
    openDateTime: String,
    tip: String,
    intro: String,
    ticketInfo: String
  }
}
</script>

<style lang="scss" scoped>

</style>