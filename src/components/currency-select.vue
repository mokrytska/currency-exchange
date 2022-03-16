<template>
  <div class="wrapper">
    <div class="select border">
      <div >{{ value }}</div>
      <div @click="isVisible = !isVisible" class="arrow">
        <span class="material-icons"> expand_more </span>
      </div>
    </div>
    <div class="back_drop" v-if="isVisible"></div>
    <div class="currency_list" v-if="isVisible">
      <template v-for="item in currencyItems">
        <div
          :class="{item_selected: value === item}"
          class="item"
          v-bind:key="item"
          @click="
            isVisible = false;
            $emit('input', item);
          "
        >
          {{ item }}
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currencyItems: Array,
    value: String,
  },

  data() {
    return {
      isVisible: false,
    };
  },
};
</script>

<style scoped>
.wrapper {
  position: relative;
}
.select {
  padding-left: 15px;
  height: 35px;
  text-align: center;
  display: flex;
  line-height: 30px;
  justify-content: space-between;
}
.arrow {
  cursor: pointer;
  margin: 5px;
  position: absolute;
  right: 5px;
}
.back_drop {
  background: white;
  opacity: 0.5;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.item {
  padding-left: 15px;
  width: 165px;
  background: white;
}
.item:hover {
  background: rgb(23, 185, 235);
}
.item_selected {
  background: rgb(23, 185, 235);
}
.currency_list {
  position: absolute;
  top: 40px;
  z-index: 2;
  border-radius: 10px;
  cursor: pointer;
  border: 0.5px solid black;
  overflow-y: scroll;
  height: 300px;
  background: white;
}
</style>
