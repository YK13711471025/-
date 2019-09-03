<template>
  <div id="app">
    <div class="code" @click="refreshCode">

      <!-- ：fresh：父组件向子组件传送刷新验证码的信号；
    @makedCode：子组件向父组件传送验证码的值-->

      <s-identify :fresh="flag" @makedCode="getMakedCode"></s-identify>
    </div>

    <div class="code" @click="refreshCodetwo">

      <!-- ：fresh：父组件向子组件传送刷新验证码的信号；
    @makedCode：子组件向父组件传送验证码的值-->

      <yanzhengma :freshtwo="flagtwo" @makedCodetwo="getMakedCodetwo"></yanzhengma>
    </div>
    <div>
      <el-button type="text" @click="dialogFormVisible = true">打开嵌套表单的 Dialog</el-button>

      <el-dialog title="举报" :visible.sync="dialogFormVisible">
        <el-form>
          <el-form-item label="举报原因" :label-width="formLabelWidth">
            <el-input v-model="conent" auto-complete="off"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="letgo">确 定</el-button>
        </div>
      </el-dialog>
    </div>

  </div>
</template>
<script>
import SIdentify from "@/components/identify.vue";
import yanzhengma from "@/components/yanzhengma.vue";
export default {
  name: "codetest",
  data() {
    return {
      flag: true, //该值变化，就会触发刷新
      code: "", //刷新后的验证码
      flagtwo: true, //该值变化，就会触发刷新
      codetwo: "", //刷新后的验证码
      input1: "",
      dialogFormVisible: false,
      conent:'',
      formLabelWidth: "120px"
    };
  },
  components: {
    SIdentify,
    yanzhengma
  }, // 验证码初始化
  mounted() {
    this.flag = !this.flag;
    this.flagtwo = !this.flagtwo;
  },
  methods: {
    // 切换验证码
    refreshCode() {
      this.flag = !this.flag;
    },
    refreshCodetwo() {
      this.flagtwo = !this.flagtwo;
    },
    getMakedCode(code) {
      this.code = code;
      console.log("getMakedCode:", this.code);
    },
    getMakedCodetwo(codetwo) {
      this.codetwo = codetwo;
      console.log("getMakedCodetwo:", this.codetwo);
    },
    letgo(){
      this.dialogFormVisible = false
      if(this.conent){
        this.$message({
          message: '举报成功',
          type: 'success'
        });
      }
    }
  }
};
</script>
 

