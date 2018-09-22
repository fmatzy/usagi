<!--
  Portions are:
  Copyright (c) 2016 ICS INC.
  Originally under MIT License
  https://github.com/ics-creative/160311_css3_animation
-->
<template>
  <div :style="styleObject" class="creature" :class="{touched: touched, inverse: inverse}"
    @click.stop="touch">
    <img ref="img" :src="image.src">
  </div>
</template>

<script lang="ts">
import {
  Component,
  Prop,
  Vue
} from "nuxt-property-decorator"
import { setTimeout, setInterval } from "timers";

export class ImageProp {
  src: any;
  size: {width: number, height: number};
  orientation: "left"|"right";
}

@Component({})
export default class Creature extends Vue {
  @Prop() position: {x: number, y:number};
  @Prop() image: ImageProp;

  touched: boolean = false;
  inverse: boolean = false;

  get styleObject() {
    return {
      top: (this.position.y - this.image.size.height / 2) + "px",
      left: (this.position.x - this.image.size.width / 2) + "px",
      position: "absolute",
      width: this.image.size.width + "px",
      height: this.image.size.height + "px",
    }
  }

  mounted(): void {
    setInterval(() => {
      const getDelta = () => Math.floor(Math.random() * 100) - 50;
      var deltaX = getDelta();
      var deltaY = getDelta();

      this.position.x += deltaX;
      this.position.y += deltaY;
      this.inverse = (this.image.orientation == "left") ? (deltaX > 0) : !(deltaX > 0);
    },300);
  }

  touch(): void {
    if (this.touched) return;

    this.touched = true;
    setTimeout(() => { this.touched = false }, 1100);
  }

}
</script>

<style lang="scss" scoped>
.creature {
  transition: top 0.3s, left 0.3s;
  -webkit-touch-callout: none;
  -webkit-user-select: none;

  &.touched {
    animation: fluffy 0.7s linear 0s 1;
  }
  &.inverse {
    transform: scale(-1,1);
  }
}

@keyframes fluffy {
  0%   { transform: scale(1.0, 1.0) translate(0%, 0%); }
  10%  { transform: scale(1.1, 0.9) translate(0%, 5%); }
  40%  { transform: scale(1.2, 0.8) translate(0%, 15%); }
  50%  { transform: scale(1.0, 1.0) translate(0%, 0%); }
  60%  { transform: scale(0.9, 1.2) translate(0%, -50%); }
  75%  { transform: scale(0.9, 1.2) translate(0%, -20%); }
  85%  { transform: scale(1.2, 0.8) translate(0%, 15%); }
  100% { transform: scale(1.0, 1.0) translate(0%, 0%); }
}
</style>
