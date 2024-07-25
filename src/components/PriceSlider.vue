<template>
  <transition name="fade">
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label for="" class="font-weight-bold mr-2">Max</label>
        <input
          type="number"
          class="form-control mx-2"
          style="width: 60px; text-align: center"
          v-model="maxAmount"
          @change="emitUpdate"
        />
        <input
          type="range"
          class="custom-range"
          min="0"
          max="200"
          v-model="maxAmount"
          @input="emitUpdate"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: this.maximum, // initialize with prop value
    };
  },
  props: ["sliderStatus", "maximum"],
  watch: {
    maximum(newVal) {
      this.maxAmount = newVal;
    },
  },
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
  methods: {
    emitUpdate: function () {
      this.$emit("update-maximum", Number(this.maxAmount));
    },
  },
};
</script>
