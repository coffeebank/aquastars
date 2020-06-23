<template>
  <div class="home">
    <div class="pt-12"></div>
    <img alt="logo" class="hoverscale vclickspinny cursor-pointer rounded-full mx-auto my-4 shadow-lg" style="width:50%;max-width:128px;height:auto;" src="@/assets/apple-touch-icon.png">
    <h1 class="text-5xl font-bold">✨ Aqua Stars ⚝</h1>
    <p class="text-2xl pt-4 pb-8">The best up and coming Cali idol group! 😉</p>

    <div id="radiohook">
      <img alt="logo" class="hoverscale cursor-pointer rounded-full mx-auto my-4 shadow-lg" style="width:50%;max-width:128px;height:auto;" src="@/assets/brian.png" onclick="document.getElementById('radioid').play()">
    </div>

    <p class="text-xl italic">"@snowy claire You're part of my Idol group now"<br>- Brian Walker</p>

  </div>
</template>

<style lang="scss">
.vclickspinny {
  transition: all 0.35s ease;

  &:active {
    animation-name: spin;
    animation-duration: 0.875s;
    animation-iteration-count: infinite;
    animation-timing-function: linear; 
    @keyframes spin {
      from {
          transform:rotate(0deg);
      }
      to {
          transform:rotate(360deg);
      }
    }
  }
}
</style>