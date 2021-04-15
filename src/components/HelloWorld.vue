<template>
  <div class="hello">
    <Custom-Input></Custom-Input>
    <GZ-Textarea></GZ-Textarea>
    <GZ-radio></GZ-radio>
    <GZ-checkbox></GZ-checkbox>
    <GZ-select></GZ-select>
    <GZ-mutipleSelect></GZ-mutipleSelect>
    <GZ-switch></GZ-switch>
  </div>
</template>

<script>
import CustomInput from '@/components/Form/input'
import GZTextarea from '@/components/Form/textarea'
import GZradio from '@/components/Form/radio'
import GZcheckbox from '@/components/Form/checkbox'
import GZselect from '@/components/Form/select'
import GZmutipleSelect from '@/components/Form/mutipleSelect'
import GZswitch from '@/components/Form/switch'

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
    'GZ-checkbox': GZcheckbox,
    'GZ-select': GZselect,
    'GZ-mutipleSelect': GZmutipleSelect,
    'GZ-switch': GZswitch
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
