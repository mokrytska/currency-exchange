<template>
  <div
    class="switch_path"
    :class="{switch_path_active: value}"
    @click="$emit('input', !value)"
  >
    <div class="switch_handle" :class="{switch_handle_active: value}"></div>
  </div>
</template>

<script>
export default {
  props: {
    value: Boolean,
  },
};
</script>
<style scoped>
.switch_path {
  width: 40px;
  height: 20px;
  border-radius: 10px;
  border: 1px solid grey;
  background-color: #ccc;
  cursor: pointer;
}

.switch_handle {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  transition: all 0.3s ease-in-out;
  background: #999;
}

.switch_path_active {
  background: rgb(137, 137, 235);
}
.switch_handle_active {
  transform: translateX(20px);
  background: blue;
}
</style>
