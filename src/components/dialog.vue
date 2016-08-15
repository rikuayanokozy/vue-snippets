<template>
  <div class="dialog-backdrop" v-if="show" @click="show=false" @keypress.27="show=false">
    <div class="dialog" @click.stop>
      <div class="dialog-title">
        <span class="dialog-close-button" @click="show=false" v-if="closeBtn">&times;</span>
        {{title}}
      </div>
      <div class="dialog-content">
        <slot name="content">{{content}}</slot>
      </div>
      <div class="dialog-footer text-right">
        <slot name="footer">
          <a href="#" class="btn btn-primary" @click.prevent="show=false">OK</a>
        </slot>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    show: {
      type: Boolean,
      twoWay: true,
    },
    title: String,
    content: String,
    closeBtn: {
      type: Boolean,
      default: true,
    },
  },
  watch: {
    show(next) {
      const escHandler = e => {
        if (e.keyCode === 27) {
          this.$set('show', false);
        }
      };
      if (next) {
        document.body.addEventListener('keydown', escHandler);
      } else {
        document.body.removeEventListener('keydown', escHandler);
      }
    },
  },
};
</script>
<style scoped>
.dialog-backdrop {
  display: flex;
  justify-content: center;
  -webkit-justify-content: center;
  align-items: center;
  -webkit-align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, .8);
}
.dialog {
  background: #fff;
  border: 1px solid #dcdcdc;
  box-shadow: 0 2px 3px rgba(100,100,100,.27);
  border-radius: 3px;
  min-width: 320px;
  max-width: 500px;
}
  .dialog-title, .dialog-content, .dialog-footer {
    padding: 15px 30px;
  }
  .dialog-title {
    height: 30px;
    line-height: 30px;
    font-size: 16px;
    border-bottom: 1px solid #dcdcdc;
  }
    .dialog-close-button {
      cursor: pointer;
      float: right;
      margin-right: -5px;
      font-size: 20px;
      height: 30px;
      line-height: 30px;
    }
  .dialog-footer {
    background: #fafafa;
  }
    .dialog-footer a.btn {
      font-size: 14px;
      margin-right: 10px;
    }
    .dialog-footer.text-right a.btn {
      margin-left: 10px;
      margin-right: 0;
    }
    .dialog-footer a.btn.left {
      margin-left: 0;
    }
.text-right {
  text-align: right;
}
</style>
