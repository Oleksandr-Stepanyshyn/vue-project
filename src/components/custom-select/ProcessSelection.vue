<template>
  <form class="select">
    <div class="select__title" :style="{ backgroundColor: title.color, borderColor: title.color }" @click="openOptions"
      data-action="open">
      <input class="custom-checkbox" name="checkbox" :style="{ borderColor: title.color }" type="checkbox"
        v-if="showCheckbox" v-bind:checked="title.checked" @change="changeCheckbox" />
      <p class="title--active" type="select" data-action="open">{{ title.label }}</p>
    </div>
    <OptionList v-if="areOptionsVisible" :options="options" @select-option="selected" @close-option="closeOptions" />
  </form>
</template>

<script>

import OptionList from "@/components/custom-select/OptionList.vue"

export default {
  name: "process-selection",
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
      areOptionsVisible: false,
      title: this.select,
    }
  },
  methods: {
    toggleSelectVisible() {
      this.areOptionsVisible = !this.areOptionsVisible;
    },
    openOptions(e) {
      if (e.target.type === "checkbox") {
        return;
      }
      this.toggleSelectVisible();
      // document.addEventListener("click", this.hideSelect.bind(this), true);
    },
    closeOptions() {
      console.log("closeOptions");
      this.areOptionsVisible = false;
      // document.removeEventListener("click", this.hideSelect);
    },
    selected(option) {
      this.title = option;
      this.toggleSelectVisible();
      this.$emit("select", option);
    },
    changeCheckbox(e) {
      this.$emit("checkbox-checked", e.target.checked)
    },
   
    // hideSelect(e) {
    //   console.log(e.target);
    //   console.log(e.target.dataset.action);
    //   if (e.target.dataset.action === "open" || e.target.type === "option") {
    //     console.log("option");
    //     return;
    //   }
    //   this.areOptionsVisible = false;
    //   console.log("end");
    //   this.closeOptions();
    //   return; 
    // },
    
  },
  // mounted() {
  //   document.addEventListener("click", this.hideSelect.bind(this), true);
  // },
  // beforeDestroy() {
  //   document.removeEventListener(this.hideSelect);
  // }
  components: {
    OptionList
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

.custom-checkbox {
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


</style>