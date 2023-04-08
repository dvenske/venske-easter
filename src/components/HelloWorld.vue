<template>
  <div>
    <canvas></canvas>
    <div class="play">
      <img
        width="150px"
        @click="playAudio()"
        src="https://i.pinimg.com/originals/56/4d/ff/564dff1560e92dd38be7141e8a94801e.png"
      />
      <div style="margin-top: -30px">(Turn up volume)</div>
    </div>
    <div class="options" v-if="showOptions && option == ''">
      <button @click="option = 'drive'" style="background-color: cyan">
        Drive</button
      ><br />
      <button @click="option = 'stroll'" style="background-color: magenta">
        Digital Stroll
      </button>
    </div>
    <div class="options" v-if="option == 'drive'">
      <button @click="option = ''" style="background-color: green">BACK</button
      ><br />
      Very well. Get in your car and drive up Colombo Street. When you find
      hell's neighbor you will have your first clue.<br />
      Your father will provide you with the coded answer.
    </div>
    <div class="options" v-if="option == 'stroll'">
      <button @click="option = ''" style="background-color: green">BACK</button
      ><br />
      Very well... Google maps is pretty impressive. You can almost feel like
      you're walking down a street. And sometimes you can even turn back time.
      What used to be where Dominos is? Cashmere _ _ _ _ _
      <br />
      Your father will provide you with the coded answer.
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      audio: null,
      showOptions: false,
      option: "",
    };
  },
  props: {
    msg: String,
  },
  methods: {
    playAudio: function () {
      if (this.audio) {
        this.audio.pause();
        this.audio.currentTime = 0;
        this.audio.play();
      } else {
        this.audio = new Audio(require("@/assets/intro.wav"));
        this.audio.play();
        this.showOptions = true;
      }
    },
  },
  mounted() {
    const canvas = document.querySelector("canvas");
    const ctx = canvas.getContext("2d");
    const colors = [
      "#b4b2b5",
      "#dfd73f",
      "#6ed2dc",
      "#66cf5d",
      "#c542cb",
      "#d0535e",
      "#3733c9",
    ];
    let rAF;
    console.log(rAF);

    canvas.width = innerWidth;
    canvas.height = innerHeight;

    function texts(color) {
      ctx.font = "10vh Bungee Outline";
      ctx.shadowBlur = 30;
      ctx.shadowColor = color;
      ctx.fillStyle = color;
      ctx.setTransform(1, -0.15, 0, 1, 0, -10);
      ctx.fillText("Easter", innerWidth / 2, innerHeight / 2.5 - 5);

      ctx.fillStyle = "white";
      ctx.shadowBlur = 30;
      ctx.shadowColor = color;
      ctx.fillText("Easter", innerWidth / 2, innerHeight / 2.5);

      ctx.font = "8vh Bungee Inline";
      ctx.shadowBlur = 30;
      ctx.shadowColor = color;
      ctx.fillStyle = "#fff";
      ctx.setTransform(1, -0.15, 0, 1, 0, -10);
      ctx.fillText(
        "HUNT 2023",
        innerWidth / 2,
        innerHeight / 2.5 + innerHeight / 10
      );

      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
    }

    function glitch() {
      rAF = window.requestAnimationFrame(glitch);

      ctx.fillStyle = "#1a191c";
      ctx.fillRect(0, 0, innerWidth, innerHeight);

      texts(colors[Math.floor(Math.random() * 7)]);
      ctx.shadowBlur = 0;
      ctx.shadowColor = "none";
      ctx.setTransform(1, 0, 0, 1, 0, 0);

      for (let i = 0; i < 1000; i++) {
        ctx.fillStyle = `rgba(255, 255, 255, ${Math.random() * 0.01})`;
        ctx.fillRect(
          Math.floor(Math.random() * innerWidth),
          Math.floor(Math.random() * innerHeight),
          Math.floor(Math.random() * 30) + 1,
          Math.floor(Math.random() * 30) + 1
        );

        ctx.fillStyle = `rgba(0,0,0,${Math.random() * 0.1})`;
        ctx.fillRect(
          Math.floor(Math.random() * innerWidth),
          Math.floor(Math.random() * innerHeight),
          Math.floor(Math.random() * 25) + 1,
          Math.floor(Math.random() * 25) + 1
        );
      }

      ctx.fillStyle = colors[Math.floor(Math.random() * 40)];
      ctx.fillRect(
        Math.random() * innerWidth,
        Math.random() * innerHeight,
        Math.random() * innerWidth,
        Math.random() * innerHeight
      );
      ctx.setTransform(1, 0, 0, 0.8, 0.2, 0);
    }

    glitch();

    window.addEventListener("resize", () => {
      canvas.width = innerWidth;
      canvas.height = innerHeight;
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.play {
  text-align: center;
  color: white;
  font-family: Verdana;
  width: 150px;
  height: 150px;
  position: absolute;
  top: 0px;
  left: calc(50% - 75px);
}
.options {
  position: absolute;
  bottom: 100px;
  font-size: 16pt;
  width: 300px;
  text-align: center;
  left: calc(50% - 150px);
  font-family: Verdana;
  color: white;
}
button {
  font-family: Bungee Inline;
  font-size: 16pt;
  margin-bottom: 10px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
