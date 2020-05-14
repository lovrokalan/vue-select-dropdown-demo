<template>
  <div
    class="dropdown-container"
    :class="{ opened: isOpen }"
    @click="openDropdown"
    v-clickoutside="closeDropdown"
  >

    <!-- closed dropdown text or input -->
    <span v-show="!isOpen">
      <span
        v-if="!value"
        class="closed-dropdown-text"
      >
        Select an item
      </span>
      <span
        v-else
        class="closed-dropdown-text selected-value-text"
      >
        {{value}}
      </span>
    </span>
    <span v-show="isOpen">
      <input
        v-model="searchText"
        ref="search"
        type="text"
        :placeholder="searchInputPlaceholderText"
        class="search-dropdown-input"
      >
    </span>

    <!-- chevron icon -->
    <span
      class="cursor-pointer z-1"
      @click.stop="isOpen ? closeDropdown() : openDropdown()"
    >
      <img
        class="float-right chevron-icon"
        :class="{ rotate: isOpen }"
        src="../assets/chevron-down.svg"
      >
    </span>

    <!-- extended dropdown -->
    <transition name="height-slide">
    <div
      v-if="isOpen"
      class="dropdown-items-container overflow-auto"
    >
      <div v-if="filteredItems.length > 0">
        <div
          v-for="(item, index) in filteredItems" :key="index"
          class="dropdown-item clickable"
          @click.stop="handleItemSelect(item)"
        >
          {{item}}
        </div>
      </div>
      <div
        v-else
        class="dropdown-item empty-list-msg"
      >
        No items were found.
      </div>
    </div>
    </transition>

  </div>
</template>

<script>
export default {
  name: 'DropdownSelect',
  props: {
    value: {
      type: String,
      default: ''
    },
    items: {
      type: Array,
      required: true
    },
    searchInputPlaceholderText: {
      type: String,
      default: 'This is a search input'
    },
    focusInputOnOpen: { // passing false is recommended for mobile devices
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      isOpen: false,
      searchText: ''
    }
  },
  computed: {
    filteredItems() {
      return this.items.filter(itemValue => itemValue.toLowerCase().includes(this.searchText))
    }
  },
  methods: {
    openDropdown() {
      this.isOpen = true
      if (this.focusInputOnOpen) {
        this.$nextTick(() => { //nextTick makes sure the search input is focused after it is displayed in the DOM
          this.$refs.search.focus()
        })
      }
    },
    closeDropdown() {
      this.isOpen = false
      this.searchText = ''
    },
    handleItemSelect(itemValue) {
      this.$emit('input', itemValue)
      this.closeDropdown()
    }
  },
  directives: {
    clickoutside: {
      bind: function (el, binding, vnode) {
        el.eventOnClick = function (event) {
            if (!el.contains(event.target)) {
                // call method provided in the attribute value
                vnode.context[binding.expression](event)
            }
        };
        // add click and touchend event listeners
        document.addEventListener('click', el.eventOnClick)
        document.addEventListener('touchend', el.eventOnClick)
      },
      unbind: function (el) {
        // remove eventListener once an element with this directive is removed from the DOM
        document.removeEventListener('click', el.eventOnClick)
        document.removeEventListener('touchend', el.eventOnClick)
      }
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
  margin-top: 24px;
  transform-origin: top;
  max-height: 204px;
  margin-right: 6px;
}

.dropdown-item {
  font-size: 14px;
  line-height: 24px;
  font-weight: 600;
  color: #1A202C;
}

.dropdown-item.clickable:hover {
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
  -webkit-transform: rotate(180deg);
  -moz-transform: rotate(180deg);
  transform: rotate(180deg);
  /* changing svg fill color with a filter: */
  filter: brightness(0) saturate(100%) invert(15%) sepia(13%) saturate(570%) hue-rotate(138deg) brightness(93%) contrast(93%);
  -webkit-filter: brightness(0) saturate(100%) invert(15%) sepia(13%) saturate(570%) hue-rotate(138deg) brightness(93%) contrast(93%);
  -moz-filter: brightness(0) saturate(100%) invert(15%) sepia(13%) saturate(570%) hue-rotate(138deg) brightness(93%) contrast(93%);
}

.search-dropdown-input {
  outline: none;
  height: 24px;
  width: calc(100% - 30px);
  font-size: 16px;
  color: #1A202C;
}

.empty-list-msg {
  color: #A0AEC0;
}

/* vue transition styles: */
.height-slide-enter-active {
  transition: transform .25s;
}

.height-slide-enter {
  -webkit-transform: scaleY(0);
  -moz-transform: scaleY(0);
  transform: scaleY(0);
}
</style>
