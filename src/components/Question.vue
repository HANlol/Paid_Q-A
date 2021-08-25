/*
 * @Author: hjj 
 * @Date: 2021-08-25 10:50:22 
 * @Last Modified by: hjj
 * @Last Modified time: 2021-08-25 16:57:57
 */

<template>
    <el-container>
        <el-header>
            <el-input placeholder="请输入内容" v-model="input">
                <el-button slot="append" type="primary" icon="el-icon-search"></el-button>
            </el-input>
            <el-button-group>
                <el-button type="primary" icon="el-icon-s-operation" @click="changeGrid()"></el-button>
                <el-button type="primary" icon="el-icon-menu" @click="changeRow()"></el-button>
            </el-button-group>
        </el-header>
        <el-main>
            <el-row v-show="gridShow" v-for="(r, count) in allUsers/5" :key="r">
                <el-col :span="4" v-for="(o, index) in 5" :key="o" :offset="index > 0 ? 1 : 0">
                    <el-card :body-style="{ padding: '0px' }" shadow="hover">
                        <img src="https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png" class="image">
                        <div style="padding: 14px;">
                            <div class="bottom clearfix">
                                <el-button type="text">向他提问</el-button>
                                <el-button type="text">和他聊天</el-button>
                                <div>{{count * 5 + index}}</div>
                            </div>
                        </div>
                    </el-card>
                </el-col>
            </el-row>
            <el-row v-show="rowShow">
            <el-table :data="tableData" style="width: 100%">
                <el-table-column label="从业时长" width="240">
                    <template slot-scope="scope">
                        <i class="el-icon-time"></i>
                        <span style="margin-left: 10px">{{ scope.row.date }}</span>
                    </template>
                </el-table-column>
                <el-table-column label="基本信息" width="240">
                    <template slot-scope="scope">
                        <el-popover trigger="hover" placement="top">
                            <p>姓名: {{ scope.row.name }}</p>
                            <p>负责科目: {{ scope.row.subject }}</p>
                            <div slot="reference" class="name-wrapper">
                                <el-tag size="medium">{{ scope.row.name }}</el-tag>
                            </div>
                        </el-popover>
                    </template>
                </el-table-column>
                <el-table-column label="科目" width="240">
                    <template slot-scope="scope">
                        <i class="el-icon-notebook-1"></i>
                        <span style="margin-left: 10px">{{ scope.row.subject }}</span>
                    </template>
                </el-table-column>
                <el-table-column label="价格" width="240">
                    <template slot-scope="scope">
                        <i class="el-icon-coin"></i>
                        <span style="margin-left: 10px">{{ scope.row.price }}</span>
                    </template>
                </el-table-column>
                <el-table-column label="操作">
                    <template slot-scope="scope">
                        <el-button size="mini" type="primary" @click="handleQue(scope.$index, scope.row)">提问</el-button>
                        <el-button size="mini" type="primary" @click="handleChat(scope.$index, scope.row)">聊天</el-button>
                    </template>
                </el-table-column>
            </el-table>
            </el-row>
        </el-main>
    </el-container>
</template>

<script>
export default({
    name: 'Question',
    data () {
        return{
            select: '',
            input: '',
            gridShow: true,
            rowShow: false,
            allUsers: 15,
            tableData: [{
                date: '20months',
                name: '张三',
                subject: '数学',
                price: '$10'
                }, {
                date: '10months',
                name: '李四',
                subject: '历史',
                price: '$7'
                }, {
                date: '12months',
                name: '王五',
                subject: '英语',
                price: '$8'
                }, {
                date: '6months',
                name: '赵六',
                subject: '政治',
                price: '$15'
                },{
                date: '20months',
                name: '张三',
                subject: '数学',
                price: '$10'
                }, {
                date: '10months',
                name: '李四',
                subject: '历史',
                price: '$7'
                }, {
                date: '12months',
                name: '王五',
                subject: '英语',
                price: '$8'
                }, {
                date: '6months',
                name: '赵六',
                subject: '政治',
                price: '$15'
                },{
                date: '20months',
                name: '张三',
                subject: '数学',
                price: '$10'
                }, {
                date: '10months',
                name: '李四',
                subject: '历史',
                price: '$7'
                }, {
                date: '12months',
                name: '王五',
                subject: '英语',
                price: '$8'
                }, {
                date: '6months',
                name: '赵六',
                subject: '政治',
                price: '$15'
            }]
        }
    },
    methods: {
        changeGrid: function(){
            if(this.gridShow == true){
                this.gridShow = false;
                this.rowShow = true;
            }
        },
        changeRow: function(){
            if(this.rowShow == true){
                this.gridShow = true;
                this.rowShow = false;
            }
        },
        handleQue(index, row) {
            console.log(index, row);
        },
        handleChat(index, row) {
            console.log(index, row);
        }
    }
})
</script>

<style scoped>
    .el-input{
        height: 5vh;
        width: 70vw;
    }

    .el-header{
        line-height: 6vh;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .el-main {
        text-align: center;
        line-height: 20px;
    }

    .button {
        padding: 0;
        float: right;
    }

    .image {
        width: 100%;
        display: block;
    }

    .bottom {
        margin-top: 3px;
        line-height: 12px;
    }

    .clearfix:before,
    .clearfix:after {
        display: table;
        content: "";
    }
    
    .clearfix:after {
        clear: both
    }

    .el-row {
        margin-bottom: 20px;
    }
    
    .el-raw:last-child{
        margin-bottom: 0;
    }

    .el-col {
        border-radius: 4px;
    }
</style>
