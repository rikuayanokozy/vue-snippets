<template>
  <h3>Welcome to my vue snippets</h3>
  <hr>
  <h4>Countdown Button</h4>
  <countdown-btn :interval="30" :onclick="countDownBtnClick" :onfinish="countDownFinish"></countdown-btn>
  <span>Status: {{countDownBtnStatus}}</span>
</template>
<script>
import CountdownButton from './components/countdown-btn';

export default {
  data: () => ({
    countDownBtnStatus: 'available',
  }),
  components: {
    'countdown-btn': CountdownButton,
  },
  methods: {
    countDownBtnClick() {
      this.countDownBtnStatus = 'clicked';
    },
    countDownFinish() {
      this.countDownBtnStatus = 'available';
    },
  },
};
</script>
