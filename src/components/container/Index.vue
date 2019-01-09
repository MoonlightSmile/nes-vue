<template>
  <div :class="computedClass">
    <p v-if="title" class="title">{{ title }}</p>
    <p v-if="content">{{ content }}</p>
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
  name: 'NContainer',
})
export default class YourComponent extends Vue {
  @Prop({ type: String, default: '' })
  private title!: string;

  @Prop({ type: Boolean, default: false })
  private dark!: boolean;

  @Prop({ type: Boolean, default: false })
  private rounded!: boolean;

  @Prop({ type: String, default: '' })
  private content!: string;

  private get computedClass(): object {
    return {
      'nes-container': true,
      'with-title': this.title,
      'is-dark': this.dark,
      'is-rounded': this.rounded,
    };
  }
}
</script>
