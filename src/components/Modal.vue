<template lang="html">
  <transition name="z-modal-expand">
    <div class="z-supernatant" v-show="show">
      <div class="z-modal-wrapper">
        <div class="z-modal">
          <div class="z-modal-title">
            {{title}}
          </div>
          <div class="z-modal-content">
            {{content}}
          </div>
          <div class="z-modal-footer">
            <a class="z-btn-modal" @click="cancelFunc" v-if="type=='confirm'">{{cancel}}</a>
            <a class="z-btn-modal" :class="{'z-btn-modal-sure': type=='confirm'}" @click="sureFunc">{{sure}}</a>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'z-modal',
  props: {
    sure: {
      type: String,
      default: "确定"
    },
    cancel: {
      type: String,
      default: "取消"
    },
    show: {
      type: Boolean,
      required: true
    },
    title: {
      type: String,
      default: "提示"
    },
    content: {
      type: String,
      required: true
    },
    type: {
      type: String,
      default: "alert"
    },
    sureEvent: {
      type: Function,
      default: function() {
        console.log("点击了确定")
      }
    },
    cancelEvent: {
      type: Function,
      default: function() {
        console.log("点击了取消")
      }
    }
  },
  methods: {
    sureFunc: function() {
      this.$emit("close-modal")
      this.sureEvent()
    },
    cancelFunc: function() {
      this.$emit("close-modal")
      this.cancelEvent()
    }
  }
};
</script>

<style lang="css" scoped>
  .z-supernatant {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
    display: table;
    transition: opacity .3s ease;
  }

  .z-modal-wrapper {
    display: table-cell;
    vertical-align: middle;
  }

  .z-modal {
    width: 300px;
    margin: 0px auto;
    background-color: #fff;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
    transition: all .3s ease;
  }

  .z-modal-expand-enter, .z-modal-expand-leave-active {
    opacity: 0;
  }

  .z-modal-expand-enter .z-modal, .z-modal-expand-leave-active .z-modal{
    -webkit-transform: scale(0.5);
    transform: scale(0.5);
  }

  .z-modal-title {
    line-height: 44px;
    text-align: center;
  }

  .z-modal-content {
    padding: 0 12px 12px;
    text-align: left;
  }

  .z-modal-footer {
    border-top: 1px solid #ccc;
    display: table;
    width: 100%;
  }

  .z-btn-modal {
    display: table-cell;
    text-align: center;
    cursor: pointer;
    line-height: 44px;
  }

  .z-btn-modal:nth-child(2) {
    border-left: 1px solid #ccc;
  }

  .z-btn-modal-sure {
    background-color: rgb(65, 184, 131);
    color: #fff;
  }
</style>
