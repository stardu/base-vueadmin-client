<template>
    <div class="header-top">
        <BreadcrumbBar />
        <div class="header-right">
            <div class="box">
                <div class="user-menu">
                    <i class="iconfont icon-xiaoxi"></i>
                    <span class="vertical-line"></span>
                    <img class="user-avatar" v-image-preview src="../../../assets/imgs/default-avatar.png" alt="user">
                    <el-dropdown @command="handleCommand">
                        <div class="user-content">
                            <h5>暂无</h5>
                            <p class="user-name">超级管理员</p>
                        </div>
                        <el-dropdown-menu slot="dropdown">
                            <el-dropdown-item command="personCenter">个人中心</el-dropdown-item>
                            <el-dropdown-item command="logout">退出系统</el-dropdown-item>
                        </el-dropdown-menu>
                    </el-dropdown>
                </div>
            </div>
        </div>
    </div>
</template>

<script  type="text/ecmascript-6">
import BreadcrumbBar from './BreadcrumbBar.vue';
import Cookies from 'js-cookie';

export default {
    name: 'HeaderTop',
    components: {
        BreadcrumbBar
    },
    data () {
        return {
            defaultLogo: '../../../static/img/logo.png',
            imgUrl: '../../../static/img/default-avatar.png'
        };
    },

    methods: {

        //下拉回调
        handleCommand (command) {
            switch (command) {
            case 'logout': //退出系统
                this.logout(); break;
            case 'personCenter':
                this.showDetailDialog(); break;
            }
        },

        //退出系统
        logout () {
            this.$confirm('您确定要退出系统吗?', '提示', {
                cancelButtonText: '取消',
                confirmButtonText: '确定',
                type: 'warning',
                center: true,
                customClass: 'bg-warning'
            }).then(() => {
                Cookies.remove('adminToken');
                this.$router.push(`/login`);
            }).catch(() => {
                this.$message({
                    type: 'info',
                    message: '已取消操作'
                });
            });
        }
    }
};
</script>
<style lang="less" scoped>
@header-height: 55px;
.header-top {
  display: flex;
  background: #fff;
  border-bottom: 1px solid #ccc;
  .header-right {
    flex: 1;
    .box {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      height: @header-height;
      .user-menu {
        min-width: 166px;
        color: #fff;
        .icon-xiaoxi,
        .vertical-line {
          font-size: 26px;
          vertical-align: middle;
        }
        .vertical-line {
          display: inline-block;
          width: 1px;
          height: 28px;
          margin: 0 12px;
          background-color: #fff;
        }
        .user-avatar {
          width: 32px;
          display: inline-block;
          vertical-align: middle;
        }

        .el-dropdown {
          vertical-align: middle;
          color: #000;
          margin-left: 8px;
          font-size: 12px;
          cursor: pointer;
          .user-name {
            margin-top: 5px;
          }
        }
      }
    }
  }
}
</style>
