<template>
  <div>
    <div class="title">Information</div>
    <div class="items">
      <div class="item">
        <div class="name">Path:</div>
        <div class="value">{{ path }}</div>
      </div>
      <div class="item">
        <div class="name">Route Name:</div>
        <div class="value">{{ name }}</div>
      </div>
      <div class="item">
        <div class="name">Vue.js:</div>
        <div class="value">{{ vue }}</div>
      </div>
      <div class="item">
        <div class="name">Electron:</div>
        <div class="value">{{ electron }}</div>
      </div>
      <div class="item">
        <div class="name">Node:</div>
        <div class="value">{{ node }}</div>
      </div>
      <div class="item">
        <div class="name">Platform:</div>
        <div class="value">{{ platform }}</div>
      </div>
      <div class="item">
        <div class="name">Custom Setting:</div>
        <div class="value">{{ customSetting }}</div>
      </div>
      <div class="item">
        <div class="name">Spacebro message:</div>
        <div class="value" id="message">{{ message }}</div>
      </div>
    </div>
    <img :src="media.url" :alt="media.meta.description"/></img>
  </div>
</template>

<script>
  import { mapState } from 'vuex'
  import settings from '@/lib/settings'

  export default {
    computed: mapState({
      media: state => state.Media.media
    }),
    spacebroEvents: {
      connect: function () {
        this.$spacebro.emit(this.$spacebro.config.client.out.outMessage.eventName, {message: 'thank you'})
      },
      inMessage: function (data) {
        this.message = data.message
      }
    },
    data () {
      let customSetting
      if (settings) {
        customSetting = settings.customSetting
      } else {
        customSetting = 'missing setting'
      }

      return {
        electron: process.versions['atom-shell'],
        name: 'landing-page',
        node: process.versions.node,
        path: '/',
        platform: require('os').platform(),
        customSetting: customSetting,
        message: 'start',
        vue: require('vue/package.json').version
      }
    }
  }
</script>

<style scoped>
  .title {
    color: #888;
    font-size: 18px;
    font-weight: initial;
    letter-spacing: .25px;
    margin-top: 10px;
  }

  img {
    margin-top: 10px;
  }

  .items { margin-top: 8px; }

  .item {
    display: flex;
    margin-bottom: 6px;
  }

  .item .name {
    color: #6a6a6a;
    margin-right: 6px;
  }

  .item .value {
    color: #35495e;
    font-weight: bold;
  }
</style>
