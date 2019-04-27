<template>
  <div>
    <div id="cs-timeline" style="height: 300px; overflow: scroll;">
      <transition-group name="list" class="timeline" tag="ul">
        <TimeLineItem v-for="(item, index) in timelines"
                      :key="`${item.name}`"
                      :data="item"/>
      </transition-group>
    </div>
  </div>
</template>

<script>
  import TimeLineItem from "./TimeLineItem"
  import _ from "lodash"

  export default {
    name: "TimeLine",
    components: {
      TimeLineItem
    },
    created() {
      window.addEventListener('beforeunload', this.removeUser)
      setInterval(() => {
        this.addItem();
      },2000)
    },
    data(){
      return {
        number: 0,
        timelines: [
          {
            name: "FreeLancer",
            active: false,
            direction: 'left'
          },
          {
            name: "Dev",
            active: false,
            direction: 'left'
          },
          {
            name: "Manager",
            active: false,
            direction: 'left'
          },
          {
            name: "Boss",
            active: false,
            direction: 'right'
          }
        ]
      }
    },
    methods: {
      addItem: _.debounce(function (){
        let randomNumber = Math.floor(Math.random() * 2)
        this.timelines.unshift({
          name: this.number,
          active: false,
          direction: randomNumber === 0 ? 'left' : 'right'
        })
        this.timelines.forEach((o,index) => {
          o.active = index === 0;
        })
        this.number++
      },250)
    }
  }
</script>

<style scoped>
  .list-enter-active,
  .list-leave-active {
    transition: opacity 0.3s, transform 0.3s;
    transform-origin: right center;
  }
  .list-enter, .list-leave-to /* .list-leave-active for <2.1.8 */ {
    opacity: 0;
    transform: scale(0.5);
  }

  .list-leave-active {
    position: absolute;
  }

  .list-move {
    transition: transform .4s linear .3s;
  }

  #cs-timeline::-webkit-scrollbar {
    display: none;
  }
  .timeline {
    position: relative;
    width: 660px;
    margin: 20px auto 0;
    padding: 1em 0;
    list-style-type: none;
  }

  .timeline:before {
    position: absolute;
    left: 50%;
    top: 0;
    content: ' ';
    display: block;
    width: 6px;
    min-height: 300px;
    height: 100%;
    margin-left: -3px;
    background: rgb(80,80,80);
    background: -moz-linear-gradient(top, rgba(80,80,80,0) 0%, rgb(80,80,80) 8%, rgb(80,80,80) 92%, rgba(80,80,80,0) 100%);
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(30,87,153,1)), color-stop(100%,rgba(125,185,232,1)));
    background: -webkit-linear-gradient(top, rgba(80,80,80,0) 0%, rgb(80,80,80) 8%, rgb(80,80,80) 92%, rgba(80,80,80,0) 100%);
    background: -o-linear-gradient(top, rgba(80,80,80,0) 0%, rgb(80,80,80) 8%, rgb(80,80,80) 92%, rgba(80,80,80,0) 100%);
    background: -ms-linear-gradient(top, rgba(80,80,80,0) 0%, rgb(80,80,80) 8%, rgb(80,80,80) 92%, rgba(80,80,80,0) 100%);
    background: linear-gradient(to bottom, rgba(80,80,80,0) 0%, rgb(80,80,80) 8%, rgb(80,80,80) 92%, rgba(80,80,80,0) 100%);
    z-index: -1;
  }

  .timeline li {
    padding: 1em 0;
  }

  .timeline li:after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
  }
</style>
