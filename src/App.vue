<template>
  <div id="app">
    <e-button>aaa</e-button>
    <e-button type="primary">aaa</e-button>
    <e-button type="error">aaa</e-button>
    <e-button type="success">aaa</e-button>
    <e-button disabled>aaa</e-button>
    <e-button
      type="warning"
      disabled
    >aaa</e-button>
    <e-container rounded>
      <p>Good morning. Thou hast had a good night's sleep, I hope.</p>
      <e-button type="warning">aaa</e-button>
    </e-container>
    <e-container
      dark
      title="aaa"
      rounded
    >
      Good morning. Thou hast had a good night's sleep, I hope.
    </e-container>

    <e-radio
      v-for="({label, value: OValue}) in list"
      :key="OValue"
      v-model="value"
      :label="label"
      :value="String(OValue)"
    />
    <p style="color: red">val:{{value}}</p>
    <e-radio-group
      v-model="value2"
      :options="list"
    ></e-radio-group>
    <p style="color: red">val:{{value2}}</p>
    <e-radio-group
      v-model="value3"
      :options="yesOrNo"
    ></e-radio-group>
    <p style="color: red">val:{{value3}}</p>
    <e-checkbox
      v-model="value4"
      v-for="{value, label} in list"
      :key="value"
      :value="value"
      :label="label"
      :options="list"
    ></e-checkbox>
    <p style="color: red">val:{{value4}}</p>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import EButton from '@/components/button/Index.vue';
import EContainer from '@/components/container/Index.vue';
import ERadio from '@/components/radio/Index.vue';
import ERadioGroup from '@/components/radio/RadioGroup.vue';
import ECheckbox from '@/components/checkbox/Index.vue';

interface Options {
  label: string;
  value: boolean | string | number;
}

@Component({
  components: {
    EButton,
    EContainer,
    ERadio,
    ERadioGroup,
    ECheckbox,
  },
})
export default class App extends Vue {
  private value: string = '3';
  private value2: number = 3;
  private value3: boolean = false;
  private value4: number[] = [3];
  private list: Options[] = [
    {
      label: 'apple',
      value: 1,
    },
    {
      label: 'banana',
      value: 2,
    },
    {
      label: 'grapes',
      value: 3,
    },
    {
      label: 'orange',
      value: 4,
    },
  ];
  private yesOrNo = [
    { label: 'yes', value: true },
    { label: 'no', value: false },
  ];
}
</script>

<style lang="stylus">
#app
  font-family 'Press Start 2P', 'Kongtext'
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #2c3e50
</style>
