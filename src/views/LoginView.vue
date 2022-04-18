<template>
    <div class="page">
      <div class="container">
        <div class="left">
          <div class="login">Mailbox</div>
          <div class="eula">Plataforma administrativa y de consulta de reportes, noticias.</div>
        </div>
        <div class="right">
          <svg viewBox="0 0 320 300">
            <defs>
              <linearGradient
                inkscape:collect="always"
                id="linearGradient"
                x1="13"
                y1="193.49992"
                x2="307"
                y2="193.49992"
                gradientUnits="userSpaceOnUse">
                <stop
                  style="stop-color:#ff00ff;"
                  offset="0"
                  id="stop876" />
                <stop
                  style="stop-color:#ff0000;"
                  offset="1"
                  id="stop878" />
              </linearGradient>
            </defs>
            <path d="m 40,120.00016 239.99984,-3.2e-4 c 0,0 24.99263,0.79932 25.00016,35.00016 0.008,34.20084 -25.00016,35 -25.00016,35 h -239.99984 c 0,-0.0205 -25,4.01348 -25,38.5 0,34.48652 25,38.5 25,38.5 h 215 c 0,0 20,-0.99604 20,-25 0,-24.00396 -20,-25 -20,-25 h -190 c 0,0 -20,1.71033 -20,25 0,24.00396 20,25 20,25 h 168.57143" />
          </svg>
          <div class="form">
            <label for="email">Correo</label>
            <input type="email" id="email" @focus="focus('email')" v-model="email">
            <label for="password">Contraseña</label>
            <input type="password" id="password" @focus="focus('password')" v-model="password">
            <input type="submit" id="submit" value="Ingresar" @click="focus('submit')">
          </div>
        </div>
      </div>
    </div> 
</template>

<script>

  import anime from 'animejs';
  import axios from 'axios';

  export default {

    name: 'LoginView',
    components: {
      // LoginComponent
    },
    data() {
      return {
        email: '',
        password: '',
        token: ''
      }
    },
    methods: {
      focus(selector) {
        var current = null;
        if(selector == 'email') {
          if (current) current.pause();
          current = anime({
            targets: 'path',
            strokeDashoffset: {
              value: 0,
              duration: 700,
              easing: 'easeOutQuart'
            },
            strokeDasharray: {
              value: '240 1386',
              duration: 700,
              easing: 'easeOutQuart'
            }
          });
        } else if(selector == 'password') {
          if (current) current.pause();
          current = anime({
            targets: 'path',
            strokeDashoffset: {
              value: -336,
              duration: 700,
              easing: 'easeOutQuart'
            },
            strokeDasharray: {
              value: '240 1386',
              duration: 700,
              easing: 'easeOutQuart'
            }
          });

        } else if(selector == 'submit') {
          if (current) current.pause();
          current = anime({
            targets: 'path',
            strokeDashoffset: {
              value: -730,
              duration: 700,
              easing: 'easeOutQuart'
            },
            strokeDasharray: {
              value: '530 1386',
              duration: 700,
              easing: 'easeOutQuart'
            },
          });
          this.login();
        } 
      },

      // login with user
      login() {

        const credentials = {
          email: this.email,
          password: this.password
        }

        // communication with the backend
        axios.post('http://127.0.0.1:8000/api/sign_in', credentials)
          .then( response => {
            if(response.data.status) {
              this.token = response.data.access_token;
              this.$router.push({name: 'home'});
            } else if(response.data.email) {
              alert(response.data.email)
            } else if(response.data.password) {
              alert(response.data.password)
            } else {
              alert(response.data.message)
            }
          })
          .catch(function(e){
            console.error(e);
          })
      },
    }
  };
</script>

