<template>
  <button
    :disabled="smsState.disabled"
    @tap="onClick"
    type="warn"
  >{{ smsState.text }}
  </button>
</template>

<script>
import {reactive, ref} from 'vue'
import './index.scss'

export default {
  name: 'page-index',
  setup() {
    const smsState = reactive({
      text: '发送验证码',
      disabled: false
    });

    const onClick = () => {
      let second = 60;
      smsState.text = `${second}s`;
      smsState.disabled = true;

      let interval = setInterval(() => {

        if (second-- > 1) {
          smsState.text = `${second}s`;

        } else {
          smsState.text = `发送验证码`;
          smsState.disabled = false;
          clearInterval(interval);
        }
      }, 1000);
    };

    return {
      onClick,
      smsState
    }
  }
}
</script>
