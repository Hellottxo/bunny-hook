<script setup>
import * as PIXI from "pixi.js";
import { onMounted } from "vue";
import bunnyTexture from '../assets/examples/bunny.png';
import hookTexture from '../assets/examples/hook.png';

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

  const bunnyContianer = new PIXI.Container();

  app.stage.addChild(bunnyContianer);

  // Create a bunny
  const bunny = PIXI.Sprite.from(bunnyTexture);
  bunny.anchor.set(0.5);
  bunny.x = 0;
  bunny.y = 0;
  bunnyContianer.addChild(bunny);

  // Move bunny to the center
  bunnyContianer.x = app.screen.width / 2;
  bunnyContianer.y = app.screen.height / 2;

  // Center bunny sprite in local container coordinates
  bunnyContianer.pivot.x = -bunnyContianer.width / 2;
  bunnyContianer.pivot.y = -bunnyContianer.height / 2;

  // create a ropeContainer
  const ropeContainer = new PIXI.Container();
  bunnyContianer.addChild(ropeContainer);

  // Create a hook
  const hook = PIXI.Sprite.from(hookTexture);
  hook.scale.set(0.15);
  hook.anchor.set(0.5);
  hook.x = 31;
  hook.y = 10;
  ropeContainer.addChild(hook);
  // Create a rope
  const rope = new PIXI.Graphics();
  rope.beginFill(0x64371f);
  rope.lineStyle(1, 0x64371f);
  rope.moveTo(25, -5);
  rope.lineTo(31, 0);
  rope.endFill();
  ropeContainer.addChild(rope);

  let direct = 1;

  // Listen for animate update
  app.ticker.add((delta) => {
    // rotate the container!
    // use delta to create frame-independent transform
    if (Math.abs(hook.rotation) > 0.15) {
      direct *= -1;
    }
    hook.rotation += 0.01 * delta * direct;
  });
}

onMounted(() => initState());
</script>

<template>
  <div id="pixi2"></div>
</template>
