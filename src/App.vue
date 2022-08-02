<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <hot-table ref="boxListTable" :data="boxListTable" :settings="boxListSettings"></hot-table>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

import {HotTable} from '@handsontable/vue'
import {registerAllModules} from 'handsontable/registry'
import 'handsontable/dist/handsontable.full.css'

registerAllModules()

export default {
  name: 'App',
  components: {
    HelloWorld, HotTable
  },
  data(){
    function getHeight() {
      const height = document.body.clientHeight - 220
      console.log(height, 'height')
      return height
      // if (this.boxListTable.length > 20 || this.goodsListTable.length > 20) {
      //   const height = document.body.clientHeight - 220
      //   console.log(height, 'height')
      //   return height
      // } else {
      //   return 'auto'
      // }
    }
    return {
      boxListTable: [
        ['11', '11', '11', '11', '11','11']
      ],
      boxListSettings: {
        data: ['11', '11', '11', '11', '11','11'],
        rowHeaders: true,
        licenseKey: 'non-commercial-and-evaluation',
        colHeaders: ['货箱编号', '货箱长度(cm)', '货箱宽度(cm)', '货箱高度(cm)', '货箱重量(kg)', '系统编号'],
        colWidths: [250, 250, 250, 250, 250, 200],
        className: 'htCenter htMiddle',
        fixedRowsTop: 0,
        cells(row, column, prop) {
          const cellProperties = {readOnly: false}
          console.log(prop, 'prop')
          // const visualRowIndex = this.instance.toVisualRow(row)
          const visualColIndex = this.instance.toVisualColumn(column)
          if (visualColIndex === 5) {
            cellProperties.readOnly = true
          }
          return cellProperties
        },
        // afterChange: (change, source) => {
        //   // this.reCalculation(change, source)
        //   // if (change != null) {
        //   //   console.log(change, source, 'chnage==table')
        //   //   this.boxValueChange()
        //   // }
        // },
        height: getHeight()
      },
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
