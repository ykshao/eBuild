<template>
<div class="project_add">
    <div class="mod_tit">全局设置</div>
    <div class="row">
        <el-checkbox v-model="transRem">开启px2rem</el-checkbox>
        , 1rem = <el-input class="ipt_ratio" v-model="myConfig.remRatio" size="mini"></el-input> px
    </div>
    <!-- <div class="row">
        <el-checkbox v-model="myConfig.checkSyntax">同步前进行语法检查</el-checkbox>
    </div> -->
    <div class="row">
        <el-checkbox v-model="myConfig.autoPrefix">CSS补齐前缀</el-checkbox>
    </div>
    <div class="row">
        <el-checkbox v-model="myConfig.codeMinify">代码压缩</el-checkbox>
    </div>
    <div class="row">
        <el-checkbox v-model="myConfig.removeProtocolHead">去协议头</el-checkbox>
    </div>

    <div class="row">
        <div class="row_btn">
            <el-button type="primary" @click="save">保存</el-button>
        </div>
    </div>
</div>
</template>

<script>
    import {mapGetters, mapActions } from 'vuex'

    export default {
        data(){
            return {
                transRem: false,
                myConfig: {
                    autoPrefix:false,
                    remRatio: 50,
                    codeMinify: false,
                    removeProtocolHead: true
                },
            }
        }
        ,mounted() {
            for (var key in this.config){
                if (this.config.hasOwnProperty(key)) {
                    this.myConfig[key] = this.config[key]
                }
            }
            if (1*this.config['remRatio']) {
                this.transRem = true
            }
        }
        ,computed:{
            ...mapGetters(['config'])
        }
        ,methods: {
            ...mapActions(['saveConfig'])
            ,save() {
                if (!this.transRem) {
                    this.myConfig.remRatio = 0
                }
                this.saveConfig(this.myConfig)
                this.$router.back(-1)
            }
        }
    }
</script>

<style scoped>
    .mod_tit {padding-top: 20px;font-size: 22px;padding-bottom:10px;color: #555;}
    .project_add {width: 500px;margin: 0 auto;padding: 20px 0; font-size: 14px;}
    .project_add .row {margin: 20px 0;}
    .project_add .row_btn {padding: 15px 0 0;}
    .project_add .row_btn button {margin-right: 10px;}
    .project_add .sel {width:100%;}

    .ipt_ratio {width: 70px;}
    .ipt_ratio input {padding: 0 5px;text-align: center;}

</style>

