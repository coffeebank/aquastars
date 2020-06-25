<template>
  <div id="app">

    <div class="w-full h-screen overflow-hidden p-16">
      <div class="w-full h-full overflow-hidden bg-teal-700 flex shadow-lg" style="border-radius:1rem;">

        <!-- left sidebar -->
        <div class="bg-gray-800 h-full text-center overflow-y-auto" style="width:30%;min-width:350px">
            <router-link to="/">
              <img alt="logo" class="hoverscale cursor-pointer rounded-full mx-auto my-8 shadow-lg" style="width:248px;max-width:30%;height:auto;" src="@/assets/apple-touch-icon.png">
            </router-link>
            <div class="w-full px-8 my-8 text-left">
              <div class="player hoverscale bg-red-700 p-4 shadow-lg rounded-lg flex items-center cursor-pointer" v-if="!isPlaying" @click="play">
                <button class="play p-2">▶️</button>
                <div class="mx-2 text-lg font-bold select-none">Stream Listen.moe Radio</div>
              </div>
              <div class="player hoverscale bg-red-800 p-4 shadow-lg rounded-lg flex items-center cursor-pointer" v-else @click="pause">
                <button class="pause p-2">⏸️</button>
                <div class="mx-2 text-lg font-bold select-none">Stream Listen.moe Radio</div>
              </div>
            </div>
        
            <div id="nav" class="w-full px-8 flex md:flex-wrap">
              <router-link to="/">Home</router-link>
              <router-link to="/about">About</router-link>
            </div>
        </div>

        <!-- main body -->
        <main class="App__main w-full overflow-y-auto">
          <transition
            :name="transitionName"
            mode="out-in"
            beforeLeave="beforeLeave"
            enter="enter"
            afterEnter="afterEnter"
          >
            <router-view/>
          </transition>
        </main>

      </div>
    </div>


    <!-- <div id="nav" class="absolute bottom-0 mb-4 w-full">
      <router-link to="/" class="shadow-lg">Home</router-link>
      <router-link to="/about" class="shadow-lg">About</router-link>
    </div>
    
    <main class="App__main">
      <transition
        :name="transitionName"
        mode="out-in"
        beforeLeave="beforeLeave"
        enter="enter"
        afterEnter="afterEnter"
      >
        <router-view/>
      </transition>
    </main>


    <audio id="radioid" preload="auto">
      <source src="https://listen.moe/fallback" type="audio/mp3" />
    </audio> -->

  </div>
</template>

