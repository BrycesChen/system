<template>
  <div>
    <div class="main">
      <div class="loginBox">
        <div class="picBox">
          <img src="../assets/loginBg.jpg" alt="">
        </div>
        <div class="contentBox">
          <p class="title">XXXXXX系统</p>
          <p class="description">XXXXXX系统</p>
          <div>
            <Row style="margin-top: 20px">
              <Form ref="formInline" :model="formInline" :rules="ruleInline" inline>
                <i-col span="24" style="height: 62px;">
                  <FormItem prop="user">
                    <i-Input type="text" style="width: 310px" v-model="formInline.user" placeholder="Username">
                      <Icon type="ios-person-outline" slot="prepend"></Icon>
                    </i-Input>
                  </FormItem>
                </i-col>

                <i-col span="24" style="height: 62px">
                  <FormItem prop="password">
                      <i-Input type="password" style="width: 310px"  v-model="formInline.password" placeholder="Password">
                        <Icon type="ios-lock-outline" slot="prepend"></Icon>
                      </i-Input>
                  </FormItem>
                </i-col>
                <FormItem style="display: block">
                  <Button type="primary" style="width: 100%" @click="handleSubmit('formInline')">Signin</Button>
                </FormItem>
              </Form>
            </Row>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      formInline: {
        user: '',
        password: ''
      },
      ruleInline: {
        user: [
          { required: true, message: '请输入用户名', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { type: 'string', min: 6, message: '密码不得小于六位', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    handleSubmit (name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          this.$Message.success('Success!')
          this.$router.push({path: '/homeIndex'})
        } else {
          this.$Message.error('Fail!')
        }
      })
    }
  }
}
</script>

<style scoped>
  .loginBox {
    display: flex;
    transform: translate(-50%,-50%);
    position: absolute;
    top: 50%;
    left: 50%;
    height: 420px;
    width: 802px;
    box-shadow: 0 0 16px 0 rgba(0,92,205,.15)
  }
  .picBox{
    display: inline-block;
    width: 40%;
    min-width: 210px;
    max-width: 320px;
    vertical-align: top;
  }
  .picBox img{
    width: 100%;
    height: 100%;
    vertical-align: middle;
  }
  .contentBox{
    display: inline-block;
    width: 60%;
    height: 100%;
    font-family: PingFangSC-Medium;
    font-weight: 700;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    padding: 0 10%;
    text-align: left;
  }
  .title {
    margin-top: 25%;
    font-size: 24px;
    color: #000;
  }
  .description{
    font-size: 14px;
    color: #000;
    margin-bottom: 1em;
  }
</style>
