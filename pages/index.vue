<template>
  <div>
    <navbar />
    <div class="sidenav">
      <a href="#about">Order List</a>
      <a href="#services">About</a>
    </div>
    <div class="main">
      <h2 style="padding: 20px">Order List</h2>
      <div class="padding-body">
        <div>
          <input
            type="text"
            placeholder="search by name"
            style="padding: 0.25rem 0.75rem"
            v-model="searchKey"
            @keyup.enter="getKeywords()"
          />
          <Button content="Submit" @click="getKeywords()" />
        </div>

        <Dropdown
          @click="dropdownFilter"
          :listDropdown="listDropdown"
          :choosedList="filter"
          :isOpen="isOpenFilter"
          @click-list="chooseFilter"
        />
      </div>

      <div v-for="(user, id) in search" :key="id">
        <CardItem :userInfo="user" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardItem from "../components/CardItem.vue";
import Navbar from "../components/Navbar.vue";
import Button from "~/components/atoms/Button";
import Dropdown from "~/components/atoms/Dropdown.vue";
export default {
  components: { Navbar, CardItem, Button, Dropdown },
  name: "IndexPage",
  data() {
    return {
      users: [],
      search: [],
      searchKey: "",
      value: "",
      filter: "Sort",
      isOpenFilter: false,
      listDropdown: ["Ascending", "Descending"],
    };
  },
  watch: {
    page() {
      this.getDataUser();
    },
    choosedList() {
      this.value = this.choosedList;
    },
  },
  mounted() {
    this.getDataUser();
  },
  methods: {
    getDataUser() {
      axios
        .get("http://demo3789050.mockable.io/order")
        .then((res) => {
          console.log(res.data);
          this.users = res.data;
          this.search = this.users;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    // logChange(event) {
    //   console.log(event);
    // },
    toDetail(id) {
      console.log(`"detail , ${id} "`);
    },
    dropdownFilter() {
      this.isOpenFilter = !this.isOpenFilter;
    },
    chooseFilter(param) {
      console.log(param);
      if (param === "Ascending") {
        this.search = this.search.sort(
          (a, b) =>
            parseInt(a.createdAt.split("-").join("")) -
            parseInt(b.createdAt.split("-").join(""))
        );
      } else if (param === "Descending") {
        this.search = this.search.sort(
          (a, b) =>
            parseInt(b.createdAt.split("-").join("")) -
            parseInt(a.createdAt.split("-").join(""))
        );
      } else {
        console.log(param);
      }
    },
    getKeywords() {
      this.search = this.users.forEach((user) => {
        console.log(user);
        // let filterId =
        //   user.orderId.includes(this.searchKey) ||
        //   user.email.includes(this.searchKey);
        return user.email.includes(this.searchKey);
      });
    },
  },
};
</script>

<style>
.sidenav {
  height: 100%;
  width: 150px;
  position: fixed;
  z-index: 1;
  left: 0;
  background-color: #6be1c9;
  overflow-x: hidden;
  padding-top: 20px;
}

.sidenav a {
  padding: 6px 8px 6px 16px;
  text-decoration: none;
  font-size: 24px;
  color: white;
}

.sidenav a:hover {
  color: black;
}

.main {
  margin-left: 150px; /* Same as the width of the sidenav */
  padding: 0px 20px 0px 0px;
}

.padding-body {
  display: flex;
  justify-content: space-between;
  padding: 0px 20px;
  margin: 25px 0px;
}
</style>
