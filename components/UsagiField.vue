<template>
  <div class="field" @click="addUsagi">
    <usagi v-for="(position, i) in positions" :key="i" :position="position"/>
  </div>
</template>

<script lang="ts">
import {
  Component,
  Vue
} from "nuxt-property-decorator"
import Usagi from "~/components/Usagi.vue"

@Component({
  components: {
    Usagi
  }
})
export default class UsagiField extends Vue {
  positions: {x: number, y: number}[] = [];

  addUsagi(evt: MouseEvent): void {
    this.positions.push({
      x: evt.x,
      y: evt.y,
    });
  }
}
</script>

<style lang="scss" scoped>
.field {
  position: fixed;
  width: 100%;
  height: 100%;
  -webkit-tap-highlight-color: transparent;
}
</style>
