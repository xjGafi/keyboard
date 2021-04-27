<template>
  <div class="container" id="app">
    <!-- input start -->
    <div class="input">
      <input
        v-model="word"
        type="text"
        ref="input"
        placeholder="Text input"
        @focus="showKeyboard"
        :data-layout="layout"
      />
      <p class="question">
        "Wonderful! I'll
        <b @click="inputFocus()">
          <span
            v-for="(letter, index) in answer"
            :key="index"
            class="letter"
            :class="{ success: help || answer[index] === word[index] }"
            >{{ help ? answer[index] : word[index] }}
          </span>
        </b>
        packing our suitcases."
      </p>
    </div>
    <!-- input end -->

    <!-- operate start -->
    <div class="operate" :class="{ visible: visible }">
      <div class="header">
        <span
          class="help"
          :class="{ closed: help }"
          @click="help ? hideHelp() : showHelp()"
        ></span>
        <span class="count">1 / 10</span>
        <span class="tips"></span>
      </div>
      <keyboard
        ref="keyboard"
        :options="options"
        :layout="layout"
        :cancel="hideKeyboard"
        :input="input"
      ></keyboard>
    </div>
    <!-- operate end -->
  </div>
</template>

<script>
  import keyboard from './components/keyboard';

  export default {
    name: 'App',
    components: {
      keyboard: keyboard
    },
    data() {
      return {
        visible: false,
        layout: 'ios',
        input: null,
        answer: 'start',
        word: '',
        help: false,
        options: {
          useKbEvents: false,
          preventClickEvent: false
        }
      };
    },

    directives: {
      focus: {
        // 指令的定义
        inserted: function(el) {
          el.focus();
        }
      }
    },

    watch: {
      word(value) {
        if (value.length <= this.answer.length) {
          value === this.answer && this.hideKeyboard();

          let index = value.length - 1;

          // 输入错误时清除字母
          value &&
            this.answer[index] !== value[index] &&
            setTimeout(() => {
              this.$refs.keyboard.clickKey('', {
                func: 'backspace',
                classes: 'control'
              });
            }, 200);
        }
      }
    },

    methods: {
      /**
       * @description: 获取输入框焦点
       * @param {*}
       * @return {*}
       */
      inputFocus() {
        this.$refs.input.dispatchEvent(new MouseEvent('focus'));
        // navigator.userAgent.match(
        //   /(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i
        // )
        //   ? this.$refs.input.dispatchEvent(new MouseEvent('focus'))
        //   : this.$refs.input.focus();
        // console.log(
        //   '🚀 ~ file: App.vue ~ line 189 ~ inputFocus ~ this.$refs.input',
        //   this.$refs.input
        // );
      },

      /**
       * @description: 显示键盘
       * @param {*} e 事件
       * @return {*}
       */
      showKeyboard(e) {
        this.input = e.target;
        this.layout = e.target.dataset.layout;

        // document.activeElement.blur();

        if (!this.visible) this.visible = true;
      },

      /**
       * @description: 隐藏键盘
       * @param {*}
       * @return {*}
       */
      hideKeyboard() {
        this.visible = false;
      },

      showHelp() {
        if (!this.help) this.help = true;
      },

      hideHelp() {
        this.help = false;
      }
    }
  };
</script>

<style lang="scss">
  $radius: 0.35rem;
  $font-color-true: yellowgreen;
  $font-color-false: red;
  $bg-color-050: #f4f4f4;
  $bg-color-100: #fff;
  $bg-color-300: #d5d6e0;
  $bg-color-600: #a5aebd;

  :root {
    font-size: 16px;
  }

  html,
  body {
    width: 100vw;
    height: 100vh;
    padding: 0;
    margin: 0;
    overflow: hidden;
    background-color: $bg-color-050;
  }

  .input {
    input {
      display: none;
      // position: absolute;
      // top: -100%;
      // left: -100%;
      // z-index: -100;
      // opacity: 0;
    }

    .question {
      .letter {
        display: inline-block;
        text-align: center;
        vertical-align: middle;
        width: 1rem;
        height: 1.5rem;
        padding: 0 0.25rem;
        margin: 0 0.2rem;
        background-color: $bg-color-300;
        border-radius: $radius;
        color: $font-color-false;

        &.success {
          color: $font-color-true;
        }
      }
    }
  }

  .operate {
    position: absolute;
    left: 0;
    right: 0;
    bottom: -100%;
    opacity: 0;
    transition: bottom 0.16s, opacity 0.16s;

    &.visible {
      opacity: 1;
      bottom: 0;
    }

    .header {
      background: $bg-color-100;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-top-left-radius: $radius * 2;
      border-top-right-radius: $radius * 2;

      span {
        min-width: 1rem;
        min-height: 1rem;
        display: inline-block;
      }

      .help {
        padding: 0.5rem;
        background-color: $bg-color-050;
        border-radius: 1rem;
        background-image: url('./assets/icon/icon-eyes-closed.svg');
        background-position: center center;
        background-repeat: no-repeat;
        background-size: 60%;

        &.closed {
          background-image: url('./assets/icon/icon-eyes-open.svg');
        }
      }

      .tips {
        padding: 0.5rem;
        background-color: $bg-color-050;
        border-radius: 1rem;
        background-image: url('./assets/icon/icon-bulb-off.svg');
        background-position: center center;
        background-repeat: no-repeat;
        background-size: 60%;
      }

      .count {
        color: $bg-color-600;
      }
    }
  }
</style>
