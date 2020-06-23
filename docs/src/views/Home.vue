<template>
  <div class="home">
    <div class="pt-12"></div>
    <img alt="logo" class="hoverscale vclickspinny cursor-pointer rounded-full mx-auto my-4 shadow-lg" style="width:50%;max-width:128px;height:auto;" src="@/assets/apple-touch-icon.png">
    <h1 class="text-5xl font-bold">✨ Aqua Stars ⚝</h1>

    <audio loop autoplay="1" id="audiosnippetId" onPlay="getSoundAndFadeAudio(this);"><br>
        <source src="https://listen.moe/fallback" type="audio/mpeg"><br>
    </audio>

  </div>
</template>

<script>
function getSoundAndFadeAudio (audiosnippetId) { // eslint-disable-line no-unused-vars
    var sound = document.getElementById(audiosnippetId);
    sound.volume == 0.5;
}
</script>

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