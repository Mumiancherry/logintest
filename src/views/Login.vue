<template>
	<div class="login-register">
		<div class="contain">
			<div class="big-box">
				<div class="big-contain">
					<div class="btitle">账户登录</div>
					<div class="bform">
						<input type="text" placeholder="用户名" v-model="form.username">
						<span class="errTips" v-if="usernameError">* 用户名或密码填写错误 *</span>
						<input type="password" placeholder="密码" v-model="form.userpwd">
						<span class="errTips" v-if="passwordError">* 用户名或密码填写错误 *</span>
					</div>
					<button class="bbutton" @click="login">登录</button>
				</div>
			</div>
			<div class="small-box">
				<img alt="Maoyunai" src="../assets/side.png" class="sideimg">				
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		name:'Login',
		data(){
			return {
				usernameError: false,
				passwordError: false,
				form:{
					username:'',
					userpwd:''
				}
			}
		},
		methods:{			
			login() {
				const self = this;
				// 以下为不交互
				// if(self.form.username == 'admin' && self.form.userpwd == '12345')
				// {
				// 	self.passwordError = false;
				// 	self.usernameError = false;
				// 	alert("登陆成功！按下确定后跳转首页");				
				// 	this.$router.push('/');
				// }
				// else
				// {
				// 	self.passwordError = true;
				// 	self.usernameError = true;
				// }
				// 以下为交互
				if (self.form.username != "" && self.form.userpwd != "") {
					self.$axios({
						method:'post',
						url: 'https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js',
						data: {
							username: self.form.username,
							password: self.form.userpwd
						}
					})
					.then( res => {
						switch(res.data){
							case 0: 
								alert("登陆成功！按下确定后跳转首页");								
								this.$router.push('/');
								break;
							case -1:
								this.usernameError = true;
								this.passwordError = true;
								break;
						}
						// alert("res");
						// console.log(res);
						// console.log(res.token);
					})
					.catch( err => {
						console.log(err);
					})
				} else{
					alert("填写不能为空！");
				}
			}
		}
	}
</script>

<style scoped="scoped">
    .sideimg {
        display:block;
        width: 100%;
        height: 100%;
    }
	.login-register{
		width: 100vw;
		height: 100vh;
		box-sizing: border-box;
	}
	.contain{
		width: 60%;
		height: 50%;
		position: relative;
		top: 35%;
		left: 50%;
		transform: translate(-50%,-50%);
		background-color: #fff;
		border-radius: 20px;
		box-shadow: 0 0 3px #f0f0f0,
					0 0 6px #f0f0f0;
	}
	.big-box{
		width: 70%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 35%;
		transform: translateX(0%);
		transition: all 1s;
	}
    .small-box{
		width: 35%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		transform: translateX(0%);
		transition: all 1s;
		border-top-left-radius: inherit;
		border-bottom-left-radius: inherit;
	}
	.big-contain{
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.btitle{
		font-size: 1.5em;
		font-weight: bold;
		color: rgb(57,167,176);
	}
	.bform{
		width: 100%;
		height: 40%;
		padding: 2em 0;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		align-items: center;
	}
	.bform .errTips{
		display: block;
		width: 50%;
		text-align: left;
		color: red;
		font-size: 0.7em;
		margin-left: 1em;
	}
	.bform input{
		width: 50%;
		height: 30px;
		border: none;
		outline: none;
		border-radius: 10px;
		padding-left: 2em;
		background-color: #f0f0f0;
	}
	.bbutton{
		width: 20%;
		height: 40px;
		border-radius: 24px;
		border: none;
		outline: none;
		background-color: rgb(57,167,176);
		color: #fff;
		font-size: 0.9em;
		cursor: pointer;
	}
		
	.big-box.active{
		left: 0;
		transition: all 0.5s;
	}
	.small-box.active{
		left: 100%;
		border-top-left-radius: 0;
		border-bottom-left-radius: 0;
		border-top-right-radius: inherit;
		border-bottom-right-radius: inherit;
		transform: translateX(-100%);
		transition: all 1s;
	}
</style>