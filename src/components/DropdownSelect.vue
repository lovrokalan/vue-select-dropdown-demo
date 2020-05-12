<template>
  <div
    class="dropdown-container"
    @click="isOpen = true"
  >
    <span
      class="closed-dropdown-text"
    >
      Select an item
    </span>

    <span
      class="cursor-pointer z-1"
    >
      <img
        class="float-right chevron-icon"
        src="../assets/chevron-down.svg"
      >
    </span>

    <div v-show="isOpen">
      <div
        v-for="(item, index) in items" :key="index"
        class="my-4"
      >
        {{item}}
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'DropdownSelect',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      isOpen: false
    };
  }
}
</script>

<style scoped>
.dropdown-container {
  background-color: #fff;
  border-radius: 8px;
  -webkit-box-shadow: 0px 10px 15px rgba(35, 78, 82, 0.1);
  -moz-box-shadow: 0px 10px 15px rgba(35, 78, 82, 0.1);
  box-shadow: 0px 10px 15px rgba(35, 78, 82, 0.1);
  padding: 16px;
  cursor: pointer;
}

.closed-dropdown-text {
  font-size: 16px;
  line-height: 24px;
  color: #A0AEC0;
}

.chevron-icon {
  margin-top: 9px;
}
</style>
