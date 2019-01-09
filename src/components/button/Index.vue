<template>
  <button :class="computedClass" @click="onClick($event)">
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
  name: 'NButton',
})
export default class YourComponent extends Vue {
  @Prop({
    type: String,
    default: '',
    validator: (value: string): boolean => {
      return (
        ['', 'primary', 'success', 'warning', 'error', 'disabled'].indexOf(
          value,
        ) !== -1
      );
    },
  })
  private type!: string;

  private get computedClass(): object {
    return {
      'nes-btn': true,
      [`is-${this.type}`]: true,
    };
  }
  private onClick(e: MouseEvent): void {
    if (this.type === 'disabled') {
      return;
    }
    this.$emit('click', e);
  }
}
</script>
