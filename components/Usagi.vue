<template>
    <creature :position="position" :image="getUsagiImage()"/>
</template>

<script lang="ts">
import {
  Component,
  Prop,
  Vue
} from "nuxt-property-decorator"
import Creature, { ImageProp } from "~/components/Creature.vue"

@Component({
  components: {
    Creature
  }
})
export default class UsagiFactory extends Vue {
  @Prop() position: {x: number, y: number};

  static readonly usagiImages: ImageProp[] = [
    { src: require("~/assets/usagi1.png"), size: {width:160, height: 160}, orientation: "left"},
    { src: require("~/assets/usagi2.png"), size: {width:170, height: 170}, orientation: "right"},
    { src: require("~/assets/usagi3.png"), size: {width:170, height: 170}, orientation: "right"},
  ];

  getUsagiImage(): ImageProp {
    return UsagiFactory.usagiImages[Math.floor(Math.random() * UsagiFactory.usagiImages.length)];
  }
}
</script>
