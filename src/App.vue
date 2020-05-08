<template>
  <div id="app">
    <div v-if="$route.path !== '/'" class="layout">
      <Layout :style="{minHeight: '100vh'}">
        <Sider collapsible :collapsed-width="78" v-model="isCollapsed">
          <Menu @on-select="select" active-name="homeIndex" theme="dark" width="auto" :class="menuitemClasses">
            <Menu-Item name="homeIndex">
              <Icon type="ios-navigate"></Icon>
              <span>首页</span>
            </Menu-Item>
            <Menu-Item name="template1">
              <Icon type="ios-search"></Icon>
              <span>模板1</span>
            </Menu-Item>
            <Menu-Item name="template2">
              <Icon type="ios-settings"></Icon>
              <span>模板2</span>
            </Menu-Item>
          </Menu>
        </Sider>
        <Layout>
          <Header :style="{background: '#fff', boxShadow: '0 2px 3px 2px rgba(0,0,0,.1)'}">
            <div>
              <Row type="flex" justify="end" align="middle">
                <Dropdown transfer trigger="click" @on-click="handleClickUserDropdown">
                  <Avatar style="background: #619fe7;margin-left: 10px;"></Avatar>
                  <a href="javascript:void(0)">
                    <span class="main-user-name">用户名</span>
                    <Icon type="arrow-down-b"></Icon>
                  </a>
                  <DropdownMenu slot="list">
                    <DropdownItem name="ownSpace">个人中心</DropdownItem>
                    <DropdownItem name="updatePassword" divided>修改密码</DropdownItem>
                    <DropdownItem name="logout" divided>退出登录</DropdownItem>
                  </DropdownMenu>
                </Dropdown>
              </Row>
            </div>
          </Header>
          <i-Content :style="{padding: '0 16px 16px'}">
            <Breadcrumb :style="{margin: '16px 0', textAlign: 'left'}">
              <BreadcrumbItem to="/homeIndex">Home</BreadcrumbItem>
            </Breadcrumb>
            <Card>
              <div style="height: 600px">
                <router-view/>
              </div>
            </Card>
          </i-Content>
        </Layout>
      </Layout>
    </div>
    <div>
      <router-view/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      isCollapsed: false
    }
  },
  computed: {
    rotateIcon () {
      return [
        'menu-icon',
        this.isCollapsed ? 'rotate-icon' : ''
      ]
    },
    menuitemClasses () {
      return [
        'menu-item',
        this.isCollapsed ? 'collapsed-menu' : ''
      ]
    }
  },
  methods: {
    select (name) {
      this.$router.push({path: name})
    },
    handleClickUserDropdown (name) {
      if (name === 'ownSpace') {
        this.$Message.info('个人中心')
      } else if (name === 'logout') {
        this.$Message.info('修改密码')
      } else if (name === 'updatePassword') {
        this.$Message.info('退出登录')
      }
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  .header-user {
    width: 112px;
    height: 54px;
    position: absolute;
    right: 10px;
    cursor: pointer;
  }
  .header-user img {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    line-height: 54px;
    margin-right: 10px;
    margin-top: 15px;
  }
  .header-user span{
    font-size: 14px;
    color: #000;
  }
  .menu-item span{
    display: inline-block;
    overflow: hidden;
    width: 69px;
    text-overflow: ellipsis;
    white-space: nowrap;
    vertical-align: bottom;
    transition: width .2s ease .2s;
  }
  .menu-item i{
    transform: translateX(0px);
    transition: font-size .2s ease, transform .2s ease;
    vertical-align: middle;
    font-size: 16px;
  }
  .collapsed-menu span{
    width: 0px;
    transition: width .2s ease;
  }
  .collapsed-menu i{
    transform: translateX(5px);
    transition: font-size .2s ease .2s, transform .2s ease .2s;
    vertical-align: middle;
    font-size: 22px;
  }
</style>
