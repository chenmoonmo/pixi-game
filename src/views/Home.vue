<template>
  <div class="container" ref="container"></div>
</template>

<script>
import * as PIXI from "pixi.js";
import clonedeep from "lodash.clonedeep";
export default {
  name: "Home",
  data() {
    return {
      app: null,
      image: require("../assets/images/little_witch.png"),
    };
  },
  mounted() {
    this.app = new PIXI.Application({
      backgroundColor: 0x1d9ce0,
    });
    this.$refs.container.appendChild(this.app.view);
    this.app.loader.add("human", this.image).load(this.setup);
  },
  methods: {
    setup() {
      let texture = this.app.loader.resources.human.texture;
      const frames = [];
      for (let i = 0; i < 3; i++) {
        let rectangle = new PIXI.Rectangle(58 * i, 0, 58, 46);
        texture.frame = rectangle;
        frames.push(clonedeep(texture));
      }
      const anim = new PIXI.AnimatedSprite(frames);
      anim.x = this.app.screen.width / 2;
      anim.y = this.app.screen.height / 2;
      anim.anchor.set(0.5);
      anim.animationSpeed = 0.05;
      anim.play();
      this.app.stage.addChild(anim);
    },
  },
};
</script>
