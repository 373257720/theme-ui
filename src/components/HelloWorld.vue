<template>
  <div class="hello">
    <Custom-Input></Custom-Input>
    <GZ-Textarea></GZ-Textarea>
    <GZ-radio></GZ-radio>
    <GZ-checkbox></GZ-checkbox>
  </div>
</template>

<script>
import CustomInput from '@/components/input/input'
import GZTextarea from '@/components/input/textarea'
import GZradio from '@/components/radio/radio'
import GZcheckbox from '@/components/checkbox/checkbox'
// import { component } from 'vue/types/umd'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    'Custom-Input': CustomInput,
    'GZ-Textarea': GZTextarea,
    'GZ-radio': GZradio,
    'GZ-checkbox': GZcheckbox
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
