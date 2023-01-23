<template>
  <div class="container-dropdown">
    <div style="position: relative; width: 100%">
      <div class="">
        <button
          @click="$emit('click')"
          type="button"
          class="container-dropdown"
          id="menu-button"
          aria-expanded="true"
          aria-haspopup="true"
        >
          {{ choosedList }}
          <svg
            style="height: 20px; width: 20px"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
            aria-hidden="true"
          >
            <path
              fill-rule="evenodd"
              d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
      </div>

      <div v-if="isOpen" class="content-dropdown">
        <div style="padding: 0px 2px">
          <div v-for="(item, id) in listDropdown" :key="id">
            <p style="color: gray" @click="$emit('click-list', item, id)">
              {{ item }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    choosedList: {
      type: String,
      default: "Sort",
    },
    isOpen: {
      type: Boolean,
      default: false,
    },
    listDropdown: {
      type: Array,
      default: [],
    },
    error: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      value: "",
    };
  },
  watch: {
    choosedList() {
      this.value = this.choosedList;
    },
  },
};
</script>

<style>
.container-dropdown {
  display: inline-flex;
  justify-content: space-between;
  align-items: center;
  width: 200px;
  padding: 0.25rem 0.75rem;
  font-size: 5 rem;
  font-weight: 700;
  color: #6c7fe1;
}

.content-dropdown {
  transform-origin: top right;
  position: absolute;
  left: 0;
  width: 100%;
  background-color: white;
  border: 1px solid black;
  font-size: 14px;
  padding: 0px 10px;
  line-height: 20px;
}

p:hover {
  cursor: pointer;
}
</style>
