<template>
  <div
    class="dropdown-container"
    :class="{ opened: isOpen }"
    @click="openDropdown()"
  >

    <!-- closed dropdown text or input -->
    <span v-show="!isOpen">
      <span
        v-if="!selectedItem"
        class="closed-dropdown-text"
      >
        Select an item
      </span>
      <span
        v-else
        class="closed-dropdown-text selected-value-text"
      >
        {{selectedItem}}
      </span>
    </span>
    <span v-show="isOpen">
      <input ref="search" type="text" placeholder="Search" class="search-dropdown-input">
    </span>

    <!-- chevron icon -->
    <span
      class="cursor-pointer z-1"
      @click.stop="isOpen = !isOpen"
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
        @click.stop="handleItemSelect(item)"
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
      isOpen: false,
      selectedItem: null
    };
  },
  methods: {
    openDropdown() {
      this.isOpen = true
      this.$nextTick(() => { //nextTick makes sure the search input is focused after it is displayed in the DOM
        this.$refs.search.focus()
      })
    },
    handleItemSelect(itemValue) {
      this.selectedItem = itemValue
      this.isOpen = false
    }
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

.closed-dropdown-text.selected-value-text {
  color: #1A202C;
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
  color: #1A202C;
}

.dropdown-item:hover {
  cursor: pointer;
  color: #4299E1;
}

.dropdown-item:not(:last-child) {
  margin-bottom: 12px;
}

.chevron-icon {
  transition: transform .25s;
  margin-right: 7px;
}

.chevron-icon.rotate {
  transform: rotate(180deg);
  /* changing svg fill color with a filer: */
  filter: brightness(0) saturate(100%) invert(15%) sepia(13%) saturate(570%) hue-rotate(138deg) brightness(93%) contrast(93%);
}

.search-dropdown-input {
  outline: none;
  height: 24px;
  width: calc(100% - 30px);
  font-size: 16px;
}
</style>
