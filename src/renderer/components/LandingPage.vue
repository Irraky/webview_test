<template>
  <div id="wrapper">
    <img id="logo" src="~@/assets/logo.png" alt="electron-vue">
    <main>
      <div class="left-side">
        <span class="title">
          Welcome to your new project!
        </span>
<webview id="foo" src="http://localhost:3000/" style="width:640px; height:480px" plugins></webview>

      </div>

      <div class="right-side">
        <div class="doc">
          <div class="title">Getting Started</div>
          <p>
            electron-vue comes packed with detailed documentation that covers everything from
            internal configurations, using the project structure, building your application,
            and so much more.
          </p>
          <button @click="open('https://simulatedgreg.gitbooks.io/electron-vue/content/')">Read the Docs</button><br><br>
        </div>
        <div class="doc">
          <div class="title alt">Other Documentation</div>
          <button class="alt" @click="open('https://electron.atom.io/docs/')">Electron</button>
          <button class="alt" @click="open('https://vuejs.org/v2/guide/')">Vue.js</button>
        </div>

      </div>
    </main>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  import ServiceWorkerInformation from './LandingPage/ServiceWorkerInformation'

  onload = () => {
    const webview = document.querySelector('webview')
    const indicator = document.querySelector('.indicator')
    console.log('hey' + webview.loadURL)
    const loadstart = () => {
      indicator.innerText = 'loading...'
    }
    console.log('indicator.innerText')
    console.log(indicator.innerText)
    const loadstop = () => {
      indicator.innerText = ''
    }

    webview.addEventListener('did-start-loading', loadstart)
    webview.addEventListener('did-stop-loading', loadstop)
  }
  export default {
    name: 'landing-page',
    components: { SystemInformation, ServiceWorkerInformation },
    methods: {
      sendMessage () {
        this.$spacebro.emit(this.$spacebro.config.client.out.outMessage.eventName, {
          message: 'thank you'.split('').sort(function () { return 0.5 - Math.random() }).join('')
        })
      },
      sendMedia () {
        this.$spacebro.emit(this.$spacebro.config.client.out.outMedia.eventName, {
          url: 'http://lorempixel.com/400/200/business/spacebro-is-' + 'awesome'.split('').sort(function () { return 0.5 - Math.random() }).join(''),
          file: 'file.jpg',
          type: 'image/jpg',
          details: {
            width: 320,
            height: 240
          },
          meta: {
            title: 'galaxy',
            description: 'galaxy image'
          }
        })
      },
      open (link) {
        this.$electron.shell.openExternal(link)
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  

  body { font-family: 'Source Sans Pro', sans-serif; }

  #wrapper {
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }

  #logo {
    height: auto;
    margin-bottom: 20px;
    width: 420px;
  }

  main {
    display: flex;
    justify-content: space-between;
  }

  main > div { flex-basis: 50%; }

  .left-side {
    display: flex;
    flex-direction: column;
  }

  .welcome {
    color: #555;
    font-size: 23px;
    margin-bottom: 10px;
  }

  .title {
    color: #2c3e50;
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 6px;
  }

  .title.alt {
    font-size: 18px;
    margin: 10px 0px;
  }

  p {
    color: black;
    margin-bottom: 10px;
  }

  button {
    font-size: .8em;
    cursor: pointer;
    outline: none;
    padding: 0.75em 2em;
    border-radius: 2em;
    display: inline-block;
    color: #fff;
    background-color: #4fc08d;
    transition: all 0.15s ease;
    box-sizing: border-box;
    border: 1px solid #4fc08d;
  }

  .doc button.alt {
    color: #42b983;
    background-color: transparent;
  }

  .value {
    display: inline;
    color: #35495e;
    font-weight: bold;
  }
</style>
