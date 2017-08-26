<template>
  <transition name="vodal-fade">
    <div v-show="show" tabindex="-1" :style="style" class="vodal" @keyup.esc="show && $emit('hide')">
      <div class="vodal-mask" v-if="mask" @click="$emit('hide')" />
      <transition :name="`vodal-${animation}`">
        <div class="vodal-dialog" :class="[className]"  v-show="show">
          <span class="vodal-close" v-if="closeButton" @click="$emit('hide')" />
          <slot></slot>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'vodal',

  props: {
    show: {
      type: Boolean,
      required: true
    },
    width: {
      type: Number,
      default: 400
    },
    height: {
      type: Number,
      default: 240
    },
    duration: {
      type: Number,
      default: 300
    },
    measure: {
      type: String,
      default: 'px'
    },
    animation: {
      type: String,
      default: 'zoom'
    },
    mask: {
      type: Boolean,
      default: true
    },
    closeButton: {
      type: Boolean,
      default: true
    },
    className: {
      type: String,
      default: ''
    }
  },

  computed: {
    style() {
      return {
        animationDuration: `${this.duration}ms`
      };
    },
  },

  watch: {
    show(show) {
      show && this.$nextTick(() => {
        this.$el.focus();
      })
    }
  }
}
</script>

<style>
.vodal-dialog {
  width: 90%;
  max-height: 70%;
}

@media (min-width: 768px) {
  .vodal-dialog {
    width: 600px;
  }
  .vodal-sm {
      width: 400px;
  }
}
@media (min-width: 992px) {
  .vodal-lg {
      width: 900px;
  }
}

.vodal-content{
  max-height: calc(100% - 20px);
  overflow: auto;
  margin-top: 20px;
}

</style>
