<template>
  <path @mouseenter="isHovering = true" @mouseleave="isHovering = false" @click="showInfo" class="svg-list__path"
        :class="{svg__path : isHovering, }"
        :d="item.path">
  </path>
</template>

<script>
export default {
  name: "SvgMap",
  computed: {},
  props: {
    item: {
      type: Object
    },
  },
  data: () => ({
    isHovering: false,
  }),
  mounted() {
  },
  methods: {
    showInfo() {
      this.isHovering = true
      this.$emit('showInfo')
    },
  },
}
</script>

<style lang="scss" scoped>
svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.svg {
  &-list__path {
    fill: #ffffff;
    opacity: 0;
  }
}

.svg__path {
  transition: .3s;
  cursor: pointer;
}

.svg__path:hover {
  fill: #294256;
  opacity: .3;
}

.svg__description {
  position: absolute;
  display: none;
}
.disabled{
  fill: none;
  opacity: 1;
}
.reserve{
  fill: #ffffff;
  opacity: 0;
}
</style>
