<template>
  <div id="app">
    <e-button>aaa</e-button>
    <e-button type="primary">aaa</e-button>
    <e-button type="error">aaa</e-button>
    <e-button type="success">aaa</e-button>
    <e-button type="disabled">aaa</e-button>
    <e-button type="warning">aaa</e-button>
    <e-container rounded content="Good morning. Thou hast had a good night's sleep, I hope.">
      <e-button type="warning">aaa</e-button>
    </e-container>
    <e-container dark title="aaa" rounded content="Good morning. Thou hast had a good night's sleep, I hope."></e-container>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import EButton from '@/components/button/Index.vue';
import EContainer from '@/components/container/Index.vue';

@Component({
  components: {
    EButton,
    EContainer,
  },
})
export default class App extends Vue {}
</script>

<style lang="stylus">
#app
  font-family 'Press Start 2P', 'Kongtext'
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  color #2c3e50
</style>
