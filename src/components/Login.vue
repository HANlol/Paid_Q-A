/*
 * @Author: hjj 
 * @Date: 2021-08-19 18:39:59 
 * @Last Modified by:   hjj 
 * @Last Modified time: 2021-08-19 18:39:59 
 */
<template>
<div class="mainbody">
    <div v-bind:class="{'container':true, 'right-panel-active':isOK}">
        <!-- Sign Up -->
        <div class="container__form container--signup">
            <form action="#" class="form" id="form1">
                <h2 class="form__title">Sign Up</h2>
                <div class="user-box">
                    <input type="text" name="" required value="">
                    <label>Username</label>
                </div>
                <div class="user-box">
                    <input type="email" name="" required value="">
                    <label>Email</label>
                </div>
                <div class="user-box">
                    <input type="password" name="" required value="">
                    <label>Password</label>
                </div>
                <a href="#">
                    <span></span>
                    <span></span>
                    <span></span>
                    <span></span>
                    Sign Up
                </a>
            </form>
        </div>
    
        <!-- Sign In -->
        <div class="container__form container--signin">
            <form action="#" class="form" id="form2">
                <h2 class="form__title">Sign In</h2>
                <div class="user-box">
                    <input type="text" name="" required value="">
                    <label>Username</label>
                </div>
                <div class="user-box">
                    <input type="password" name="" required value="">
                    <label>Password</label>
                </div>
                <!--
                <a href="#" class="link">Forgot your password?</a>
                <button class="btn">Sign In</button>    
                -->
                <a href="#">
                    <span></span>
                    <span></span>
                    <span></span>
                    <span></span>
                    Sign In
                </a>
            </form>
        </div>
    
        <!-- Overlay -->
        <div class="container__overlay">
            <div class="overlay">
                <div class="overlay__panel overlay--left">
                    <button class="btn" id="signIn" @click="changeClass()">Sign In</button>
                </div>
                <div class="overlay__panel overlay--right">
                    <button class="btn" id="signUp" @click="changeClass()">Sign Up</button>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
        isOK: false
    }
  },
  methods:{
      changeClass: function(){
          this.isOK = !this.isOK;
          console.log(this.isOK)
      }
  }
}
</script>

