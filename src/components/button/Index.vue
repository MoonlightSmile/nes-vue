<template>
  <button
    :class="computedClass"
    @click="onClick($event)"
  >
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
  name: 'NButton',
})
export default class Button extends Vue {
  @Prop({
    type: Boolean,
    default: false,
  })
  private disabled!: boolean;

  @Prop({
    type: String,
    validator: (value: string): boolean => {
      const types: string[] = ['primary', 'success', 'warning', 'error'];
      return types.includes(value);
    },
  })
  private type!: string;

  private get computedClass(): object {
    const { disabled, type } = this;
    return {
      'nes-btn': true,
      [`is-${type}`]: true,
      'is-disabled': disabled,
    };
  }
  private onClick(e: MouseEvent): void {
    if (this.disabled) {
      return;
    }
    this.$emit('click', e);
  }
}
</script>
