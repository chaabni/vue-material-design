<template>
  <div>
    <table :style="mRootStyle">
      <tbody>
        <tr v-for="row in bodyContent | orderBy firstLetter" :style="mTrStyle" @click="handleClick"
            key="{{$index}}" :class="selectedRow[$index] ? 'selected':''" >
          <td v-if="checkbox" :style="mSelectStyle"><check-box :trigger="selectedRow[$index]"></check-box></td>
          <td v-for="col in row " :style="mTdStyle" track-by="$index">
            {{col}}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script type="text/javascript">
import {zDepthShadows} from 'styles/common'
import Transitions from 'styles/transitions'
import CheckBox from 'CheckBox'
import 'utils/polyfill'

export default {
  data: function() {
    const styles = {
      root: {
        backgroundColor: '#fff',
        padding: '0 24px',
        borderCollapse: 'collapse',
        width: '100%',
        borderSpacing: '0',
        tableLayout: 'fixed',
        fontFamily: 'Roboto, sans-serif'
      },
      td: {
        fontWeight: 'normal',
        fontSize: '14px',
        padding: '6px 13px',
        height: '56px',
        textAlign: 'left',
        position: 'relative',
        wordWrap: 'break-word',
        whiteSpace: 'normal',
      },
      tr: {
        borderBottom: '1px solid #e0e0e0',
      },
      checkbox: {
        width: '24px'
      },
    }
    return {
      mTrStyle: Object.assign(styles.tr, this.trStyle),
      mRootStyle: Object.assign(styles.root, this.styleObj),
      mTdStyle: Object.assign(styles.td, this.tdStyle),
      mSelectStyle: Object.assign(Object.assign({}, styles.td, styles.checkbox), this.tdStyle),
      selectedRow: []
    }
  },
  props: {
    styleObj: Object,
    bodyContent: Array,
    striped: Boolean,
    selectable: Boolean,
    checkbox: Boolean,
    trStyle: Object,
    tdStyle: Object,
    isOrder: {
      type: Boolean,
      default: true
    }
  },
  components: {
    CheckBox
  },
  methods: {
    handleClick: function(e) {
      var node
      if (e.target.nodeName === 'TR') {
        node = e.target.nodeName
      } else {
        node = e.target.closest('tr')
      }
      if (this.selectable) {
        this.selectedRow = Array(this.bodyContent.length).fill(false)
        const rowIndex = node.getAttribute('key')
        const prev = this.selectedRow[rowIndex]
        this.selectedRow.$set(rowIndex, !prev)
      }
    },
    firstLetter: function(a, b) {
      if (this.isOrder) {
        return a[0] > b[0] ? 1 : -1
      } else {
        return true
      }
    }
  }
}
</script>

<style media="screen">
  .selected {
    background-color: rgb(224, 224, 224);
  }
</style>
