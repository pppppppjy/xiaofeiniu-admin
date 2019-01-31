<template>
    <div class="Main">
    <el-container>
      <!-- 左侧菜单栏 -->
      <el-aside width="200px">
          <el-menu :default-active="defaultActive" :default-openeds="defaultOpendes" :unique-opened="true" :router="true">
              <!-- 菜单项1 -->
              <el-menu-item index="/settings">
                  <i class="el-icon-setting"></i>
                  <span slot="title">全局设置</span>
              </el-menu-item>
              <!-- 菜单项2 -->
              <el-submenu index="table">
                  <template slot="title">
                    <i class="el-icon-menu"></i>
                    <span>桌台管理</span>
                  </template>
                  <el-menu-item-group>
                    <el-menu-item index="/table/list">桌台列表</el-menu-item>  
                    <el-menu-item index="/table/add">添加桌台</el-menu-item>  
                    <el-menu-item index="/table/delete">删除桌台</el-menu-item>  
                  </el-menu-item-group>
              </el-submenu>
              <!-- 菜单项3 -->
              <el-menu-item index="/category/list">
                  <i class="el-icon-message"></i>
                  <span slot="title">菜品类别</span>
              </el-menu-item>
              <!-- 菜单项4 -->
               <el-submenu index="dish">
                  <template slot="title">
                    <i class="el-icon-tickets"></i>
                    <span>菜品管理</span>
                  </template>
                  <el-menu-item-group>
                    <el-menu-item index="/dish/list">所有列表</el-menu-item>  
                    <el-menu-item index="/dish/add">添加桌台</el-menu-item>  
                    <el-menu-item index="/dish/delete">删除桌台</el-menu-item>  
                    <el-menu-item index="/dish/update">修改桌台</el-menu-item> 
                  </el-menu-item-group>
              </el-submenu>
              <!-- 菜单项5 -->
              <el-menu-item index="/order/list">
                  <i class="el-icon-date"></i>
                  <span slot="title">订单列表</span>
              </el-menu-item>
              <!-- 菜单项6 -->
              <el-menu-item index="/security">
                  <i class="el-icon-bell"></i>
                  <span slot="title">安全管理</span>
              </el-menu-item>

          </el-menu>
      </el-aside>
      <el-container>
          <!-- 顶部的信息栏 -->
          <el-header height="60px">
            <!-- <MainHeader></MainHeader> -->
            <main-header></main-header>
          </el-header>
          <!-- 主体部分 -->
          <el-main>
              <router-view></router-view>
          </el-main>
      </el-container>
    </el-container>
    </div>
</template>
<script>
import MainHeader from '../components/MainHeader'
export default {
    data(){  //数据属性
        return {
           
        }
    },
    computed:{  //计算属性 = 数据属性 + 操作方法
      defaultActive(){
          //用户当前访问哪页,就把对应的菜单项置为"当前激活项"
          return this.$route.path;
      },
          defaultOpendes(){
              if(this.$route.path.indexOf('/table')==0){
                  //用户当前在浏览器/table/xxx菜单项
                  return ['table'];
              }else if(this.$route.path.indexOf('/dish')==0){
                  return ['dish'];
              }
              return [];
          }             
    },
    //create/mounte/update/destory
    beforeCreate(){
        //组件创建之前先要检查是否已经登录为管理员刷新跳回登录页面
        if(!this.$store.state.adminName){
           this.$router.push('/login');//未登录则跳转
        }
    },
    components:{  //当前组件内部使用过的子组件列表
       MainHeader
    }
}
</script>