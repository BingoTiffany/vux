<template>
  <a href="javascript:;" class="weui-grid" @click="onClick" :style="style">
    <div class="weui-grid__icon" v-if="hasIconSlot || icon">
      <slot name="icon"><img :src="icon" alt=""></slot>
    </div>
    <p v-if="hasLabelSlot || label" class="weui-grid__label">
      <slot name="label">
        <span v-html="label"></span>
      </slot>
    </p>
    <slot></slot>
   </a>
</template>

<script>
import { go } from '../../libs/router'

export default {
  props: ['icon', 'label', 'link'],
  mounted () {
    this.$slots.icon && (this.hasIconSlot = true)
    this.$slots.label && (this.hasLabelSlot = true)
  },
  computed: {
    style () {
      const rows = this.$parent.rows
      if (!rows || rows === 3) {
        return
      }
      const styles = {}
      styles.width = `${100 / rows}%`
      return styles
    }
  },
  methods: {
    onClick () {
      this.$emit('on-item-click')
      go(this.link, this.$router)
    }
  },
  data () {
    return {
      hasIconSlot: false,
      hasLabelSlot: false
    }
  }
}
</script>
