<template>
    <div class="question">
      <el-container v-if="seen" style="background-color: rgba(242,242,242,1)">
          <el-main>
           <h1 id="title">{{title}}</h1>
           <p class="description">{{description}}</p>
           <el-col style="background-color: #ffffff; margin-top: 100px; padding: 30px" :xs="{span:22, offset: 1}" :sm="{span:20, offset: 2}" :md="{span: 18, offset: 3}" :lg="{span: 12, offset: 6}" :xl="{span: 12, offset: 6}">
              <div v-for="(questItem,order) in questionnaireData" :key=order class="questItem">
                  <div v-if="questItem.questionType=='0'">
                      <p class="questItem-title">
                          <span style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span><span style="color: red">*</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-radio-group v-model="answerSet[order].ans.choice">
                          <div v-for="(choiceItem,index) in questItem.content.choice" :key=index class="choiceItem">
                              <el-radio :label=index disabled>{{choiceItem}}</el-radio>
                          </div>
                      </el-radio-group>
                  </div>
                  <div v-else-if="questItem.questionType=='1'">
                      <p class="questItem-title">
                          <span style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-radio-group v-model="answerSet[order].ans.choice">
                          <div v-for="(choiceItem,index) in questItem.content.choice" :key=index class="choiceItem">
                              <el-radio :label=index disabled>{{choiceItem}}</el-radio>
                          </div>
                      </el-radio-group>
                  </div>
                  <div v-else-if="questItem.questionType=='2'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span><span style="color: red">*</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-checkbox-group v-model="answerSet[order].ans.choice">
                          <div v-for="(choiceItem,index) in questItem.content.choice" :key=index class="choiceItem">
                              <el-checkbox :label="choiceItem" disabled>{{choiceItem}}</el-checkbox>
                          </div>
                      </el-checkbox-group>
                  </div>
                  <div v-else-if="questItem.questionType=='3'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-checkbox-group v-model="answerSet[order].ans.choice">
                          <div v-for="(choiceItem,index) in questItem.content.choice" :key=index class="choiceItem">
                              <el-checkbox :label="choiceItem" disabled>{{choiceItem}}</el-checkbox>
                          </div>
                      </el-checkbox-group>
                  </div>
                  <div v-else-if="questItem.questionType=='4'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span><span style="color: red">*</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-input v-model="answerSet[order].ans.text" placeholder="" :disabled="true"></el-input>
                  </div>
                  <div v-else-if="questItem.questionType=='5'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-input v-model="answerSet[order].ans.text" placeholder="" :disabled="true"></el-input>
                  </div>
                  <div v-else-if="questItem.questionType=='6'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span><span style="color: red">*</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-input v-model="answerSet[order].ans.text" placeholder="" type="textarea" :rows="5" :disabled="true"></el-input>
                  </div>
                  <div v-else-if="questItem.questionType=='7'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-input v-model="answerSet[order].ans.text" placeholder="" type="textarea" :rows="5" :disabled="true"></el-input>
                  </div>
                  <div v-else-if="questItem.questionType=='8'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span><span style="color: red">*</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-rate v-model="answerSet[order].ans.mark" disabled></el-rate>
                  </div>
                  <div v-else-if="questItem.questionType=='9'">
                      <p class="questItem-title">
                          <span class="questionTitle" style="font-weight: bold">{{questItem.order+1}} </span><span>{{questItem.content.title}}</span>
                          <span v-text="questItem.title"></span>
                      </p>
                      <el-rate v-model="answerSet[order].ans.mark" disabled></el-rate>
                  </div>
                  <div v-else-if="questItem.questionType=='10'">
                      <p class="questItem-title">
                          <span>{{questItem.order+1}}、</span>
                          <span v-for="(titleBlank,index) in questItem.content.title" :key=index class="titleBlank">
                              <span v-if="index!=questItem.content.title.length-1">
                                  <span>{{titleBlank}}<el-input v-model="answerSet[order].ans.text[index]" placeholder="" class="blank" :disabled="true"></el-input></span>
                              </span>
                              <span v-else>
                                  <span>{{titleBlank}}(必填)<br></span>
                              </span>
                          </span>
                      </p>
                  </div>
                  <div v-else-if="questItem.questionType=='11'">
                      <p class="questItem-title">
                          <span>{{questItem.order+1}}、</span>
                          <span v-for="(titleBlank,index) in questItem.content.title" :key=index class="titleBlank">
                              <span v-if="index!=questItem.content.title.length-1">
                                  <span>{{titleBlank}}<el-input v-model="answerSet[order].ans.text[index]" placeholder="" class="blank" :disabled="true"></el-input></span>
                              </span>
                              <span v-else>
                                  <span>{{titleBlank}}(选填)</span>
                              </span>
                          </span>
                      </p>
                  </div>
              </div>
           </el-col>
         </el-main>
      </el-container>
    </div>
