<template>
  <div class="star-rating">
    <label
      class="star-rating star"
      v-for="r in maxStar"
      :key="r"
      :class="{ on: (hover > 0 ? hover : value) >= r, disabled: disabled }"
      @mouseover="onHover(r)"
      @mouseout="onHover(0)"
    >
      <input
        class="star-rating checkbox"
        type="radio"
        :value="r"
        :disabled="disabled || readOnly"
        v-model="compValue"
      />
      ★
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Number,
      default: 0
    },
    disabled: {
      type: Boolean,
      default: false
    },
    readOnly: {
      type: Boolean,
      default: false
    },
    maxStar: {
      type: Number,
      default: 5
    }
  },
  computed: {
    compValue: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  },
  data() {
    return {
      hover: 0
    }
  },
  methods: {
    onHover(num) {
      if (this.disabled || this.readOnly) {
        return
      }
      this.hover = num
    }
  }
}
</script>

<style scoped>
.star-rating {
  user-select: none;
}
.star-rating.checkbox {
  position: absolute;
  overflow: hidden;
  clip: rect(0 0 0 0);
  padding: 0;
  border: 0;
}

.star-rating.star {
  display: inline-block;
  padding: 3px;
  vertical-align: middle;
  line-height: 1;
  font-size: 1.5em;
  color: #ababab;
  transition: color 0.2s ease-out;
}
.star-rating.star:hover {
  cursor: pointer;
}
.star-rating.star.on {
  color: #ffd700;
}
.star-rating.star.disabled {
  opacity: 0.5;
}
</style>
