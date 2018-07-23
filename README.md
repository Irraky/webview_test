# webview

> Test of webview using socket.io-unity

#### Build Setup

``` bash
# install dependencies
cd ..
git clone https://github.com/Irraky/socket.io-unity
cd socket.io-unity
npm install
npm run dev
cd ../webview_test (or the name you choose to clone the project)
Change src of webview in LandingPage.vue line 9 with
npm install

# serve with hot reload at localhost:9080
npm run dev

# build electron application for production
npm run build

# run unit & end-to-end tests
npm test


# lint all JS/Vue component files in `src/`
npm run lint

```

---

This project was generated with [electron-vue](https://github.com/soixantecircuits/electron-vue)@[4c6ee7b](https://github.com/SimulatedGREG/electron-vue/tree/4c6ee7bf4f9b4aa647a22ec1c1ca29c2e59c3645) using [vue-cli](https://github.com/vuejs/vue-cli). Documentation about the original structure can be found [here](https://soixantecircuits.gitbooks.io/electron-vue/content/index.html).
