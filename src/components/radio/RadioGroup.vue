<template>
  <div>
    <slot>
      <n-radio
        v-for="({value, label}) in options"
        :key="value"
        v-model="radioValue"
        :value="value"
        :label="label"
        @input="$emit('input', $event.target.value)"
      ></n-radio>
    </slot>
  </div>
</template>

<script lang="ts">
import { Model, Component, Prop, Vue, Watch } from 'vue-property-decorator';
import NRadio from './Index.vue';
type Value = boolean | string | number;

interface Options {
  label: string;
  value: Value;
}

@Component({
  name: 'NRadioGroup',
  components: {
    NRadio,
  },
})
export default class RadioGroup extends Vue {
  @Prop()
  private value: Value;
  @Prop()
  private options: Options[];

  private radioValue: Value = this.value;

  @Watch('value')
  private onValueChange(val: Value, oldVal: Value): void {
    this.radioValue = val;
  }
  @Watch('radioValue')
  private onRadioValueChange(val: Value, oldVal: Value): void {
    this.$emit('input', val);
  }
}
</script>
