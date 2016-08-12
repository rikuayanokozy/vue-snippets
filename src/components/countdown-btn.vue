<template>
  <button :disabled="countDownSecs||disabled" @click="click">
    <template v-if="countDownSecs">Resend after {{countDownSecs}}</template>
    <template v-else>Send</template>
  </button>
</template>
<script>
export default {
  data: () => ({
    countDownSecs: 0,
  }),
  props: {
    disabled: {
      type: Boolean,
      default: false,
    },
    interval: {
      type: Number,
      required: true,
    },
    onclick: Function,
    onfinish: Function,
  },
  methods: {
    click() {
      if (this.countDownSecs) return;
      this.countDownSecs = this.interval;
      setTimeout(this.countDown.bind(this), 1000);
      if (this.onclick) {
        this.onclick();
      }
    },
    countDown() {
      if (--this.countDownSecs) {
        setTimeout(this.countDown.bind(this), 1000);
      } else {
        this.onfinish();
      }
    },
  },
};
</script>
