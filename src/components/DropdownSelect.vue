<template>
  <div
    class="dropdown-container"
    :class="{ opened: isOpen }"
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
        :class="{ rotate: isOpen }"
        src="../assets/chevron-down.svg"
      >
    </span>

    <div
      v-show="isOpen"
      class="dropdown-items-container"
    >
      <div
        v-for="(item, index) in items" :key="index"
        class="dropdown-item"
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
  max-height: 56px;
  transition: max-height .25s;
}

.closed-dropdown-text {
  font-size: 16px;
  line-height: 24px;
  color: #A0AEC0;
}

.chevron-icon {
  margin-top: 9px;
}

.dropdown-container.opened {
  max-height: 284px;
  cursor: default;
}

.dropdown-items-container {
  padding-top: 24px;
}

.dropdown-item {
  font-size: 14px;
  line-height: 24px;
  font-weight: 600;
}

.dropdown-item:hover {
  cursor: pointer;
  color: #4299E1;
}

.dropdown-item:not(:last-child) {
  margin-bottom: 12px;
}

.chevron-icon {
  transition: .25s;
}

.chevron-icon.rotate {
  transform: rotate(180deg);
}
</style>
