<template>
  <Editor
    class="bytemd"
    :value="value" 
    :plugins="plugins" 
    @change="handleChange"
    placeholder="请输入..."
    :locale="zhHans" 
    :uploadImages="uploadImage"
    :editorConfig="editorConfig"
  />
</template>

<script>
// CSS
import 'bytemd/dist/index.min.css'
import 'highlight.js/styles/default.css'
import 'katex/dist/katex.css'
import 'juejin-markdown-themes/dist/juejin.min.css'

// 中文包
import zhHans from 'bytemd/locales/zh_Hans.json'
import gfmLocale from '@bytemd/plugin-gfm/locales/zh_Hans.json';
import mathLocale from '@bytemd/plugin-math/locales/zh_Hans.json';
import mermaidLocale from '@bytemd/plugin-mermaid/locales/zh_Hans.json';
//插件
import breaks from '@bytemd/plugin-breaks' 
import frontmatter from '@bytemd/plugin-frontmatter'
import gemoji from '@bytemd/plugin-gemoji'
import gfm from '@bytemd/plugin-gfm'
// import highlight from '@bytemd/plugin-highlight'
import highlight from '@bytemd/plugin-highlight-ssr'
// import math from '@bytemd/plugin-math'
import math from '@bytemd/plugin-math-ssr'
import mediumZoom from '@bytemd/plugin-medium-zoom' 
import mermaid from '@bytemd/plugin-mermaid'
import { Editor } from '@bytemd/vue'

const plugins = [
  breaks(),
  frontmatter(),
  gemoji(),
  gfm({locale: gfmLocale}),
  highlight(),
  math({locale: mathLocale}),
  mediumZoom(),
  mermaid({locale: mermaidLocale}),
]

export default {
  components: { Editor },
  data() {
    return { 
      value: '',
      plugins,
      zhHans,
      editorConfig:{

      }
    }
  },
  methods: {
    handleChange(v) {
      this.value = v
    },
    async uploadImage(files) {
      console.log('files', files)
      return [
        {
          title: files.map((i) => i.name),
          url: 'http'
        }
      ]
    }
  }
}
</script>
<style scoped>

</style>