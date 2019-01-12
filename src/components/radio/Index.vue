<template>
  <label>
    <input
      type="radio"
      class="nes-radio"
      :value="value"
      :checked="checked === radioValue"
      @change="onChange"
    >
    <span>{{ label }}</span>
  </label>
</template>

<script lang="ts">
import { Model, Component, Prop, Vue, Watch } from 'vue-property-decorator';
interface MyHTMLInputElement extends HTMLInputElement {
  value: string;
}
interface InputEvent extends Event {
  target: MyHTMLInputElement;
}
type Value = boolean | string | number;
interface ComputedValue {
  [index: string]: (value: string) => Value;
}

@Component({
  name: 'NRadio',
})
export default class Radio extends Vue {
  @Model('change')
  private checked!: Value;
  @Prop()
  private label: string;
  @Prop()
  private value: Value;

  private radioValue: Value = this.value;
  private computedValue(type: string, value: string): Value {
    const typeMap: ComputedValue = {
      number: (val: string): number => {
        return Number(value);
      },
      string: (val: string): string => {
        return String(value);
      },
      boolean: (val: string): boolean => {
        return value === 'true';
      },
    };
    return typeMap[type](value);
  }
  private onChange(e: InputEvent): void {
    const {
      target: { value },
    } = e;
    const currentType: string = typeof this.value;
    const resValue: Value = this.computedValue(currentType, value);
    this.$emit('change', resValue);
  }
}
</script>
