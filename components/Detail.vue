<template>
  <div style="margin: 20px; background-color: #c2c2c2; padding: 30px">
    <h4>Order Detail</h4>
    <CardItem />
    <card-item style="padding: 20px 0px 20px 0px" />
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
      <AtomsButton content="Oke" style="float: right" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    userInfo: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
ds
<style>
.card-detail {
  font-weight: 600;
  line-height: 1.8;
  display: flex;
  border: 1px solid black;
  padding: 10px 34px;
}
</style>
