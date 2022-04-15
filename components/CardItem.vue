<template>
  <div class="container-card">
    <div
      class="grid-card"
      style="grid-template-columns: auto auto; justify-content: space-between"
    >
      <div>
        Order Id: <span class="bold">{{ userInfo.orderId }}</span>
      </div>
      <div>Created At: {{ userInfo.createdAt }}</div>
    </div>
    <div class="grid-card" style="border-style: none solid solid solid">
      <div class="account-info" style="line-height: 1.8">
        <p>Info Akun</p>
        <p class="bold">{{ userInfo.personalAccount.name }}</p>
        <p class="bold">{{ userInfo.personalAccount.email }}</p>
        <p class="bold">{{ userInfo.personalAccount.phonenumber }}</p>
      </div>
      <div class="packet-info">
        <div>
          <p>Provider</p>
          <p>Paket</p>
          <p>Exp</p>
        </div>
        <div>
          <p class="bold">{{ userInfo.provider }}</p>
          <p class="bold">{{ userInfo.packet }}</p>
          <p class="bold">{{ userInfo.expired }}</p>
        </div>
        <div>
          <p class="bold" style="font-size: x-large">
            Rp. <span>{{ userInfo.payment.paymentTotal }}</span>
          </p>
        </div>
      </div>
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

<style>
.container-card {
  margin: 20px;
}
.header-card {
  width: 100%;
  border: 2px solid indigo;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

.bold {
  font-weight: bold;
}

.grid-card {
  border-style: solid solid none solid;
  border: 2px solid indigo;
  display: grid;
  grid-template-columns: 50% 50%;
  gap: 10px;
  padding: 10px;
}

.grid-card > div {
  text-align: start;
}

.packet-info {
  line-height: 1.8;
  display: grid;
  grid-template-columns: 70px auto auto;
  align-items: center;
  border: 2px solid indigo;
  border-style: none none none solid;
  padding: 0px 0px 0px 30px;
}

.tab1 {
  tab-size: 16;
}

.account-info > p {
  padding-left: 24px;
}
</style>
