<template>
  <el-container>
    <el-header height="3em">
      <el-row :gutter="24">
        <el-col :span="18">
          <div class="grid-content">
            <div class="title">金鼎矿业在线IP表查询系统</div>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="grid-content user">
            <div class="login">
              <el-popover placement="bottom" width="400" trigger="click">
                <div class="form-title">
                  登录
                </div>
                <el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">
                  <el-form-item label="用户名">
                    <el-input v-model="formLabelAlign.name"></el-input>
                  </el-form-item>
                  <el-form-item label="密码">
                    <el-input v-model="formLabelAlign.region"></el-input>
                  </el-form-item>
                  <el-form-item>
                    <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
                    <el-button @click="resetForm('ruleForm')">找回</el-button>
                  </el-form-item>
                </el-form>
                <el-button slot="reference">登录</el-button>
              </el-popover>
            </div>
            <div class="logoff">
              <el-button>注销</el-button>
            </div>
          </div>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
        <el-menu :default-openeds="['1', '3']">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-message"></i>用户管理
            </template>
            <el-menu-item-group>
              <template slot="title">管理员设置</template>
              <el-menu-item index="1-1">选项1</el-menu-item>
              <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="权限设置">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项4</template>
              <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-menu"></i>主题设置
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="2-1">选项1</el-menu-item>
              <el-menu-item index="2-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="2-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-setting"></i>导航三
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="3-1">选项1</el-menu-item>
              <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main>
        <el-button @click="fetchData">获取</el-button>
        <el-table :data="tableData" style="width: 100%">
          <el-table-column prop="serialNumber" label="序号"></el-table-column>
          <el-table-column prop="ipAddress" label="ip地址"></el-table-column>
          <el-table-column prop="address" label="安装位置"></el-table-column>
          <el-table-column prop="password" label="密码"></el-table-column>
          <el-table-column prop="thoroughfare" label="通道"></el-table-column>
          <el-table-column prop="state" label="状态"></el-table-column>
          <el-table-column prop="Number" label="编号"></el-table-column>
        </el-table>
        <el-footer>Footer</el-footer>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      labelPosition: "right",
      formLabelAlign: {
        name: "",
        region: "",
        type: ""
      },
      tableData: [
        {
          serialNumber: 1,
          ipAddress: "192.168.1.1",
          address: "主井",
          password: "jdky2020",
          thoroughfare: 1,
          state: "在线",
          Number: 1
        }
      ],
      currentTitle: "用户管理"
    };
  },
  methods: {
    fetchData() {
      this.axios.defaults.baseURL = "http://192.168.1.6:3000";
      this.axios
        .get("/")
        .then(response => {
          this.tableData.push(response.data);
          console.log(response.data);
        })
        .catch(error => {
          console.log("error");
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.el-header {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  font-size: 28px;
  line-height: 3em;
  .title {
    text-align: left;
    font-weight: bold;
  }

  .user {
    width: 150px;
    font-size: 16px;
    float: right;
    .login {
      display: inline-block;
      // padding-left: 16px;
      // padding-right: 16px;
    }
    .logoff {
      display: inline-block;
      // padding-left: 16px;
      // padding-right: 16px;
    }
  }
}
.el-footer {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
}
.form-title {
  text-align: center;
  padding:15px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: left;
  line-height: 3em;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  line-height: 3em;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>
