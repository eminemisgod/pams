<style>
.tip {
    padding: 8px 16px;
    background-color: #ecf8ff;
    border-radius: 4px;
    border-left: 5px solid #67c23a;
    margin: 20px 0;
    min-height: 23px;
    margin-top: -2px;
}

.top-style span {
    color: #fff !important;
}

.top-style {
    margin-left: 10px !important;
}

.bor-style {
    background: rgba(0, 0, 0, 0.28) !important;
    padding: 10px 30px;
    margin-left: -40px;
    margin-right: -40px;
    margin-top: -10px;
    margin-bottom: 25px;
    box-shadow: 0px 2px 3px rgba(255, 255, 255, 0.23);
}

.button-creat {
    float: right;
    margin-top: -3px;
}

.input-style {
    margin-right: 10px
}

.chose-type {
    width: 160px;
    border-right: 1px #999 solid
}

.chose-type2 {
    width: 160px;
    border-right: 1px #999 solid;
    margin-left: 20px !important;
}

.dialog-width>div {
    width: 70%
}

.input-with-select {}

.el-select .el-input {
    width: 130px;
}

.input-with-select .el-input-group__prepend {
    background-color: #fff;
}

.select-width1>div>div>div {
    width: 120px !important
}

.select-width2>div {
    width: 100% !important
}

.select-width3>div {
    width: 30% !important
}

.fr-body {
    background: rgba(10, 10, 10, 0.03)
}

.i-font-s {
    font-size: 19px;
    color: #67c23a;
    position: relative;
    top: 2px
}

.i-font-s-n {
    font-size: 19px;
    color: #b7b9b7;
    position: relative;
    top: 2px;
    pointer-events: none;
}

.over-s {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 185px;
}

.div-list-user {
    margin-left: 0px;
    width: 80px;
    display: inline-block;
    overflow: hidden;
    border-bottom: 0px solid #dcffca;
    text-align: left;
}
.over-user {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: 85px;
}
.div-list-appid {
    margin-left: 0px;
    width: 85px;
    display: inline-block;
    overflow: hidden;
    border-bottom: 0px solid #dcffca;
    text-align: center;
    background: #edffe5;
    border-radius: 4px
}
.div-list-time {
    margin-left: 0px;
    width: 70px;
    display: inline-block;
    overflow: hidden;
    text-align: center;
}
.div-list-version {
    display: inline-block;
    border-bottom: 0px solid #dcffca;
    text-align: left;
    margin-left: 8px;
    top: 2px;
    position: relative;    
}

