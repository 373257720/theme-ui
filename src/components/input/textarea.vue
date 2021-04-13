/* eslint-disable no-undef */
<template>
  <div class="GZ-textarea">
    <textarea
      class="GZ-textarea__inner"
      :style="{ height: AutoHight }"
      v-model="content"
      @keydown="handleKeyCode($event)"
      placeholder="please input"
    ></textarea>
  </div>
</template>
<script>
var hiddenTextarea = void 0
var HIDDEN_STYLE =
  '\n  height:0 !important;\n  visibility:hidden !important;\n  overflow:hidden !important;\n  position:absolute !important;\n  z-index:-1000 !important;\n  top:0 !important;\n  right:0 !important\n'
export default {
  data () {
    return {
      content: '',
      leave: true,
      AutoHight: ''
    }
  },
  created () {
  },
  methods: {
    calculateNodeStyling (targetElement) {
      var CONTEXT_STYLE = [
        'letter-spacing',
        'line-height',
        'padding-top',
        'padding-bottom',
        'font-family',
        'font-weight',
        'font-size',
        'text-rendering',
        'text-transform',
        'width',
        'text-indent',
        'padding-left',
        'padding-right',
        'border-width',
        'box-sizing'
      ]
      var style = window.getComputedStyle(targetElement)

      var boxSizing = style.getPropertyValue('box-sizing')

      var paddingSize =
        parseFloat(style.getPropertyValue('padding-bottom')) +
        parseFloat(style.getPropertyValue('padding-top'))

      var borderSize =
        parseFloat(style.getPropertyValue('border-bottom-width')) +
        parseFloat(style.getPropertyValue('border-top-width'))

      var contextStyle = CONTEXT_STYLE.map(function (name) {
        return name + ':' + style.getPropertyValue(name)
      }).join(';')

      return {
        contextStyle: contextStyle,
        paddingSize: paddingSize,
        borderSize: borderSize,
        boxSizing: boxSizing
      }
    },
    calcTextareaHeight (targetElement) {
      var minRows =
        arguments.length > 1 && arguments[1] !== undefined ? arguments[1] : 1
      var maxRows =
        arguments.length > 2 && arguments[2] !== undefined
          ? arguments[2]
          : null
      if (!hiddenTextarea) {
        hiddenTextarea = document.createElement('textarea')
        document.body.appendChild(hiddenTextarea)
      }
      var _calculateNodeStyling = this.calculateNodeStyling(targetElement)
      var paddingSize = _calculateNodeStyling.paddingSize
      var borderSize = _calculateNodeStyling.borderSize
      var boxSizing = _calculateNodeStyling.boxSizing
      var contextStyle = _calculateNodeStyling.contextStyle

      hiddenTextarea.setAttribute('style', contextStyle + ';' + HIDDEN_STYLE)
      hiddenTextarea.value =
        targetElement.value || targetElement.placeholder || ''

      var height = hiddenTextarea.scrollHeight
      var result = {}

      if (boxSizing === 'border-box') {
        height = height + borderSize
      } else if (boxSizing === 'content-box') {
        height = height - paddingSize
      }

      hiddenTextarea.value = ''
      var singleRowHeight = hiddenTextarea.scrollHeight - paddingSize

      if (minRows !== null) {
        var minHeight = singleRowHeight * minRows
        if (boxSizing === 'border-box') {
          minHeight = minHeight + paddingSize + borderSize
        }
        height = Math.max(minHeight, height)
        result.minHeight = minHeight + 'px'
      }
      if (maxRows !== null) {
        var maxHeight = singleRowHeight * maxRows
        if (boxSizing === 'border-box') {
          maxHeight = maxHeight + paddingSize + borderSize
        }
        height = Math.min(maxHeight, height)
      }
      result.height = height + 'px'
      hiddenTextarea.parentNode &&
        hiddenTextarea.parentNode.removeChild(hiddenTextarea)
      hiddenTextarea = null
      return result
    },
    // 键盘回车事件
    handleKeyCode (event) {
      let a = this.calcTextareaHeight(event.target)
      this.AutoHight = a.height
      console.log(a)
    }
  }
}
</script>

<style lang='scss'>
.GZ-textarea {
  width: 180px;
  position: relative;
  font-size: 14px;
  margin-bottom: 30px;;
//   display: inline-block;
  //   vertical-align: bottom;
  .GZ-textarea__inner {
    display: block;
    resize: vertical;
    background-image: none;
    min-height: 33px;
    font-family: inherit;
    @include Font(inherit, 1.5, #606266);
    @include border(1px, solid, #dcdfe6, 4px);
    @include boxModel(100%, 54px, #fff, 5px 15px);
    transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
    &:focus {
      outline: none;
      border-color: $themeColor;
    }
  }
  .GZ-textarea__suffix {
    z-index: $default-Index;
    color: $themeColor;
    cursor: pointer;
    @include positonAbsolute("m", 0, "r", 10px);
  }
}
</style>
