<template>
  <li>
    <div :class="data.direction === 'left' ? 'direction-l' : 'direction-r'">
      <div class="flag-wrapper">
        <span :class="flagClass">
          {{ data.name}}
          <b style="display: none">
            {{ data.active}}
          </b>
        </span>
      </div>
    </div>
  </li>
</template>

<script>
  export default {
    name: "TimeLineItem",
    props:{
      data:{
        type: Object,
        required: true
      }
    },
    mounted(){
      if(this.data.active) {
        setTimeout(() => {
          this.flagClass = 'flag-active'
        }, 500)
      }
    },
    updated(){
      if(this.data.active === false) {
        setTimeout(() => {
          this.flagClass = 'flag'
        }, 500)
      }
    },
    data(){
      return {
        flagClass: 'flag'
      }
    }
  }
</script>

<style scoped>
  .direction-l {
    position: relative;
    width: 300px;
    float: left;
    text-align: right;
  }

  .direction-r {
    position: relative;
    width: 300px;
    float: right;
  }

  .flag-wrapper {
    position: relative;
    display: inline-block;

    text-align: center;
  }

  .flag {
    position: relative;
    display: inline;
    background: rgb(248,248,248);
    padding: 6px 10px;
    border-radius: 5px;

    font-weight: 600;
    text-align: left;
  }

  .direction-l .flag {
    -webkit-box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    -moz-box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
  }

  .direction-r .flag {
    -webkit-box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    -moz-box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
  }

  .direction-l .flag:before,
  .direction-r .flag:before {
    position: absolute;
    top: 50%;
    right: -40px;
    content: ' ';
    display: block;
    width: 12px;
    height: 12px;
    margin-top: -10px;
    background: #fff;
    border-radius: 10px;
    border: 1px solid rgb(255,80,80);
    z-index: 10;
  }

  .direction-r .flag:before {
    left: -35px;
  }
  .direction-l .flag:before {
    right: -36px;
  }

  .direction-r .flag:after {
    content: "";
    position: absolute;
    right: 100%;
    top: 50%;
    height: 0;
    width: 0;
    margin-top: -8px;
    border: 8px solid transparent;
    border-right-color: rgb(248, 248, 248);
    pointer-events: none;
  }

  .direction-l .flag:after {
    content: "";
    position: absolute;
    left: 100%;
    top: 50%;
    height: 0;
    width: 0;
    margin-top: -8px;
    border: 8px solid transparent;
    border-left-color: rgb(248, 248, 248);
    pointer-events: none;
  }


  /*Flag-active*/

  .flag-active {
    position: relative;
    display: inline;
    background: rgb(248,248,248);
    padding: 6px 10px;
    border-radius: 5px;

    font-weight: 600;
    text-align: left;
  }

  .direction-l .flag-active {
    -webkit-box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    -moz-box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    box-shadow: -1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
  }

  .direction-r .flag-active {
    -webkit-box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    -moz-box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
    box-shadow: 1px 1px 1px rgba(0,0,0,0.15), 0 0 1px rgba(0,0,0,0.15);
  }

  .direction-l .flag-active:before,
  .direction-r .flag-active:before {
    position: absolute;
    top: 50%;
    right: -40px;
    content: ' ';
    display: block;
    width: 12px;
    height: 12px;
    margin-top: -10px;
    background: deepskyblue;
    border-radius: 10px;
    border: 1px solid rgb(10, 69, 221);
    z-index: 10;
  }

  .direction-r .flag-active:before {
    left: -35px;
  }

  .direction-l .flag-active:before {
    right: -36px;
  }

  .direction-r .flag-active:after {
    content: "";
    position: absolute;
    right: 100%;
    top: 50%;
    height: 0;
    width: 0;
    margin-top: -8px;
    border: 8px solid transparent;
    border-right-color: rgb(248, 248, 248);
    pointer-events: none;
  }

  .direction-l .flag-active:after {
    content: "";
    position: absolute;
    left: 100%;
    top: 50%;
    height: 0;
    width: 0;
    margin-top: -8px;
    border: 8px solid transparent;
    border-left-color: rgb(248, 248, 248);
    pointer-events: none;
  }
</style>