<style scoped>
.mainbody {
	align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    overflow-y: hidden;
	background: linear-gradient(#141e30,#243b55);
	background-attachment: fixed;
	background-position: center;
	background-repeat: no-repeat;
	background-size: cover;
	display: grid;
	height: 100%;
    width: 100%;
	place-items: center;
    font-family: Arial, Helvetica, sans-serif;
}

.title{
    font-size: 30px;
    letter-spacing: 20px;
    color: #fff;
}

.form__title {
	font-weight: 300;
	margin: 0;
	margin-bottom: 2rem;
}

/*
.link {
	color: #333;
	font-size: 0.9rem;
	margin: 1.5rem 0;
	text-decoration: none;
}
*/

.container {
	background: rgba(0, 0, 0, 0.5);
    box-sizing: border-box;
    box-shadow: 0,15px,25px,rgba(0, 0, 0, 0.6);
    border-radius: 10px;
	height: 420px;
	max-width: 758px;
	overflow: hidden;
	position: relative;
	width: 100%;
}

.container__form {
	height: 100%;
	position: absolute;
	top: 0;
	transition: all 0.6s ease-in-out;
}

.container--signin {
	left: 0;
	width: 50%;
	z-index: 2;
}

.container.right-panel-active .container--signin {
	transform: translateX(100%);
}

.container--signup {
	left: 0;
	opacity: 0;
	width: 50%;
	z-index: 1;
}

.container.right-panel-active .container--signup {
	animation: show 0.6s;
	opacity: 1;
	transform: translateX(100%);
	z-index: 5;
}

.container__overlay {
	height: 100%;
	left: 50%;
	overflow: hidden;
	position: absolute;
	top: 0;
	transition: transform 0.6s ease-in-out;
	width: 50%;
	z-index: 100;
}

.container.right-panel-active .container__overlay {
	transform: translateX(-100%);
}

h2{
    margin: 0 0 30px;
    padding: 0;
    color: #fff;
    text-align: center;
}
.user-box{
    position: relative;
    width: 100%;
}
.user-box input{
    width: 100%;
    padding: 10px 0;
    font-size: 16px;
    color: #fff;
    margin-bottom: 30px;
    border: none;
    border-bottom: 1px solid #fff;
    outline: none;
    background: transparent;
}
.user-box label{
    position: absolute;
    top: 0;
    left: 0;
    padding: 10px 0;
    font-size: 16px;
    color: #fff;
    pointer-events: none;
    transition: .5s;
}
.user-box input:focus ~ label,
.user-box input:valid ~ label{
    top: -20px;
    left: 0;
    color: #03e9f4;
    font-size: 12px;
}

.overlay {
	background: linear-gradient(#141e30,#243b55);
	background-attachment: fixed;
	background-position: center;
	background-repeat: no-repeat;
	background-size: cover;
	height: 100%;
	left: -100%;
	position: relative;
	transform: translateX(0);
	transition: transform 0.6s ease-in-out;
	width: 200%;
}

.container.right-panel-active .overlay {
	transform: translateX(50%);
}

.overlay__panel {
	align-items: center;
	display: flex;
	flex-direction: column;
	height: 100%;
	justify-content: center;
	position: absolute;
	text-align: center;
	top: 0;
	transform: translateX(0);
	transition: transform 0.6s ease-in-out;
	width: 50%;
}

.overlay--left {
	transform: translateX(-20%);
}

.container.right-panel-active .overlay--left {
	transform: translateX(0);
}

.overlay--right {
	right: 0;
	transform: translateX(0);
}

.container.right-panel-active .overlay--right {
	transform: translateX(20%);
}

.btn {
	background-color: #0367a6;
	background-image: linear-gradient(90deg, #0367a6 0%, #008997 74%);
	border-radius: 20px;
	border: 1px solid #0367a6;
	color: #616060;
	cursor: pointer;
	font-size: 0.8rem;
	font-weight: bold;
	letter-spacing: 0.1rem;
	padding: 0.9rem 4rem;
	text-transform: uppercase;
	transition: transform 80ms ease-in;
}

a{
    position: relative;
    display: inline-block;
    padding: 10px 20px;
    color: #03e9f4;
    font-size: 12px;
    text-decoration: none;
    text-transform: uppercase;
    overflow: hidden;
    margin-top: 40px;
    transition: .5s;
    letter-spacing: 4px;
    background: #202020;
}
.btn{
    position: relative;
    display: inline-block;
    padding: 10px 20px;
    color: #03e9f4;
    font-size: 12px;
    text-decoration: none;
    text-transform: uppercase;
    overflow: hidden;
    margin-top: 40px;
    transition: .5s;
    letter-spacing: 4px;
}
.form > .btn {
	margin-top: 1.5rem;
}
.form > a {
	margin-top: 1.5rem;
}

.btn:active {
	transform: scale(0.95);
}

.btn:focus {
	outline: none;
}

a:hover{
    background: #03e9f4;
    color: #fff;
    border-radius: 5px;
    box-shadow: 0 0 5px #03e9f4,
                0 0 25px #03e9f4,
                0 0 50px #03e9f4,
                0 0 100px #03e9f4;
}

.form {
	background-color: #202020;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	padding: 0 3rem;
	height: 100%;
	text-align: center;
}

a span{
    position: absolute;
    display: block;
}
a span:nth-child(1){
    top: 0;
    left: -100%;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg,transparent,#03e9f4);
    animation: btn-anim1 1s linear infinite;
}
a span:nth-child(2){
    top: -100%;
    right: 0;
    width: 2px;
    height: 100%;
    background: linear-gradient(180deg,transparent,#03e9f4);
    animation: btn-anim2 1s linear infinite;
    animation-delay: .25s;
}
a span:nth-child(3){
    bottom: 0;
    right: -100%;
    width: 100%;
    height: 2px;
    background: linear-gradient(270deg,transparent,#03e9f4);
    animation: btn-anim3 1s linear infinite;
    animation-delay: .5s;
}
a span:nth-child(4){
    bottom: -100%;
    left: 0;
    width: 2px;
    height: 100%;
    background: linear-gradient(360deg,transparent,#03e9f4);
    animation: btn-anim4 1s linear infinite;
    animation-delay: .75s;
}
@keyframes btn-anim1{
    0%{
        left: -100%;
    }
    50%,100%{
        left: 100%;
    }
}
@keyframes btn-anim2{
    0%{
        top: -100%;
    }
    50%,100%{
        top: 100%;
    }
}
@keyframes btn-anim3{
    0%{
        right: -100%;
    }
    50%,100%{
        right: 100%;
    }
}
@keyframes btn-anim4{
    0%{
        bottom: -100%;
    }
    50%,100%{
        bottom: 100%;
    }
}

@keyframes show {
	0%,
	49.99% {
		opacity: 0;
		z-index: 1;
	}

	50%,
	100% {
		opacity: 1;
		z-index: 5;
	}
}
</style>
