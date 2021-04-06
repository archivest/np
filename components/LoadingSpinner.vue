<template>
  <div class="orbit-spinner">
    <div class="orbit"></div>
    <div class="orbit"></div>
    <div class="orbit"></div>
  </div>
</template>

<style type="text/css">
.orbit-spinner,
.orbit-spinner * {
  box-sizing: border-box;
}

@media only screen and (max-width: 600px) {
  .orbit-spinner {
    height: 55px;
    width: 55px;
  }
}

.orbit-spinner {
  height: 1100px;
  width: 1100px;
  border-radius: 50%;
  perspective: 8000px;
}

.orbit-spinner .orbit {
  position: absolute;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  border-radius: 50%;
}

.orbit-spinner .orbit:nth-child(1) {
  left: 0%;
  top: 0%;
  animation: orbit-spinner-orbit-one-animation 1200ms linear infinite;
  border-bottom: 60px solid black;
}

.orbit-spinner .orbit:nth-child(2) {
  right: 0%;
  top: 0%;
  animation: orbit-spinner-orbit-two-animation 1200ms linear infinite;
  border-right: 60px solid black;
}

.orbit-spinner .orbit:nth-child(3) {
  right: 0%;
  bottom: 0%;
  animation: orbit-spinner-orbit-three-animation 1200ms linear infinite;
  border-top: 60px solid black;
}

@keyframes orbit-spinner-orbit-one-animation {
  0% {
    transform: rotateX(35deg) rotateY(-45deg) rotateZ(0deg);
  }

  100% {
    transform: rotateX(35deg) rotateY(-45deg) rotateZ(360deg);
  }
}

@keyframes orbit-spinner-orbit-two-animation {
  0% {
    transform: rotateX(50deg) rotateY(10deg) rotateZ(0deg);
  }

  100% {
    transform: rotateX(50deg) rotateY(10deg) rotateZ(360deg);
  }
}

@keyframes orbit-spinner-orbit-three-animation {
  0% {
    transform: rotateX(35deg) rotateY(55deg) rotateZ(0deg);
  }

  100% {
    transform: rotateX(35deg) rotateY(55deg) rotateZ(360deg);
  }
}
</style>
