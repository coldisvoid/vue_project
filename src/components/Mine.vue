<template>
  <div>
    <h3>我的问卷</h3>
    <el-collapse accordion>
  <el-collapse-item v-for="(q,index) in Questionnaires" :title="q.title" :key="index">

    <el-button  @click="edit(index)">编辑</el-button>
  </el-collapse-item>

</el-collapse>

  </div>
</template>

<script>
export default {
  data () {
    return {
      Questionnaires: [
        {
          title: '问卷一',
          questions: [
            {
              type: 'input',
              question: '单行输入问题',
              answer: ''
            },
            {
              type: 'radio',
              question: '单选问题',
              choices: ['选项1', '选项2'],
              answer: ''
            },
            {
              type: 'checkbox',
              question: '多选问题',
              choices: ['选项1', '选项2'],
              answer: []
            }
          ]
        },
        {
          title: '问卷二',
          questions: [
            {
              type: '',
              question: '单选问题',
              choices: [],
              answer: ''
            }
          ]
        }
      ]

    }
  },
  created () {
    // this.$router.push('/edit')
  },
  methods: {
    add () {
      this.Questionnaires.push({
        title: 'sa',
        id: 'dsad',
        questions: [
          {
            type: '',
            question: '',
            choices: ''
          }
        ]
      })
    },
    onSubmit () {
      console.log(this.Questionnaires)
    },
    edit (index) {
      this.$router.push({
        path: '/edit',
        query: {
          choose: index
        }
      })
    }
  }
}

</script>
