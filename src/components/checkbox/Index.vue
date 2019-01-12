<template>
  <label>
    <input
      type="checkbox"
      class="nes-checkbox"
      :value="value"
      :checked="checked.includes(checkboxValue)"
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
  name: 'NCheckbox',
})
export default class Checkbox extends Vue {
  @Model('change')
  private checked!: any[];
  @Prop()
  private label: string;
  @Prop()
  private value: Value;

  private checkboxValue: Value = this.value;
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
    if (this.checked.includes(resValue)) {
      const index = this.checked.findIndex((val: string) => {
        return val === resValue;
      });
      this.$delete(this.checked, index);
    } else {
      this.checked.push(resValue);
    }
    this.$emit('change', this.checked);
  }
}
</script>
