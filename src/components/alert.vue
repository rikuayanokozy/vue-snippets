<template>
  <div :class="className">
    <strong v-if="title">{{title}}</strong>
    <slot>{{message}}</slot>
  </div>
</template>
<script>
export default {
  props: {
    type: {
      type: String,
      default: 'info',
    },
    title: String,
    message: String,
  },
  computed: {
    className() {
      let type = this.type;
      switch (type) {
        case 'info':
        case 'error':
        case 'warning':
        case 'success':
          break;
        default:
          type = 'info';
      }
      return `alert alert-${type}`;
    },
  },
};
</script>
<style scoped>
/* from bootstrap */
.alert {
  padding: 10px 15px;
  border: 1px solid transparent;
  border-radius: 4px;
  margin-bottom: 10px;
}
.alert-error {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.alert-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.alert-info {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.alert-success {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
</style>