<script>
const DEFAULT_TRANSITION = 'fade';
export default {
  name: 'App',
  data() {
    return {
      prevHeight: 0,
      transitionName: DEFAULT_TRANSITION,
      isPlaying: false,
      // src: require('./assets/listenmoe.m3u'),
      player: new Audio('https://listen.moe/fallback')
    };
  },
  created() {
    this.$router.beforeEach((to, from, next) => {
      let transitionName = to.meta.transitionName || from.meta.transitionName;
      if (transitionName === 'slide') {
        const toDepth = to.path.split('/').length;
        const fromDepth = from.path.split('/').length;
        transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left';
      }
      this.transitionName = transitionName || DEFAULT_TRANSITION;
      next();
    });
  },
  methods: {
    beforeLeave(element) {
      this.prevHeight = getComputedStyle(element).height;
    },
    enter(element) {
      const { height } = getComputedStyle(element);

      element.style.height = this.prevHeight;

      setTimeout(() => {
        element.style.height = height;
      });
    },
    afterEnter(element) {
      element.style.height = 'auto';
    },
    play () {
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    }
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');
@import url('https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css');

body {
  background-image: linear-gradient(45deg, rgba(114, 40, 169,0.2) 0%, rgba(114, 40, 169,0.2) 16.667%,rgba(140, 59, 158,0.2) 16.667%, rgba(140, 59, 158,0.2) 33.334%,rgba(166, 77, 147,0.2) 33.334%, rgba(166, 77, 147,0.2) 50.001%,rgba(245, 133, 115,0.2) 50.001%, rgba(245, 133, 115,0.2) 66.668%,rgba(219, 114, 126,0.2) 66.668%, rgba(219, 114, 126,0.2) 83.335%,rgba(193, 96, 137,0.2) 83.335%, rgba(193, 96, 137,0.2) 100.002%),linear-gradient(22.5deg, rgba(114, 40, 169,0.2) 0%, rgba(114, 40, 169,0.2) 16.667%,rgba(140, 59, 158,0.2) 16.667%, rgba(140, 59, 158,0.2) 33.334%,rgba(166, 77, 147,0.2) 33.334%, rgba(166, 77, 147,0.2) 50.001%,rgba(245, 133, 115,0.2) 50.001%, rgba(245, 133, 115,0.2) 66.668%,rgba(219, 114, 126,0.2) 66.668%, rgba(219, 114, 126,0.2) 83.335%,rgba(193, 96, 137,0.2) 83.335%, rgba(193, 96, 137,0.2) 100.002%),linear-gradient(0deg, rgba(114, 40, 169,0.2) 0%, rgba(114, 40, 169,0.2) 16.667%,rgba(140, 59, 158,0.2) 16.667%, rgba(140, 59, 158,0.2) 33.334%,rgba(166, 77, 147,0.2) 33.334%, rgba(166, 77, 147,0.2) 50.001%,rgba(245, 133, 115,0.2) 50.001%, rgba(245, 133, 115,0.2) 66.668%,rgba(219, 114, 126,0.2) 66.668%, rgba(219, 114, 126,0.2) 83.335%,rgba(193, 96, 137,0.2) 83.335%, rgba(193, 96, 137,0.2) 100.002%),linear-gradient(90deg, rgb(55, 55, 55),rgb(181, 181, 181));
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}

#app {
  font-family: 'Indie Flower', cursive, Arial, Helvetica, sans-serif;
  text-align: center;
  color: #eee;
}

#nav {
  a {
    width:90%;
    padding: 2rem 0rem;
    font-weight: bold;
    font-size: 1.1rem;
    background-color: hsl(205,20,40);
    color: hsl(205,80,90);
    padding: 0.5rem 1.75rem;
    transition: all 0.35s ease;
    border-radius: 0.25rem;
    text-decoration: none;
    margin: 0.25rem auto;

    &:hover {
      width:100%;
    }

    &.router-link-exact-active {
      color: hsl(205,40,30);
      background-color: hsl(235,60,75);
    }
  }
}

.hoverscale {
  transition: all 0.35s ease;
  
  &:hover {
    transform:scale(1.05);
  }
}

.bg-stage {
  background:url('./assets/elijah-ekdahl-8XxF2kYHIgo-unsplash.jpg');
  background-size: cover;
  background-position: center;
}

.fade-enter-active,
.fade-leave-active {
  transition-duration: 0.3s;
  transition-property: height, opacity;
  transition-timing-function: ease;
  overflow: hidden;
}

.fade-enter,
.fade-leave-active {
  opacity: 0
}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition-duration: 0.5s;
  transition-property: height, opacity, transform;
  transition-timing-function: cubic-bezier(0.55, 0, 0.1, 1);
  overflow: hidden;
}

.slide-left-enter,
.slide-right-leave-active {
  opacity: 0;
  transform: translate(0, 2em);
}

.slide-left-leave-active,
.slide-right-enter {
  opacity: 0;
  transform: translate(0, 2em);
}

.puff-in-hor {
	-webkit-animation: puff-in-hor 0.7s cubic-bezier(0.470, 0.000, 0.745, 0.715) both;
	animation: puff-in-hor 0.7s cubic-bezier(0.470, 0.000, 0.745, 0.715) both;
}
@-webkit-keyframes puff-in-hor {
  0% {
    -webkit-transform: scaleX(2);
    transform: scaleX(2);
    -webkit-filter: blur(4px);
    filter: blur(4px);
    opacity: 0;
  }
  100% {
    -webkit-transform: scaleX(1);
    transform: scaleX(1);
    -webkit-filter: blur(0px);
    filter: blur(0px);
    opacity: 1;
  }
}
@keyframes puff-in-hor {
  0% {
    -webkit-transform: scaleX(2);
    transform: scaleX(2);
    -webkit-filter: blur(4px);
    filter: blur(4px);
    opacity: 0;
  }
  100% {
    -webkit-transform: scaleX(1);
    transform: scaleX(1);
    -webkit-filter: blur(0px);
    filter: blur(0px);
    opacity: 1;
  }
}

</style>