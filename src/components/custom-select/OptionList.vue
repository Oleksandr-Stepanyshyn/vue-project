<template>
  <ul class="select__list">
    <li class="select__item" name="option" type="option" v-for="option in options" :key="option.id"
      @click="selectOption(option)">
      <span class="item__color" :style="{ backgroundColor: option.color }"></span>
      {{ option.label }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "options-list",
  props: {
    options: {
      type: Array,
      required: true
    },
  },
  methods: {
    selectOption(option) {
      this.$emit("select-option", option)
    },
    hideOptions(e) {
      if (e.target.dataset.action === "open" || e.target.type === "option") {
        return;
      }
      this.$emit("close-option", false)
    }
  },
  mounted() {
    document.addEventListener("click", this.hideOptions);
  },
  beforeDestroy() {
    document.removeEventListener("click", this.hideOptions);
  }
  }
</script>

<style scoped>
.select__list {
  width: 200px;
  position: absolute;
  border: 1px solid gray;
  border-left: 3px solid gray;
  /* opacity: 0;
  pointer-events: none; */
  z-index: 12;
  background-color: #fff;
}

.select__list.open {
  opacity: 1;
  pointer-events: all;
}

.select__item {
  display: flex;
  position: relative;
  padding: 8px;
  padding-left: 56px;
  cursor: pointer;

}

.select__item:hover,
.select__item:focus {
  background-color: #5ee2ff;
}

.select__item:not(:first-child) {
  /* margin-top: 12px; */
}

.item__color::before {
  content: "";
  position: absolute;
  /* display: block; */
  left: 24px;
  top: 50%;
  transform: translateY(-50%);
  width: 12px;
  height: 12px;
  background-color: inherit;
}
</style>