<template>
  <d2-container>
    <el-form>
      <el-form-item>
        <h1>原始合约</h1>
        <el-input v-model="inputText" placeholder="请输入内容" type="textarea" autosize disabled="true"></el-input>
      </el-form-item>
      <el-form-item>
        <h1>修改后合约</h1>
        <el-input v-model="outputText" type="textarea" autosize disabled="true"></el-input>
      </el-form-item>
      <el-form-item>
        <template>
          <el-radio @change="chooseMethod('1')" v-model="radio" label="1">方案一</el-radio>
          <el-radio @change="chooseMethod('2')" v-model="radio" label="2">方案二</el-radio>
          <el-button>导出修改</el-button>
        </template>
      </el-form-item>
    </el-form>
  </d2-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'locateOne',
  data () {
    return {
      radio: '1',
      inputText: 'contract Storage {\n' +
        '    uint256 number;\n' +
        '\n' +
        '    function store(uint256 num) public {\n' +
        '        number = num;\n' +
        '    }\n' +
        '\n' +
        '    function retrieve() public view returns (uint256){\n' +
        '        return number;\n' +
        '    }\n' +
        '}',
      outputText: 'text1',
      form: {
        name: '',
        init: 'randomized',
        desc: '',
        fileList: []
      }
    }
  },
  methods: {
    onSubmit () {
      console.log(this.form)
      axios.post('/api/create', this.form, { emulateJSON: true }, { headers: { 'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8' } }
      ).then(response => {
        console.log('提交成功')
      })
    },
    httpRequest (option) {
      this.form.fileList.push(option)
    },
    chooseMethod (label) {
      switch (label) {
        case '1':
          this.outputText = 'text1'
          break
        case '2':
          this.outputText = 'text2'
          break
        default:
          break
      }
    }
  }
}
</script>
