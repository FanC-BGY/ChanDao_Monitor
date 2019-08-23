<template>
	<div class="about">
		<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
			<el-form-item label="姓名" prop="name">
				<el-input v-model="ruleForm.name"></el-input>
			</el-form-item>
			<el-form-item label="BIP账号" prop="account" >
				<el-input v-model="ruleForm.account"></el-input>
			</el-form-item>
			<el-form-item label="禅道密码" prop="chandaoPass">
				<template v-if="!isShow">
						<el-input type="password" v-model="ruleForm.chandaoPass" @change="isChange(ruleForm.chandaoPass)"></el-input>
				</template>
				<template v-if="isShow">
						<el-input v-model="ruleForm.chandaoPass" @change="isChange(ruleForm.chandaoPass)"></el-input>
				</template>
					<i @click="changeStatus">
						<img class="pic" v-show="isShow" src="../assets/img/open.svg" alt="#">
						<img class="pic" v-show="!isShow" src="../assets/img/close.svg" alt="#">
					</i>
				<el-button type="primary" @click="change(ruleForm.chandaoPass)" style="width:33%;">生成MD5码</el-button>
			</el-form-item>
			<el-form-item label="MD5密码" prop="mpsPass">
				<!-- <el-input v-model="mpsPass" disabled></el-input> -->
				<el-input type="textarea" v-model="ruleForm.mpsPass" disabled></el-input>
			</el-form-item>
			<el-form-item label="企业微信号" prop="weixin">
				<el-input v-model="ruleForm.weixin"></el-input>
			</el-form-item>
			<el-form-item label="免打扰" prop="resource">
				<el-radio-group v-model="ruleForm.resource" style="line-height:50px;margin-bottom:0 !importat;">
					<el-radio label="是"></el-radio>
					<el-radio label="否"></el-radio>
				</el-radio-group>
			</el-form-item>
			<el-form-item>
				<el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
				<el-button @click="resetForm('ruleForm')">重置</el-button>
			</el-form-item>
		</el-form>
	</div>
</template>
<script>
		export default {
		data() {
			return {
				value: '',
				isShow: false,
				ruleForm: {
					account: '',
					name: '',
					chandaoPass: '',
					mpsPass: '',
					weixin: '',
					resource: '是',
				},
				// mpsPass: '',
				msg: '',
				rules: {
					account: [
						{ required: true, message: '请输入账号', trigger: 'blur' },
					],
					name: [
						{ required: true, message: '请输入姓名', trigger: 'blur' },
					],
					chandaoPass: [
						{ required: true, message: '请输入禅道密码', trigger: 'change' }
					],
					mpsPass :[
						{ required: true, message: '请生成MD5码', trigger: 'change' }
					],
					weixin: [
						{ required: false, message: '请输入微信号', trigger: 'change' }
					],
					resource: [
						{ required: true, message: '请选择是否免打扰', trigger: 'change' }
					],
				}
			};
		},
		methods: {
			isChange(){
				// console.log( value )
			},
			// 生成mps码
			change() {
				if( this.ruleForm.chandaoPass !== '') {
					// this.mpsPass = this.$md5(this.ruleForm.chandaoPass)
					this.ruleForm.mpsPass = this.$md5(this.ruleForm.chandaoPass)
					console.log(this.$md5('你好吗'))
				} else{
					console.log('请输入禅道密码')
				}
			},
			// 
			changeStatus(){
					// if(this.isShow === true){
					// 	this.msg = this.ruleForm.chandaoPass;
					// 	this.ruleForm.chandaoPass = '******';
					// }else{
					// 	this.ruleForm.chandaoPass= this.msg;
					// }
					// this.isShow = !this.isShow;
					if(this.isShow === false){
						// this.ruleForm.chandaoPass = '******';
						this.msg = this.ruleForm.chandaoPass;
						
					}else{
						this.ruleForm.chandaoPass= this.msg;
					}
					this.isShow = !this.isShow;
			},
			submitForm(formName) {
				this.$refs[formName].validate((valid) => {
				if (valid) {
					
					this.$alert('恭喜，您的信息已提交成功！', '温馨提示', {
					confirmButtonText: '确定',
					});
					window.location("http://www.baidu.com")
				} else {
					console.log('error submit!!');
					return false;
				}
				});
			},
			resetForm(formName) {
				this.mpsPass = '',
				this.$refs[formName].resetFields();
			}
		}
	}
</script>
<style lang="scss">
.about{
	width:100vw;
	height:100vh;
	position: relative;
	overflow: hidden;
	.demo-ruleForm{
		width:35%;
		height:69%;
		position: absolute;
		top:50%;
		left:80%;
		transform: translate(-50%,-50%);
		background: rgba(9, 18, 59,.8);
		// background: #1a2f72;
		padding-top:30px;
		border-radius: 5%;
		.el-input__inner {
			-webkit-appearance: none;
			background-color: #FFF;
			background-image: none;
			border-radius: 4px;
			border: 1px solid #DCDFE6;
			-webkit-box-sizing: border-box;
			box-sizing: border-box;
			color: #606266;
			display: inline-block;
			font-size: inherit;
			height: 35px;
			line-height: 35px;
			outline: 0;
			-webkit-transition: border-color .2s cubic-bezier(.645,.045,.355,1);
			transition: border-color .2s cubic-bezier(.645,.045,.355,1);
		}
		.el-input{
			width:55%;
			margin-right:5px;
			float: left;
		}
		img{
			position: absolute;
			top:15%;
			right:47%;
			width:30px;
		}
    }
}
.el-radio-group{
	float: left;
	line-height: 50px;
}	
.el-form-item__content {
    line-height: 35px;
    position: relative;
    font-size: 14px;
	display: flex;
}
.el-form-item {
    margin-bottom: 18px!important;
}
.el-form-item__label {
    vertical-align: middle;
    float: left;
    font-size: 14px;
	color:#f2f2f2!important;
    line-height: 40px;
    padding: 0 12px 0 0;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
.el-radio {
	color:#f2f2f2!important;
    cursor: pointer;
    margin-right: 30px;
}
.el-textarea.is-disabled .el-textarea__inner {
    background-color: #F5F7FA;
    border-color: #E4E7ED;
    color: #C0C4CC;
    cursor: not-allowed;
    width: 55%;
    height: 35px;
}
</style>
