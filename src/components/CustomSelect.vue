<template>
  <!-- <h2>Custom select</h2> -->
  <div class="custom-select">
    <p 
      class="title"
      @click="areOptionsVisible = !areOptionsVisible"
    >
      {{selected.label}}
    </p>
    <div 
      class="options"
      v-if="areOptionsVisible"
    >
      <p 
        v-for="option in options" 
        :key="option.id"
        @click="selectOption(option)"
      >
        {{option.label}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'custom-select',
  props: {
    options: {
      type: Array,
      default() {
        return [];
      }
    },
    selected: {
      type: Object,
      require: true,
    }
  },
  data() {
    return {
      areOptionsVisible: false,
    }
  },
  methods: {
    selectOption(option) {
      console.log('hello')
      this.$emit("select", option);
      this.areOptionsVisible = false;
    },
    hideSelect() {
      this.areOptionsVisible = false;
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true);
  },
  beforeDestroy() {
    document.removeEventListener(this.hideSelect);
  }
  }
</script>

<style scoped>
  .custom-select {
    position: relative;
    width: 200px;
    cursor: pointer;
  }
  .custom-select p{
    margin: 0;
  }

  .title {
    border: 1px solid #aeaeae;
  }
  .options {
    border: 1px solid #aeaeae;
    position: absolute;
    top: 30px;
    right: 0;
    width: 100%;
  }

  .options p:hover {
    background-color: #e7e7e7;
  }
</style>