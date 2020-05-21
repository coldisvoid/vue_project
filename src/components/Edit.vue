<template>
    <el-container>
            <!-- 侧边栏 -->
    <el-aside width="200px">
      <!-- 侧边栏菜单区 -->
      <el-menu default-active="2" active-text-color="#409EFF">
        <!-- 一级菜单 -->
        <el-submenu :index="item.id+''" v-for="item in menulist" :key="item.id">
          <!-- 一级菜单模板区 -->
        <template slot="title">
          <!-- 图标 -->
          <i class="el-icon-location"></i>
          <!-- 文本 -->
          <span>{{item.authName}}</span>
        </template>
          <!-- 二级菜单 -->
          <el-menu-item index="subItem.id" v-for="subItem in item.children"
          :key="subItem.id">
            <!-- 图标 -->
            <i class="el-icon-location"></i>
            <!-- 文本 -->
            <span>{{subItem.authName}}</span>
          </el-menu-item>
        </el-submenu>
        <el-menu-item index="1">处理中心</el-menu-item>
    </el-menu>
    </el-aside>
    <!-- 右侧内容主题 -->
    <el-main>

问卷标题： {{this.Questionnaires[myindex].title}}
    <el-form :model="Questionnaires[myindex]">
      <el-form-item v-for="(q,index) in Questionnaires[myindex].questions" :key="index" :label="q.question">
        <el-input v-if="q.type=='input'" v-model="q.answer"></el-input>
        <el-checkbox-group v-if="q.type=='checkbox'" v-model="q.answer">
          <el-checkbox v-for="(c,index) in q.choices" :key="index" :label="c"></el-checkbox>
        </el-checkbox-group>
        <el-radio-group v-if="q.type=='radio'" v-model="q.answer">
          <el-radio v-for="(c,index) in q.choices" :key="index" :label="c"></el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" >提交</el-button>
        <el-button>取消</el-button></el-form-item>
    </el-form>

    </el-main>
    </el-container>
</template>

<script>
export default {
  data () {
    return {
      myindex: '',
      menulist: [],
      forms: [
        { id: 1, type: '1', title: 't1', text: 't1' },
        { id: 2, type: '2', title: 't2', text: 't2' },
        { id: 3, type: '1', title: 't1', text: 't1' },
        { id: 4, type: '2', title: 't2', text: 't2' }
      ],
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
              type: 'radio',
              question: '单选问题',
              choices: ['1', '2', '3'],
              answer: ''
            }
          ]
        }
      ]
    }
  },
  created () {
    this.getMenuList()
  },
  mounted () {
    this.myindex = this.$route.query.choose
    console.log(this.myindex)
  },
  methods: {

    // 获取所有菜单
    async getMenuList () {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) return 1
      this.menulist = res.data
      console.log(res)
    }
  }
}

</script>

<style lang="less" scoped>

.el-aside {
    border: 1px solid #eee;
}
.el-main {
    border: 1px solid #eee
}
</style>
