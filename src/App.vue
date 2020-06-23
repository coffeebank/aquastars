<template>
  <div id="app">
    <div id="nav" class="absolute bottom-0 mb-4 w-full">
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
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');
@import url('https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css');

body {
  background: url("assets/elijah-ekdahl-8XxF2kYHIgo-unsplash.jpg");
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
  padding: 30px;

  a {
    font-weight: bold;
    font-size: 1.25rem;
    background-color: hsl(205,20,50);
    color: hsl(205,80,90);
    padding: 0.5rem 1.75rem;
    transition: all 0.35s ease;
    border-radius: 0.25rem;
    text-decoration: none;
    margin: 0.25rem;

    &:hover {
      padding: 0.75rem 1.75rem;
    }

    &.router-link-exact-active {
      color: hsl(205,40,30);
      background-color: hsl(205,50,70);
    }
  }
}

.hoverscale {
  transition: all 0.35s ease;
  
  &:hover {
    transform:scale(1.05);
  }
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