<template>
  <div id="app">
    <e-container
      title="button"
      class="button"
    >
      <e-button>default</e-button>
      <e-button type="primary">primary</e-button>
      <e-button type="error">error</e-button>
      <e-button type="success">success</e-button>
      <e-button disabled>disabled</e-button>
      <e-button
        type="warning"
        disabled
      >warning && disabled</e-button>
    </e-container>
    <e-container title="container">
      <e-container title="Container.is-centered">
        <p>Good morning. Thou hast had a good night's sleep, I hope.</p>
      </e-container>
      <e-container
        dark
        title="Container.is-dark"
      >
        <p>Good morning. Thou hast had a good night's sleep, I hope.</p>
      </e-container>
      <e-container rounded>
        <p>Good morning. Thou hast had a good night's sleep, I hope.</p>
      </e-container>
      <e-container
        rounded
        dark
      >
        <p>Good morning. Thou hast had a good night's sleep, I hope.</p>
      </e-container>
    </e-container>
    <e-container title="radio">
      <e-radio-group
        v-model="value2"
        :options="list"
      ></e-radio-group>
      <p style="color: red">val:{{value2}}</p>

      <e-radio
        v-for="({label, value: OValue}, index) in list"
        :key="`${index + 'radio'}`"
        v-model="value"
        :label="label"
        :value="String(OValue)"
      />
      <p style="color: red">val:{{value}}</p>

      <e-radio-group
        v-model="value3"
        :options="yesOrNo"
      ></e-radio-group>
      <p style="color: red">val:{{value3}}</p>
    </e-container>
    <e-container title="checkbox">
      <e-checkbox
        v-model="value4"
        v-for="({value, label}, index) in list"
        :key="`${value+index}`"
        :value="value"
        :label="label"
        :options="list"
      ></e-checkbox>
      <p style="color: red">val:{{value4}}</p>
    </e-container>

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
body
  padding 10px
#app
  font-family 'Press Start 2P', 'Kongtext'
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #2c3e50
  .nes-container
    *:not(:first-child)
      max-width 400px
      margin-right 2px
      margin-bottom 5px
  -webkit-tap-highlight-color transparent
input[type='radio'], input[type='checkbox']
  opacity 0
</style>
