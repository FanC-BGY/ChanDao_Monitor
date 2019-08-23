<template>
	<div class="about">
		<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
			<el-form-item label="BIP账号" prop="account" >
				<el-input v-model="ruleForm.account"></el-input>
			</el-form-item>
			<el-form-item label="姓名" prop="name">
				<el-input v-model="ruleForm.name"></el-input>
			</el-form-item>
			<el-form-item label="禅道密码" prop="chandaoPass">
				<el-input v-model="ruleForm.chandaoPass" @change="isChange(ruleForm.chandaoPass)"></el-input>
					<i @click="changeStatus">
						<img class="pic" v-show="isShow" src="../assets/img/open.svg" alt="#">
						<img class="pic" v-show="!isShow" src="../assets/img/close.svg" alt="#">
					</i>
				<el-button type="primary" @click="change(ruleForm.chandaoPass)" style="width:33%;">生成MPS码</el-button>
			</el-form-item>
			<el-form-item label="MPS密码">
				<el-input v-model="mpsPass" disabled></el-input>
			</el-form-item>
			<el-form-item label="企业微信号" prop="weixin">
				<el-input v-model="ruleForm.weixin"></el-input>
			</el-form-item>
			<el-form-item label="免打扰" prop="resource">
				<el-radio-group v-model="ruleForm.resource" style="line-height:50px;">
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
				isShow: true,
				ruleForm: {
					account: '',
					name: '',
					chandaoPass: '',
					weixin: '',
					resource: '是',
				},
				mpsPass: '',
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
					weixin: [
						{ required: true, message: '请输入微信号', trigger: 'change' }
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
					this.mpsPass = this.$md5('你好吗')
					console.log(this.$md5('你好吗'))
				} else{
					console.log('请输入禅道密码')
				}
			},
			// 
			changeStatus(){
				
					if(this.isShow === true){
						this.msg = this.ruleForm.chandaoPass;
						this.ruleForm.chandaoPass = '******';
					}else{
						this.ruleForm.chandaoPass= this.msg;
					}
					this.isShow = !this.isShow;
			},
			submitForm(formName) {
				this.$refs[formName].validate((valid) => {
				if (valid) {
					alert('submit!');
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
		position: absolute;
		top:40%;
		right:0%;
		transform: translate(-50%,-50%);
		background: rgb(30, 30, 30);
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
			height: 40px;
			line-height: 40px;
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
// .el-form-item__content {
//     // line-height: 40px;
//     // position: relative;
//     // font-size: 14px;
//     margin-left:0!important;
// }
</style>
