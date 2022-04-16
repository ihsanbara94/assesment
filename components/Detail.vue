<template>
  <div
    v-if="isShowDetail"
    style="margin: 20px; background-color: #92defc; padding: 30px; color: black"
  >
    <h4>Order Detail</h4>
    <CardItem
      :user-info="userInfo"
      style="padding: 20px 0px 20px 0px; font-size: small"
    />
    <div class="card-detail">
      <div>
        <p>Voucher Code</p>
        <p>Payment Status</p>
        <p>Payment Date</p>
        <p>Payment Bank</p>
      </div>
      <div style="padding-left: 10px">
        <p>
          : <span>{{ userInfo.voucher }}</span>
        </p>
        <p>
          : <span>{{ userInfo.payment.status }}</span>
        </p>
        <p>
          : <span>{{ userInfo.createdAt }}</span>
        </p>
        <p>
          : <span>{{ userInfo.payment.bank }}</span>
        </p>
      </div>
    </div>
    <div style="padding: 20px 0px">
      <AtomsButton
        @click="$emit('close-card')"
        content="Oke"
        style="float: right"
      />
    </div>
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";
export default {
  components: { CardItem },
  props: {
    userInfo: {
      type: Object,
      default: () => {},
    },
    isShowDetail: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
ds
<style>
.card-detail {
  font-size: small;
  font-weight: 600;
  line-height: 1.8;
  display: flex;
  border: 2px solid indigo;
  padding: 10px 34px;
  margin: 20px;
}
</style>
