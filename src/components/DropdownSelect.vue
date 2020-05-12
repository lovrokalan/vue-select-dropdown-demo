<template>
  <div class="dropdown-container">
    <span
      class="closed-dropdown-text"
    >
      Select an item
    </span>

    <div
      class="inline cursor-pointer z-1"
    >
      <img
        class="float-right chevron-icon"
        src="../assets/chevron-down.svg"
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'DropdownSelect',
  props: {
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
