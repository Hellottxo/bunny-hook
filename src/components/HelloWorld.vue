<script setup>
import * as PIXI from "pixi.js";
import { onMounted } from "vue";
import bunnyTexture from '../assets/examples/bunny.png';

defineProps({
  msg: String,
});

function initState() {
  const app = new PIXI.Application({
    width: 800,
    height: 600,
    backgroundColor: 0x1099bb,
    resolution: window.devicePixelRatio || 1,
  });
  document.body.appendChild(app.view);

  const container = new PIXI.Container();

  app.stage.addChild(container);

  // Create a new texture
  const texture = PIXI.Texture.from(bunnyTexture);

  // Create a bunny
  const bunny = new PIXI.Sprite(texture);
  bunny.anchor.set(0.5);
  bunny.x = 0;
  bunny.y = 0;
  container.addChild(bunny);

  // Move container to the center
  container.x = app.screen.width / 2;
  container.y = app.screen.height / 2;

  // Center bunny sprite in local container coordinates
  container.pivot.x = container.width / 2;
  container.pivot.y = container.height / 2;

  // Listen for animate update
  app.ticker.add((delta) => {
    // rotate the container!
    // use delta to create frame-independent transform
    container.rotation -= 0.01 * delta;
  });
}

onMounted(() => initState());
</script>

<template>
  <div id="pixi2"></div>
</template>
