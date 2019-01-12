<template>
  <div :class="computedClass">
    <p
      v-if="title"
      class="title"
    >{{ title }}</p>
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { Model, Component, Prop, Vue } from 'vue-property-decorator';

@Component({
  name: 'NContainer',
})
export default class Container extends Vue {
  @Prop({ type: String, default: '' })
  private title!: string;

  @Prop({ type: Boolean, default: false })
  private dark!: boolean;

  @Prop({ type: Boolean, default: false })
  private rounded!: boolean;

  private get computedClass(): object {
    const { title, dark, rounded } = this;
    const isTitle: boolean = Boolean(title);
    return {
      'nes-container': true,
      'with-title': isTitle,
      'is-dark': dark,
      'is-rounded': rounded,
    };
  }
}
</script>