<style scoped>
  @import url('https://rsms.me/inter/inter-ui.css');
  ::selection {
    /* background: #2D2F36; */
    background: #ff9100;
  }
  ::-webkit-selection {
    background: #2D2F36;
  }
  ::-moz-selection {
    background: #2D2F36;
  }
  .page {
    /* background: #e2e2e5; */
    background-image: url('../assets/background.jpg');
    background-position: center center;
    background-repeat: no-repeat;
    background-size: 100% 100%;
    display: flex;
    flex-direction: column;
    height: 100%;
    position: absolute;
    place-content: center;
    width: 100%;
    font-family: 'Inter UI', sans-serif;
  }
  @media (max-width: 767px) {
    .page {
      height: auto;
      /* margin-bottom: 20px; */
      /* padding-bottom: 20px; */
    }
  }
  .page::before {
    content:'';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0,0,0,0.3);
  }
  .container {
    display: flex;
    height: 320px;
    margin: 0 auto;
    width: 640px;
  }
  @media (max-width: 767px) {
    .container {
      flex-direction: column;
      height: 630px;
      width: 320px;
    }
  }
  .left {
    background: white;
    height: calc(100% - 40px);
    top: 20px;
    position: relative;
    width: 50%;
  }
  @media (max-width: 767px) {
    .left {
      height: 100%;
      left: 20px;
      width: calc(100% - 40px);
      max-height: 270px;
    }
  }
  .login {
    font-size: 50px;
    font-weight: 900;
    margin: 50px 40px 40px;
  }
  .eula {
    color: #999;
    font-size: 14px;
    line-height: 1.5;
    margin: 40px;
  }
  .right {
    background: #474A59;
    box-shadow: 0px 0px 40px 16px rgba(0,0,0,0.22);
    color: #F1F1F2;
    position: relative;
    width: 50%;
  }
  @media (max-width: 767px) {
    .right {
      flex-shrink: 0;
      height: 100%;
      width: 100%;
      max-height: 350px;
    }
  }
  svg {
    position: absolute;
    width: 320px;
  }
  path {
    fill: none;
    stroke: url(#linearGradient);;
    stroke-width: 4;
    stroke-dasharray: 240 1386;
  }
  .form {
    margin: 40px;
    position: absolute;
  }

  .left {
    overflow: hidden;
    -webkit-transform: translate(0%, 0%);
    -moz-transform: translate(0%, 0%);
    -ms-transform: translate(0%, 0%);
    -o-transform: translate(0%,0%);
    transform: translate(0%, 0%);
    -webkit-transition: -webkit-transform 300ms, box-shadow 300ms;
    -moz-transition: -moz-transform 300ms, box-shadow 300ms;
    transition: transform 300ms, box-shadow 300ms;
  }
  .left::before, .left::after {
    content: "";
    position: absolute;
    width: 600px;
    height: 600px;
    border-top-left-radius: 40%;
    border-top-right-radius: 45%;
    border-bottom-left-radius: 35%;
    border-bottom-right-radius: 40%;
    z-index: -1;
  }
  .left::before {
    left: -83%;
    bottom: -190%;
    background-color: rgba(69, 105, 144, 0.15);
    -webkit-animation: wawes 6s infinite linear;
    -moz-animation: wawes 6s infinite linear;
    animation: wawes 6s infinite linear;
  }
  .left::after {
    left: -78%;
    bottom: -185%;
    background-color: rgba(2, 128, 144, 0.2);
    -webkit-animation: wawes 7s infinite;
    -moz-animation: wawes 7s infinite;
    animation: wawes 7s infinite;
  }

  @-webkit-keyframes wawes {
    from {
      -webkit-transform: rotate(0);
    }
    to {
      -webkit-transform: rotate(360deg);
    }
  }
  @-moz-keyframes wawes {
    from {
      -moz-transform: rotate(0);
    }
    to {
      -moz-transform: rotate(360deg);
    }
  }
  @keyframes wawes {
    from {
      -webkit-transform: rotate(0);
      -moz-transform: rotate(0);
      -ms-transform: rotate(0);
      -o-transform: rotate(0);
      transform: rotate(0);
    }
    to {
      -webkit-transform: rotate(360deg);
      -moz-transform: rotate(360deg);
      -ms-transform: rotate(360deg);
      -o-transform: rotate(360deg);
      transform: rotate(360deg);
    }
  }

/* end of the paste content */

  label {
    color:  #c2c2c5;
    display: block;
    font-size: 14px;
    height: 16px;
    margin-top: 20px;
    margin-bottom: 5px;
  }
  input {
    background: transparent;
    border: 0;
    color: #f2f2f2;
    font-size: 20px;
    height: 30px;
    line-height: 30px;
    outline: none !important;
    width: 100%;
  }
  input::-moz-focus-inner { 
    border: 0; 
  }
  #submit {
    color: #707075;
    margin-top: 40px;
    transition: color 300ms;
  }
  #submit:focus {
    color: #f2f2f2;
  }
  #submit:active {
    color: #d0d0d2;
  }
</style>