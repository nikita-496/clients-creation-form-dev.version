<!--https://codepen.io/drewendly/pen/ZBqazz?editors=1010-->
<template>
  <div class="modal">
    <div class="h1wrap">
      <p>Идет отправка данных, пожалуйста, подождите ...</p>
    </div>

    <div class="DNA_cont">
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
      <div class="nucleobase"></div>
    </div>
  </div>
</template>

<script>
  export default {};
</script>

<style lang="scss" scoped>
  @import "../../src/scss/_vars.scss";
  .modal {
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.8);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 3;
  }
  $b-height: 1.15em;
  $el-size: 3vh;
  $DNA_scale: 0.45; //divides '$el-size'
  $t: 2.1s;
  $td: -0.89;

  $c_a: rgb(255, 132, 144) rgb(255, 115, 124) rgb(245, 247, 249); // top / bottom / BG
  $c2_a: rgb(255, 218, 178) rgb(255, 50, 155); // Fade-anim colors

  $ease-circ: cubic-bezier(0.42, 0, 0.58, 1);

  html {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body {
    height: 100%;
    text-align: center;
    line-height: 100vh;
    background-color: nth($c_a, 3);
  }

  p {
    font-family: "Product Sans", helvetica neue, helvetica, sans-serif;
    position: absolute; // display:block;
    height: 1em;
    width: 400px;
    text-align: center;
    top: 50%;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
    line-height: 1.666em;
    font-size: 1.4rem;
    font-weight: 500;
    letter-spacing: 0.0225em;
    opacity: 0.85;
    color: $clr-body-form;
    transform: scale(1);
    @media (max-width: map-get($breack-point, mobile)) {
      width: 300px;
      font-size: 1.2rem;
    }

    span {
      position: relative;
      display: inline-block;
    }

    &:after {
      display: inline-block;
      position: relative;
      bottom: 1.4em;
      left: 0.1em;
      font-size: 4vh;
      font-weight: 900;
      letter-spacing: -1em;
      opacity: 0;

      animation: superscript 1.6s cubic-bezier(0.25, 0, 0.2, 1) forwards;
      animation-delay: 500ms;
    }
  }

  .DNA_cont {
    display: inline-block;
    position: absolute;
    width: 360px;
    text-align: center;
    top: 44%;
    left: 0;
    right: 2.5%;
    margin-left: auto;
    margin-right: auto;
    /*position: relative;
    left: 20em;
    top: 20em;*/
    transform: scale($DNA_scale);
    @media (max-width: 350px) {
      width: 300px;
    }
  }

  .nucleobase {
    display: inline-block;
    position: relative;
    vertical-align: middle;
    //  width: 1px; height: $el-size*2.75;
    //  background: transparent;
    //  box-shadow: $el-size*0.475 $el-size*-0.85 0 rgba(0,0,0,0.2);

    &:not(:last-child) {
      margin-right: $el-size * 1.62;
    }

    &:before,
    &:after {
      content: "";
      display: inline-block;
      width: $el-size;
      height: $el-size;
      border-radius: 50%;

      position: absolute;
    }

    @for $i from 1 through 10 {
      &:nth-child(#{$i}) {
        // animation: animDotBar $t $ease-circ infinite;

        animation-delay: $i * ($td * $t);
        &:before {
          // transform: translateY(-200%);

          animation: animBefore $t $ease-circ infinite;

          animation-delay: $i * ($td * $t);

          background-color: nth($c_a, 1);
        }

        &:after {
          // transform: translateY(200%);

          animation: animAfter $t $ease-circ infinite;

          animation-delay: $i * ($td * $t);

          background-color: nth($c_a, 2);

          //  mix-blend-mode: multiply;
        }
      }
    }
  }

  @keyframes animBefore {
    0% {
      top: $el-size * -2;
      z-index: 1;
    }

    25% {
      transform: scale(1.2);
      z-index: 1;
    }

    50% {
      // background-color: nth($c_a, 1) ;
      top: $el-size * 2;
      z-index: -1;
    }

    75% {
      background-color: nth($c2_a, 1);
      transform: scale(0.8);
      z-index: -1;
    }

    100% {
      top: $el-size * -2;
      z-index: -1;
    }
  }

  @keyframes animAfter {
    0% {
      top: $el-size * 2;
      z-index: -1;
    }

    25% {
      background-color: nth($c2_a, 2);
      transform: scale(0.8);
      z-index: -1;
    }

    50% {
      //  background-color: nth($c_a, 2) ;
      top: $el-size * -2;
      z-index: 1;
    }

    75% {
      transform: scale(1.2);
      z-index: 1;
    }

    100% {
      top: $el-size * 2;
      z-index: 1;
    }
  }

  @keyframes animDotBar {
    // NOT USED
    0% {
      height: $el-size * 2.75;
    }

    25% {
      height: 0;
    }

    50% {
      height: $el-size * 2.75;
    }

    75% {
      height: 0;
    }

    100% {
      height: $el-size * 2.75;
    }
  }

  @keyframes superscript {
    0% {
      opacity: 0;
      transform: translateY(-1em);
    }
    100% {
      opacity: 1;
      transform: translateY(0em);
    }
  }
</style>
