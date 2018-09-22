<template>
  <usagi-field/>
</template>

<script lang="ts">
import {
  Component,
  Vue
} from "nuxt-property-decorator"
import UsagiField from "~/components/UsagiField.vue"

@Component({
  components: {
    UsagiField
  }
})
export default class extends Vue {
}
</script>
