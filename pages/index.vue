<template>
  <div>
    <navbar />
    <div class="container-main">
      <div class="sidenav">
        <nuxt-link to="/">Order List</nuxt-link>
      </div>
      <div class="main">
        <h2 style="padding: 20px">Order List</h2>
        <div class="padding-body">
          <div>
            <input
              type="text"
              placeholder="search user name"
              style="padding: 0.25rem 0.75rem"
              v-model="searchKey"
              @keyup.enter="getCurrentPage()"
            />
            <Button content="Submit" @click="getCurrentPage()" />
          </div>

          <div>
            <Dropdown
              @click="dropdownFilterProvider"
              :listDropdown="listProvider"
              :choosedList="filterProvide"
              :isOpen="isOpenProvider"
              @click-list="chooseFilterProvider"
            />

            <Dropdown
              @click="dropdownFilter"
              :listDropdown="listDropdown"
              :choosedList="filter"
              :isOpen="isOpenFilter"
              @click-list="chooseFilter"
            />
          </div>
        </div>

        <div @click="toDetail(user)" v-for="(user, id) in search" :key="id">
          <CardItem :userInfo="user" />
        </div>

        <div style="float: right">
          <button
            type="button"
            class="page-link"
            v-if="page != 1"
            @click="page--"
          >
            Previous
          </button>

          <button
            :class="{ active: page === item }"
            @click="page = item"
            v-for="(item, id) in pages"
            :key="'a' + id"
          >
            {{ item }}
          </button>

          <button
            type="button"
            @click="page++"
            v-if="page < pages.length"
            class="page-link"
          >
            Next
          </button>
        </div>

        <Detail
          class="container-detail"
          :isShowDetail="isShowDetail"
          :userInfo="detailUser"
          @close-card="closeCard"
        />
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
import Detail from "../components/Detail.vue";
export default {
  components: { Navbar, CardItem, Button, Dropdown, Detail },
  name: "IndexPage",
  data() {
    return {
      isShowDetail: false,
      detailUser: {},
      users: [],
      search: [],
      allUser: [],
      searchKey: "",
      value: "",
      filter: "Sort",
      filterProvide: "Filter Provider",
      isOpenFilter: false,
      isOpenProvider: false,
      listDropdown: ["Ascending", "Descending"],
      listProvider: [
        "Canva",
        "Youtube",
        "Nintendo Switch",
        "Netflix",
        "Apple One",
      ],
      page: 1,
      perPage: 5,
      pages: [],
    };
  },
  watch: {
    choosedList() {
      this.value = this.choosedList;
    },
    page() {
      this.getCurrentPage();
    },
  },
  mounted() {
    this.getDataUser();
  },
  methods: {
    getDataUser() {
      axios
        // .get("http://demo2378145.mockable.io/seakun-intern-fe")
        .get("https://mocki.io/v1/a6f0c63f-5e71-4876-94f7-2131aaf1edaa")
        .then((res) => {
          this.users = res.data.data;
          this.getCurrentPage();
          this.setPages(this.users);
          console.log(this.pages);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toDetail(user) {
      this.detailUser = user;
      this.isShowDetail = true;
      console.log(this.isShowDetail);
      console.log(user);
    },
    dropdownFilter() {
      this.isOpenFilter = !this.isOpenFilter;
    },
    dropdownFilterProvider() {
      this.isOpenProvider = !this.isOpenProvider;
    },
    chooseFilter(param) {
      console.log(param);
      if (param === "Ascending") {
        this.isOpenFilter = false;
        this.search = this.search.sort(
          (a, b) =>
            parseInt(a.createdAt.split("-").join("")) -
            parseInt(b.createdAt.split("-").join(""))
        );
      } else if (param === "Descending") {
        this.isOpenFilter = false;
        this.search = this.search.sort(
          (a, b) =>
            parseInt(b.createdAt.split("-").join("")) -
            parseInt(a.createdAt.split("-").join(""))
        );
      } else {
        console.log(param);
      }
    },
    chooseFilterProvider(param) {
      console.log(param);
      if (param === "Canva") {
        this.page = 1;
        this.search = [];
        this.isOpenProvider = false;
        this.search = this.users.filter((user) => {
          return user.provider.name.match("Canva");
        });
        this.setPages(this.search);
      } else if (param === "Youtube") {
        this.page = 1;
        this.search = [];
        this.isOpenProvider = false;
        this.search = this.users.filter((user) => {
          return user.provider.name.match("Youtube");
        });
        this.setPages(this.search);
      } else if (param === "Nintendo Switch") {
        this.page = 1;
        this.search = [];
        this.isOpenProvider = false;
        this.search = this.users.filter((user) => {
          return user.provider.name.match("Nintendo Switch");
        });
        this.setPages(this.search);
      } else if (param === "Netflix") {
        this.page = 1;
        this.search = [];
        this.isOpenProvider = false;
        this.search = this.users.filter((user) => {
          return user.provider.name.match("Netflix");
        });
        this.setPages(this.search);
      } else if (param === "Apple One") {
        this.page = 1;
        this.search = [];
        this.isOpenProvider = false;
        this.search = this.users.filter((user) => {
          return user.provider.name.match("Apple One");
        });
        this.setPages(this.search);
      } else {
        console.log(param);
      }
    },

    closeCard() {
      this.isShowDetail = !this.isShowDetail;
    },
    getCurrentPage() {
      if (this.searchKey) {
        this.page = 1;
        this.search = [];
        this.search = this.users.filter((user) => {
          return (
            user.user.name.match(this.searchKey) ||
            user.user.email.match(this.searchKey) ||
            user.orderId.match(this.searchKey)
          );
        });
        this.setPages(this.search);
      } else {
        this.search = [];
        let page = this.page;
        let perPage = this.perPage;
        let from = page * perPage - perPage;
        let to = page * perPage;
        this.search = this.users.slice(from, to);

        this.setPages(this.users);
      }
    },
    setPages(user) {
      this.pages = [];
      let numberOfPages = Math.ceil(user.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
  },
};
</script>

<style>
.active {
  background-color: greenyellow;
}
button.page-link {
  display: inline-block;
}
.container-main {
  display: flex;
}
.container-detail {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-height: 95%;
  max-width: 95%;
  min-width: 20rem;
  width: 60%;
}
.sidenav {
  border-style: solid none solid none;
  border: 2px solid #f0f7f6;
  position: sticky;
  top: 0;
  left: 0;
  height: 95vh;
  width: 10%;
  background-color: #6ca2ce;
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
  width: 90%;
  padding: 20px 10px;
  background-color: #5fb5fe;
}

.padding-body {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0px 20px;
  margin: 25px 0px;
}
</style>