</template>
<script>
export default {
  props: {
  },
  data () {
    return {
      questionnaireID: this.$route.params.questionnaireID,
      answerUid: this.$route.params.answerUID,
      ip: '',
      title: '',
      description: '',
      questionnaireData: '',
      answer: '',
      answerSet: [],
      customColor: '#409eff',
      percentage: 0,
      showText: false,
      seen: false
    }
  },
  methods: {
    getQuesnaire: function () {
      return this.$axios({
        url: 'https://afo3wm.toutiao15.com/getQuesnaire',
        method: 'get',
        params: {
          questionnaireID: this.questionnaireID
        }
      })
    },
    getAns: function () {
      return this.$axios({
        url: 'https://afo3wm.toutiao15.com/getAnsByQnID',
        method: 'get',
        params: {
          questionnaireID: this.questionnaireID
        }
      })
    },
    toLabel: function (array1, array2) {
      let rs = []
      if (array1 instanceof Array) {
        for (let i = 0; i < array1.length; i++) {
          rs.push(array2[array1[i]])
        }
      } else {
        rs.push(array2[array1])
      }
      return {choice: rs}
    }
  },
  created: function () {
    const loading = this.$loading({
      lock: true,
      text: 'Loading',
      spinner: 'el-icon-loading',
      background: 'rgba(0, 0, 0, 0.7)'
    })
    this.$axios.all([this.getQuesnaire(), this.getAns()]).then(this.$axios.spread((response1, response2) => {
      let flag = 1
      for (let i = 0; i < response2.data.result.length; i++) {
        if (response2.data.result[i].answerUID === this.answerUid) {
          flag = 0
          this.answer = response2.data.result[i].answers
          break
        }
      }
      if (flag === 1) {
        this.$message({
          showClose: true,
          message: '问卷不存在',
          type: 'warning'
        })
        loading.close()
        this.$router.push('/non-existing')
        return
      }
      this.seen = true
      this.title = response1.data.Questionnaire.title
      this.description = response1.data.Questionnaire.description
      this.questionnaireData = response1.data.Questions
      for (let i = 0; i < this.questionnaireData.length; i++) {
        switch (this.questionnaireData[i].questionType) {
          case 0:
            this.answerSet.push({ans: {choice: ''}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 1:
            this.answerSet.push({ans: {choice: ''}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          case 2:
            this.answerSet.push({ans: {choice: []}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 3:
            this.answerSet.push({ans: {choice: []}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          case 4:
            this.answerSet.push({ans: {text: ''}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 5:
            this.answerSet.push({ans: {text: ''}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          case 6:
            this.answerSet.push({ans: {text: ''}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 7:
            this.answerSet.push({ans: {text: ''}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          case 8:
            this.answerSet.push({ans: {mark: null}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 9:
            this.answerSet.push({ans: {mark: null}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          case 10:
            this.answerSet.push({ans: {text: new Array(this.questionnaireData[i].content.title.length - 1)}, mustfill: 'true', type: this.questionnaireData[i].questionType})
            break
          case 11:
            this.answerSet.push({ans: {text: new Array(this.questionnaireData[i].content.title.length - 1)}, mustfill: 'false', type: this.questionnaireData[i].questionType})
            break
          default:
            break
        }
      }
      for (let i = 0; i < this.answer.length; i++) {
        console.log(this.answer[i])
        if (this.answer[i].questiontype === 2 || this.answer[i].questiontype === 3) {
          this.answer[i].Anscontent = this.toLabel(this.answer[i].Anscontent.choice, this.questionnaireData[this.answer[i].order].content.choice)
        }
        this.answerSet[this.answer[i].order].ans = this.answer[i].Anscontent
      }
    }))
      .catch((error) => {
        console.log(error)
        loading.close()
        this.$message({
          showClose: true,
          message: '与远程服务器的连接发生致命错误，提交失败',
          type: 'error'
        })
        this.$router.push('/non-existing')
      })
    loading.close()
  },
  mounted: function () {
  }
}
</script>
<style scoped>
    .titleBlank{
    }
    .blank {
        width:50px;
        border-top-width: 0px;
        border-left-width: 0px;
        border-right-width: 0px;
        border-bottom-width: 1px;
    }
    .question{
    }
    .description {
        margin-left: auto;
        margin-right: auto;
        width: 90%;
        text-align: center;
        font-size: 18px;
    }
    .questItem{
        margin-top: 50px;
        margin-left: auto;
        margin-right: auto;
        width: 90%;
        text-align: left;
    }
    .choiceItem{
    }
    #commitedButton{
        font-size: 20px;
        width: 50%;
    }
    .el-radio {
      margin-bottom: 20px;
    }
    .el-checkbox {
      margin-bottom: 20px;
    }
    .el-rate {
    }
</style>