.div-list-send {
    display: inline-block;
    overflow: hidden;
    border-bottom: 0px solid #dcffca;
    margin-left: 10px;
    position: relative;
    top: 2px;
}
.div-list-send-i {
    display: inline-block;
    margin-left: 10px;
    position: relative;
    top: -4px;
}
.rep-border{background: #a3f280 !important;}
.hand-s {
    cursor: pointer
}

.color-s {
    color: #03b04c !important
}

.color-h {
    color: #909399 !important
}

.color-table {
    color: #555
}
.select-e{
    width:95px
}
.select-e div{
    width:95px !important;
}
.select-e div input{
    height: 25px !important;
}
.item-line{
    position: relative;
    top: 3px;
    line-height: 20px;}
.item-background{background: #b9e6a4;}
.color-second {
    color: #f00
}
.color-minute {
    color: #f94c4c
}
.color-hour {
    color: #e98e8e
}
.color-day {
    color: #967a7a
}
.taskversion{    border: 1px solid #edffe5;
    background: #efefef;
    padding: 4px 0px;
    width: 86%;
    border-radius: 4px;}
</style>

<template>
    <div>
        <div class="bor-style">
            <el-breadcrumb separator-class="el-icon-arrow-right" class="top-style">
                <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                <el-breadcrumb-item :to="{ path: '/ProjectAll' }">发布计划</el-breadcrumb-item>
                <el-breadcrumb-item>任务列表</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="tip">
            <span style="position: relative;top: 0px;">{{ProjectName}}</span>
            <el-button type="success" class="button-creat" size="mini" @click="AddTask()">新增任务</el-button>

            <el-dialog title="新增标签" :visible.sync="dialogTagVisible">
                <el-form :model="NewTag">
                    <el-form-item label="标签名称：" :label-width="formLabelWidth">
                        <el-input v-model="NewTag.TagName" auto-complete="off" style="width:70%;"></el-input>
                    </el-form-item>
                </el-form>
                <div slot="footer" class="dialog-footer" style="position:relative;left:-4%;">
                    <el-button @click="dialogTagVisible = false">取 消</el-button>
                    <el-button type="primary" @click="AddTag()">确 定</el-button>
                </div>
            </el-dialog>

            <el-dialog title="新增/编辑 任务" :visible.sync="dialogFormVisible" class="dialog-width">
                <el-form ref="dynamicValidateForm">
                    <el-form-item label="任务名称：" :label-width="formLabelWidth">
                        <el-input v-model="TaskData.TaskName" style="width:90%;"></el-input>
                    </el-form-item>

                    <el-form-item label="发布详情：" :label-width="formLabelWidth">
                        <el-date-picker v-model="TaskData.TaskReleaseTime" type="date" :default-time="['09:00:00','09:00:00']"  value-format="yyyy-MM-dd" placeholder="选择日期" style="width:36.3%;">
                        </el-date-picker>

                        <el-select v-model="TaskData.TaskGrade" placeholder="任务级别" class="select-width2">
                            <el-option v-for="item in Grades" :key="item.GradeId" :label="item.text" :value="item.GradeId">
                            </el-option>
                        </el-select>

                        <el-select v-model="TaskData.TagId" placeholder="标签" class="select-width2">
                            <el-option v-for="item in Tags" :key="item.TagId" :label="item.text" :value="item.TagId">
                            </el-option>
                        </el-select>

                        <el-button type="success" plain @click="dialogTagVisible = true">新增标签</el-button>

                    </el-form-item>

                    <el-form-item v-for="(detail, index) in TaskData.TaskDetail" :label-width="formLabelWidth" :label="'发布应用' + index+'：'" :key="detail.key" :prop="'TaskDetail.' + index + '.value'">
                        <el-input placeholder="请输入..." v-model="detail.TaskAppId" class="input-with-select select-width1" style="width:29%;">
                            <el-select v-model="detail.TaskAppIdType" slot="prepend" placeholder="请选择">
                                <el-option v-for="item in TaskApps" :key="item.AppID" :label="item.AppName" :value="item.AppID">
                                </el-option>
                            </el-select>
                        </el-input>
                        <el-input placeholder="请输入..." v-model="detail.TaskVersion"  style="width:35%;">
                            <template slot="prepend">版本号</template>
                        </el-input>
                        <el-input placeholder="请输入..." v-model="detail.DevMember" style="width:18%;">
                            <template slot="prepend">开发人</template>
                        </el-input>
                        </el-input>
                        <el-button @click.prevent="removeDomain(detail)" type="danger" plain>删除</el-button>
                    </el-form-item>

                    <el-form-item>
                        <el-button @click="addDomain" style="position:relative;left:46%" type="success" plain round size="small">新增发布应用</el-button>
                    </el-form-item>
                    <el-form-item label="相关人员：" :label-width="formLabelWidth">

                        <el-input placeholder="请输入..." v-model="TaskData.TestMember" style="width:30%;">
                            <template slot="prepend">测试</template>
                        </el-input>
                        <el-input placeholder="请输入..." v-model="TaskData.Demander" style="width:30%;">
                            <template slot="prepend">需求方</template>
                        </el-input>
                        <el-input placeholder="请输入..." v-model="TaskData.Acceptance" style="width:30%;">
                            <template slot="prepend">验收方</template>
                        </el-input>

                    </el-form-item>

                    <el-form-item label="验收结果：" :label-width="formLabelWidth" autosize style="width:92%;">
                        <el-input type="textarea" autosize placeholder="请输入内容" v-model="TaskData.TestResult" :autosize="{ minRows: 2, maxRows: 6}">
                        </el-input>
                    </el-form-item>

                    <el-form-item label="备注：" :label-width="formLabelWidth" autosize style="width:92%;">
                        <el-input type="textarea" autosize placeholder="请输入内容" v-model="TaskData.Mark" :autosize="{ minRows: 2, maxRows: 6}">
                        </el-input>
                    </el-form-item>

                </el-form>
                <div slot="footer" class="dialog-footer">
                    <el-button @click="dialogFormVisible = false">取 消</el-button>
                    <el-button type="primary" @click="confirmAdd()">确 定</el-button>
                </div>
            </el-dialog>

        </div>
        <div style="" class="">
            <el-table :data="tableDatas" style="width: 100%;" border header-cell-class-name="color-h" :max-height="rollHight" cell-class-name="color-table">
                <el-table-column prop="TaskReleaseTime" label="发布日期" sortable fixed width="105" align="center" class-name="fr-body">
                </el-table-column>

                <el-table-column label="需求内容" fixed width="180" align="center" class-name="fr-body hand-s color-s">
                    <template slot-scope="scope">
                        <span @click="EditTask(scope.row.TaskId)">{{ scope.row.TaskName }}</span>
                    </template>
                </el-table-column>

                <el-table-column prop="TagId" label="标签" width="120" :formatter="transTag" :filters="Tags" :filter-method="filterTag" filter-placement="bottom-end" align="center">
                </el-table-column>

                <el-table-column prop="TaskGrade" label="级别" :formatter="transTaskGrade" width="65" align="center">
                </el-table-column>

                <el-table-column prop="TestMember" label="测试人员" width="95" align="center">
                </el-table-column>
                <el-table-column label="研发相关" width="650" align="center">
                    <template slot-scope="scope">
                        <div class="item-line" v-for="tem in scope.row.TaskDetail" :class="{'item-background': isRepeatLine(tem.TaskDetailId)}">
                            <div class="div-list-user">
                                <i class="iconfont icon-user1 i-font-s"></i>
                                <span>{{ tem.DevMember }}</span>
                            </div>

                            <div class="div-list-appid" :class="{'rep-border': isRepeat(tem.TaskAppId)}" @click="getRepeat(tem.TaskAppId)">
                                <el-tooltip effect="dark" :content="tem.TaskAppId"  :disabled="tem.TaskAppId && tem.TaskAppId.length<11" placement="top-start">
                                    <div class="over-user">
                                        <span>{{ tem.TaskAppId }}</span>
                                    </div>
                                </el-tooltip>
                            </div>

                            <div class="div-list-time" :class="{'color-second': tem.TimeGrade=='s','color-minute': tem.TimeGrade=='m','color-hour': tem.TimeGrade=='h','color-day': tem.TimeGrade=='d'}">
                                    <div class="over-user">
                                        <span>{{ tem.TimeGradeValue }}{{tem.TimeGrade}}之前</span>
                                    </div>
                            </div>

                            <div class="div-list-version">
                                <el-tooltip effect="dark" :content="tem.TaskVersion"  :disabled="tem.TaskVersion && tem.TaskVersion.length<20" placement="top-start">
                                    <div class="over-s">
                                        <i class="iconfont icon-jinbi i-font-s"></i>
                                        <input type="text" v-model="tem.TaskVersion"  class="taskversion" @blur="changeTaskVersion(scope.row.TaskId,tem.TaskDetailId,tem.TaskVersion)"/>
                                    </div>
                                </el-tooltip>
                            </div>

                            <div class="div-list-send">
                                <i class="iconfont el-icon-caret-right i-font-s"></i>
                                <el-select v-model="tem.NowEnvironment"  class="select-e" :change="changeEnvironment(scope.row.TaskId,tem.TaskDetailId,tem.NowEnvironment)">
                                    <el-option v-for="eitem in Environment" :key="eitem.eid" :label="eitem.text" :value="eitem.eid">
                                    </el-option>
                                </el-select>

                            </div>        

                            <div class="div-list-send-i" @click="toSend(tem.TaskAppIdType,tem.TaskAppId,tem.TaskVersion)">
                                <i class="iconfont el-icon-upload hand-s" v-bind:class="sendClass(tem.TaskAppId)"></i>
                                <!-- icon-mn_fasong_fill -->
                            </div>
                        </div>
                    </template>
                </el-table-column>

                <el-table-column prop="TaskId" label="需求 / 验收方" :formatter="transTaskDA" width="120" align="center">
                </el-table-column>

                <el-table-column prop="TestResult" label="生产验收结果" fit align="center" min-width="220">
                </el-table-column>

            </el-table>
        </div>

    </div>
</template>

<script>
import { setCookie, getCookie } from 'cookie';


function getTpl() {
    return {
        TaskId: "",
        TaskName: "",
        TaskReleaseTime: "",
        TaskGrade: 0,
        TagId: '',
        Demander: "",
        Acceptance: "",
        TestMember: "",
        TestResult: "",
        Mark: "",
        TaskDetail: [{
            TaskDetailId: 0,
            DevMember: '',
            TaskVersion: '',
            TaskAppId: '',
            TaskAppIdType: 1,
        },],
    }
}

export default {
    data() {
        return {

            NewTag: {
                TagName: '',
            },
            SameData: {},
            cf: [{100007704:[6]},{100002703:[10,4]}],
            cff: {100007704: [6],100002703: [10,4],100002142: [10,4]},
            repLine:[],//重复的，需要高亮的line的detail id
            dialogTagVisible: false,
            dialogTableVisible: false,
            dialogFormVisible: false,
            formLabelWidth: '120px',
            rollHight: 0,
            NowData: {},
            TaskData: {},
            //OnChangeDetail:[],//发生变动的details
            Environment: [{ eid : 0, text: '未提测' }, { eid : 1, text: 'FAT' },{ eid : 2, text: 'UAT' },{ eid : 3, text: '生产' },],
            Grades: [{ GradeId: 0, text: '常规' }, { GradeId: 1, text: '紧急' }],
            TaskApps: [],
            ProjectId: getCookie('ProjectId'),
            ProjectName: "",
            Tags: [],
            tableDatas: [],
            delDatas: [],//记录被删除的条目
        }
    },
    created() {
        this.rollHight = window.innerHeight - 185;
        this.getCookieProjectId();
        //setCookie('ProjectId', 1, 600000);//把sid写入
        this.getList();
        this.getTagList();
        this.getAppConfig();
    },

    methods: {
        getAppConfig(){
            this.$axios.post('/GetAppConfig', {}).then((res) => {
                let resdata = res.data;
                debugger;
                this.TaskApps = resdata.ResponseStatus;
            })
        },

isRepeatLine(dtid){
    if(this.repLine.indexOf(dtid)>-1){
        return true
    }
},
getRepeat(appid){
    if(this.repLine && this.repLine.length>0){
        this.repLine.splice(0,this.repLine.length);//清空数组      
    }
    const repdtid = this.SameData[appid];
    if(repdtid){
         for(var i=0;i<repdtid.length;i++){
            this.repLine.push(repdtid[i]);
        }
    }   
    this.repLine; 
    //const repdtid = this.cf.find(v => Array.isArray(v[appid]) && v[appid].length > 1);
},
isRepeat(appid){//检测是否有重复的项
    var rep = this.SameData[appid];
    if(rep && rep.length>1){
        return true
    }else{
        return false
    }
},

        changeEnvironment(tid, dtid, eid) {
            //const thetask = this.tableDatas.find(x => dtid == x.TaskDetail.TaskDetailId);
            const thetask = this.tableDatas.find(x => tid == x.TaskId);
            const thedetail = thetask.TaskDetail;
            const thetaskdetail = thedetail.find(y => dtid == y.TaskDetailId);
            if(eid!=thetaskdetail.Environment){
                thetaskdetail.Environment=eid;
                this.$axios.post('/UpdateTaskEnvironment', {"TaskDetailId": dtid,"NowEnvironment": eid}).then((res) => {
                    let resdata = res.data;
                    if(resdata.Result.ResultCode==0){
                        this.$notify({
                            title: '成功',
                            message: '更改状态成功！',
                            type: 'success'
                        })
                    }

                })
            }

 
        },
        
        changeTaskVersion(tid, dtid, value) {
                this.$axios.post('/UpdateTaskEnvironment', {"TaskDetailId": dtid,"TaskVersion": value}).then((res) => {
                    let resdata = res.data;
                    if(resdata.Result.ResultCode==0){
                        this.$notify({
                            title: '成功',
                            message: '更新成功！',
                            type: 'success'
                        })
                    }

                })}, 
fmtDate(obj){
    var date =  new Date(obj);
    var y = 1900+date.getYear();
    var m = "0"+(date.getMonth()+1);
    var d = "0"+date.getDate();
    return y+"-"+m.substring(m.length-2,m.length)+"-"+d.substring(d.length-2,d.length);
},
minu(a, b){//取两个数组的差集  
     return a.uniquelize().each(function(o){return b.contains(o) ? null : o});  
}, 
        sendClass(appid) {
            if (appid && appid.length > 0) {
                return 'i-font-s';
            } else {
                return 'i-font-s-n';
            }
        },
        getTagList() {//拉取
            this.$axios.post('/SearchTagList', {}).then((res) => {
                let resdata = res.data;
                this.Tags = resdata.ResponseStatus;
            })
        },

        addEmptyTag(tagid, tagname) {//在页面上创建空任务
            var LastTag = { 'TagId': tagid, 'text': tagname, 'value': tagname };
            this.Tags.push(LastTag)
        },
        AddTag() {
            if (this.NewTag.TagName) {
                this.$axios.post('/AddTag', { 'TagName': this.NewTag.TagName }).then((res) => {
                    let resdata = res.data;
                    if (resdata.Result.ResultCode == 0) {
                        this.$message({
                            type: 'success',
                            message: '新增标签成功!'
                        });
                        this.dialogTagVisible = false;
                        this.addEmptyTag(resdata.ResponseStatus.tag_id, resdata.ResponseStatus.tag_name)
                    }
                })
            } else {
                this.$message({
                    type: 'warning',
                    message: '标签值不能为空！'
                });
            }
        },
        toSend(atype, appid, keywords) {

            if (appid && appid.length > 0) {
            } else {
                return
            }
            if (atype == 1) {
                var url = 'http://cd.release.ctripcorp.com/#/app/' + appid + '/versions?order=&filter=' + keywords + '&limit=10&page=1';
            }else if(atype == 3) {
                var url = 'http://cd.release.ctripcorp.com/#/db?dbid='+appid;
            }else{
                var url = appid;
            }
            window.open(url)
        },
        getCookieProjectId() {
            if (getCookie('ProjectId') && getCookie('ProjectId') > 0) {
            } else {
                this.$message({
                    type: 'warning',
                    message: '请先选择一个发布计划!'
                });
                this.$router.push({ path: '/ProjectAll' })              
            }
        },
        addEmptyTask(lastid, RTime) {//在页面上创建空任务
            var LastId = { 'TaskId': lastid };
            this.TaskData.TaskReleaseTime = RTime;
            //this.TaskData.TaskId = lastid;
            Object.assign(this.TaskData, LastId);
            this.tableDatas.unshift(this.TaskData);
        },
        SubMe(processData) {//请求创建新任务
            if (this.$route.query.pid) {
                var pid = this.$route.query.pid
            } else {
                var pid = this.ProjectId
            }

            const obj = JSON.parse(JSON.stringify(processData));

            obj.ProjectId = pid

            obj.TagId = obj.TagId === '' ? 0 : obj.TagId
            this.$axios.post('/AddTask', obj).then((res) => {
                let resdata = res.data;
                if (resdata.Result.ResultCode == 0) {
                    this.$message({
                        type: 'success',
                        message: '创建成功!'
                    });
                    this.dialogFormVisible = false;
                    this.addEmptyTask(resdata.ResponseStatus.task_id, resdata.ResponseStatus.TaskReleaseTime)//把后台创建的内容同步到前端
                    //var LastId = { 'TaskId': resdata.ResponseStatus.task_id};
                }
            })
        },
        UpdateTaskList(taskid) {
            let editItem = this.tableDatas.find(x => taskid == x.TaskId);
            if (editItem) {

                Object.assign(editItem, this.TaskData);
            }
        },
        EditSubMe(processData) {//请求创建新任务


            var origin_detail = Array.from(this.originList.TaskDetail);
            var process_detail = Array.from(processData.TaskDetail);

            const c_data = [];
            for(var p=0;p<process_detail.length;p++){
                var same=0;
                
                for(var o=0;o<origin_detail.length;o++){
                    if(JSON.stringify(origin_detail[o])==JSON.stringify(process_detail[p])){
                        same=1;
                    }
                }
                if(same==0){
                    process_detail[p].TimeGrade='s'
                    process_detail[p].TimeGradeValue=1
                    c_data.push(process_detail[p])
                }
            }




            if (this.$route.query.pid) {
                var pid = this.$route.query.pid
            } else {
                var pid = this.ProjectId
            }
            var ObjPro = { 'ProjectId': pid };
            var obj = Object.assign({}, processData, ObjPro);
            obj.TagId = obj.TagId === '' ? 0 : obj.TagId
            Object.assign(processData, obj);
            processData.TagId = processData.TagId === '' ? 0 : processData.TagId
            delete processData.TagName;
            var sendingdata = JSON.parse(JSON.stringify(processData));
            var cv_data=[];
            cv_data = c_data.concat(this.delDatas);
            sendingdata.TaskDetail=cv_data;
            this.$axios.post('/EditTask', sendingdata).then((res) => {
                let resdata = res.data;
                if (resdata.Result.ResultCode == 0) {
                    this.$message({
                        type: 'success',
                        message: '编辑成功!'
                    });
                    this.dialogFormVisible = false;
                    this.UpdateTaskList(processData.TaskId)
                }
            })
        },
        confirmAdd() {//确认是否创建空任务
            if (this.TaskData.TaskId && this.TaskData.TaskId > 0) {
                this.EditSubMe(this.TaskData);
            } else {
                this.$confirm('此操作将创建一个任务, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    this.SubMe(this.TaskData);
                }).catch(() => {
                });
            }

        },
        AddTask() {
            this.TaskData = getTpl();
            this.TaskData.TaskId = 0;
            this.TaskData.TaskName = '';
            this.dialogFormVisible = true;
        },
        EditTask(TaskId) {
             this.delDatas=[];//清空待发送的已编辑数据
            this.dialogFormVisible = true;
            this.$axios.post('/SearchTask', {
                "TaskId": TaskId
            }).then((res) => {
                const list = res.data.ResponseStatus.tableData[0]
                this.originList = JSON.parse(JSON.stringify(list));
                this.TaskData = list;
            })
        },

        transTaskDA(row, column, cellValue) {
            const da = this.tableDatas.find(x => cellValue == x.TaskId);
            return da.Demander + ' / ' + da.Acceptance
        },

        transTaskGrade(row, column, cellValue) {
            const gg = this.Grades.find(x => cellValue == x.GradeId);
            return gg.text
        },

        transTag(row, column, cellValue) {
            const tt = this.Tags.find(x => cellValue == x.TagId);
            if (tt) {
                return tt.text
            }
        },
        removeDomain(item) {
            var index = this.TaskData.TaskDetail.indexOf(item);
            item.IsDeleted=1
            //var change_index = this.OnChangeDetail.indexOf(item);
            if (index !== -1) {
                this.TaskData.TaskDetail.splice(index, 1)
                this.delDatas.push (item);
            }
            // if (change_index !== -1) {
            //     this.OnChangeDetail.splice(index, 1)
            // }            
        },
        addDomain() {
            this.TaskData.TaskDetail.push({
                TaskDetailId: 0,
                DevMember: '',
                TaskAppId: '',
                TaskAppIdType: 1,
            });           
        },

        formatter(row, column) {
            return row.address;
        },
        filterTag(value, row) {
            return row.TagName === value;
        },
        filterHandler(value, row, column) {
            const property = column['property'];
            return row[property] === value;
        },
        processDate(value, key) {
            let datess = value[key];
            if (datess) {
                let da = datess.split("T")[0];
                return da;
            }
        },
        getList() {//拉取
            console.log(this.$route.query.pid);
            if (this.$route.query.pid) {
                var pid = this.$route.query.pid
            } else {
                var pid = this.ProjectId
            }
            this.$axios.post('/SearchTask', {
                "ProjectId": pid
            }).then((res) => {
                let resdata = res.data;
                this.tableDatas = resdata.ResponseStatus.tableData || [];
                this.SameData = resdata.ResponseStatus.cf || [];
                //debugger
                this.ProjectName = resdata.ResponseStatus.ProjectName;
                document.title = resdata.ResponseStatus.ProjectName;
            })
        },
    }
}
</script>

<style scoped>
.handle-box {
    margin-bottom: 20px;
}

.handle-select {
    width: 120px;
}

.handle-input {
    width: 300px;
    display: inline-block;
}
</style>
