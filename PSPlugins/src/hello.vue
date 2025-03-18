<template>
  <form style="padding: 20px">
    <sp-heading>
      {{ message }}
    </sp-heading>
    <sp-body> Button has been clicked {{ count }} times.</sp-body>
    <sp-button v-on:click="increment">Click me</sp-button>
  </form>
</template>

<script>
import {ref} from "vue";

export default {
  setup() {
    const photoshop = require('photoshop')
    const app = photoshop.app
    let count = ref(0);
    const message = "Hello World Vue 3 Component!";

    async function makeDefaultDocument(executionContext) {
      try {
        //let newDoc1 = await app.documents.add();
        const fs = require('uxp').storage.localFileSystem;
        const folder = await fs.getPluginFolder(); // returns a Folder instance
        console.log(folder);
        const folderEntry = await folder.getEntry("1.jpg");
        let dom = app.open(folderEntry);
        console.log(folderEntry);
      } catch (err) {
        console.log(err);
      }
    }

    const increment = async () => {
      console.log(app.activeDocument)
      await photoshop.core.executeAsModal(makeDefaultDocument)
      count.value++;
    };
    return {count, message, increment};
  },
};
</script>
