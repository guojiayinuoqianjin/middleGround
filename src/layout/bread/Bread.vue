<template>
    <div class='bread'>
        <strong>
            {{curRouteData[curRouteData.length-1] && curRouteData[curRouteData.length-1].name}}
        </strong>
        <el-breadcrumb separator="/" class='el-bread'>
            <!-- <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item> -->
            <el-breadcrumb-item
                v-for='(item,index) in curRouteData'
                :key='index'>{{item.name}}</el-breadcrumb-item>
        </el-breadcrumb>
    </div>
</template>

<script>
		import {store} from 'utils/';
    export default {
        name: 'bread',
        data () {
          return {
            strong:'',
          }
        },
        methods:{
          getPageText(name){
            return name=name.replace('编辑',this.$route.query.id ? '修改' : '添加');
          }
        },
        mounted(){
        },
        created(){
          /*if (this.$route.matched.length) {
            var name=this.$route.matched[this.$route.matched.length-1].meta.name;
            this.strong=this.getPageText(name);
          }*/
        },
        computed: {
				  curRouteData () {
				    return this.$store.state.router.curRouteData || [];
				  }
				},
        watch:{
          $route(to,from){
            this.strong=this.getPageText(to.meta.name);
          }
        }
    }
</script>

<style lang='less'>
    .bread{
        height: 40px;
        line-height: 26px;
        padding: 0 10px;
        .el-bread{
            display: inline-block;
            float: right;
            text-align: right;
            line-height: 26px;
        }
        strong{font-size: 14px;}
    }
    .el-breadcrumb__item__inner a:hover, .el-breadcrumb__item__inner:hover{cursor: default;color: inherit;}
</style>
