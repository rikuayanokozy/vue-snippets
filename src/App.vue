<template>
  <h3>Welcome to my vue snippets</h3>
  <hr>
  <h4>Countdown Button</h4>
  <countdown-btn :interval="30" :onclick="countDownBtnClick" :onfinish="countDownFinish"></countdown-btn>
  <span>Status: {{countDownBtnStatus}}</span>
  <hr>
  <h4>Dialog</h4>
  <button type="button" @click="showDialog1=true">Show</button>
  <button type="button" @click="showDialog2=true">Show dialog with custom footer</button>
  <dialog :title="'I\'m dialog'" :show.sync="showDialog1">
    <template slot="content">
      hello world.
    </template>
  </dialog>
  <dialog :title="'Dialog with custom footer'" :show.sync="showDialog2">
    <template slot="content">assign your custom footer to slot "footer".</template>
    <div slot="footer">
      <a href="#" class="btn btn-primary" @click.prevent="showDialog2=false">Okay, I know</a>
      <a href="#" class="btn" @click.prevent="showDialog2=false">Close</a>
    </div>
  </dialog>
</template>
<script>
import CountdownButton from './components/countdown-btn';
import Dialog from './components/dialog';

export default {
  data: () => ({
    countDownBtnStatus: 'available',
    showDialog1: false,
    showDialog2: false,
  }),
  components: {
    Dialog,
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
<style>
@import './app.css';
</style>