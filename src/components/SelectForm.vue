<template>
  <form class="select">
    <div class="select__title" :style="{ backgroundColor: title.color, borderColor: title.color }" @click="toggleList">
      <input class="custom-checkbox" name="checkbox" :style="{ borderColor: title.color }"
        type="checkbox" v-if="showCheckbox" v-bind:checked="title.checked" @change="changeCheckbox" />
      <p class="title--active">{{title.label}}</p>
    </div>
    <ul class="select__list" @click="closeList">
      <li class="select__item" v-for="option in options" :key="option.id" @click="selected(option)">
        <span class="item__color" :style="{ backgroundColor: option.color }"></span>
        {{ option.label }}
      </li>
    </ul>
  </form>
</template>

<script>
export default {
  props: {
    select: {
      type: Object
    },
    options: {
      type: Array,
      required: true
    },
    showCheckbox: {
      type: Boolean,
    }
  },
  data() {
    return {
      title: this.select,
    }
  },
  methods: {
    toggleList(e) {
      if(e.target.type === "checkbox"){
        return;
      }
      if (e.currentTarget.nextSibling.classList.contains("open")) {
        e.currentTarget.nextSibling.classList.remove("open")
        return;
      }
      e.currentTarget.nextSibling.classList.add("open")
    },
    selected(option) {
      this.title = option;
      this.$emit("select", this.title.id);
    },
    changeCheckbox(e) {
      this.$emit("checkbox-checked", e.target.checked)
    },
    closeList(e) {
      console.log(e.currentTarget);
      e.currentTarget.classList.remove("open");
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

a {
  text-decoration: none;
  display: block;
  color: inherit;
}

h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0;
}

img {
  display: block;
  max-width: 100%;
  height: auto;
}

.select {
  width: 180px;
  margin-left: auto;
  margin-right: auto;
  position: relative;
}

.select__title {
  position: relative;
  font-style: 16px;
  text-align: start;

  line-height: 3;

  border-left: 8px solid;
  background: linear-gradient(rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.8));
}

.custom-checkbox{
  position: absolute;
  top: 45%;
  left: 4px;
  transform: translateY(-50%);
  border-color: red;
}

.custom-checkbox::before {
  content: '';
  position: absolute;
  top: -1px;
  width: 14px;
  height: 14px;

  /* border: 1px solid; */
  /* border-color: inherit; */
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  background-color: #fff;
}

.custom-checkbox:checked::before {
  background-image: url('@/images/check.png');
}

.title--active {
  margin-left: 32px;
  cursor: pointer;
}

.select__list {
  width: 200px;
  position: absolute;
  border: 1px solid gray;
  border-left: 3px solid gray;
  opacity: 0;
  pointer-events: none;
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