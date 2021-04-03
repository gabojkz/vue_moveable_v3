<template>
  <div class="page main">
    <div class="container">
      <Moveable
        class="moveable"
        v-bind="moveable"
        @drag="handleDrag"
        @resize="handleResize"
        @scale="handleScale"
        @rotate="handleRotate"
        @warp="handleWarp"
      >
        <span>Vue Moveable</span>
      </Moveable>

      <div class="buttons able">
        <a
          href="#"
          v-for="(state, key) in states"
          :key="key"
          :class="{ selected: currentState === key }"
          @click="currentState = key"
        >{{ state }}</a>
      </div>
    </div>
  </div>
</template>

<script>
import Moveable from '@/components/Moveable.vue';

export default {
  name: 'app',
  components: {
    Moveable,
    // Badges,
  },
  data: () => ({
    isActive: true,
    moveable: {
      draggable: true,
      throttleDrag: 1,
      resizable: false,
      throttleResize: 1,
      keepRatio: false,
      scalable: true,
      throttleScale: 0.01,
      rotatable: true,
      throttleRotate: 0.2,
      pinchable: true,
      origin: false,
    },
    states: {
      scalable: 'Scalable',
      resizable: 'Resizable',
      warpable: 'Warpable',
    },
    currentState: 'scalable',
  }),
  methods: {
    handleDrag({ target, transform }) {
      console.log('onDrag', transform);
      target.style.transform = transform;
    },
    handleResize({ target, width, height }) {
      console.log('onResize', width, height);
      target.style.width = `${width}px`;
      target.style.height = `${height}px`;
    },
    handleScale({ target, transform }) {
      console.log('onScale', transform);
      target.style.transform = transform;
    },
    handleRotate({ target, transform }) {
      console.log('onRotate', transform);
      target.style.transform = transform;
    },
    handleWarp({ target, transform }) {
      console.log('onWarp', transform);
      target.style.transform = transform;
    },
    clearAllStates() {
      Object.keys(this.states).forEach((key) => {
        this.moveable[key] = false;
      });
    },
  },
  watch: {
    currentState(newState) {
      this.clearAllStates();
      this.moveable[newState] = true;
    },
  },
};
</script>

<style>
  html, body {
    font-family: sans-serif;
    position: relative;
    margin: 0;
    padding: 0;
    height: 100%;
    color: #333;
    letter-spacing: 1px;
    background: #f5f5f5;
    font-weight: 300;
  }

  a {
    text-decoration: none;
    color: #333;
  }

  .page {
    position: relative;
    width: 100%;
    height: 100%;
    box-sizing: border-box;
  }

  .page:nth-child(2n) {
    background: #f0f0f0;
  }
  .page.main {
    z-index: 1;
    min-height: 700px;
  }

  .container {
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 30px;
    margin: 20px;
  }

  .moveable {
    font-family: "Roboto", sans-serif;
    position: relative;
    width: 300px;
    height: 200px;
    text-align: center;
    font-size: 40px;
    margin: 0 auto;
    font-weight: 100;
    letter-spacing: 1px;
  }

  .moveable span {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    white-space: nowrap;
  }

  .description {
    text-align: center;
  }

  .buttons.able {
    margin-top: 16px;
  }
  .buttons.able a {
    min-width: auto;
    padding: 8px 20px;
  }
  .buttons {
    text-align: center;
    margin: 0;
    padding: 10px;
  }

  .buttons a {
    position: relative;
    text-decoration: none;
    color: #333;
    border: 1px solid #333;
    padding: 12px 30px;
    min-width: 140px;
    text-align: center;
    display: inline-block;
    box-sizing: border-box;
    margin: 5px;
    transition: all ease 0.5s;
  }

  .buttons a:hover, .buttons a.selected {
    background: #333;
    color: #fff;
  }
</style>