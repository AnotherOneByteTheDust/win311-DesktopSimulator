<template>
  <div id="window">
    <div class="header">
      <div class="left-icon">
        <div class="icon"></div>
      </div>
      <div class="center">
        {{ title }}
      </div>
      <div class="right-icon">
        <div class="icon"></div>
      </div>
    </div>
    <div class="content">
      <div class="options">
        <span v-for="(option, index) in options" :key="index">
          {{ option }}
        </span>
      </div>
      <div class="icon-list">
        <win311-icon
          v-for="(i, index) in icons"
          :key="index"
          :name="i"
          :class="i + index + title"
        ></win311-icon>
      </div>
    </div>
    <div class="footer">
      <p>{{ this.footerMsg }}</p>
    </div>
  </div>
</template>

<script>
import Win311Icon from "@/components/Win311Icon.vue";
import Config from "@/assets/windows.json";

export default {
  name: "Win311Window",
  components: {
    "win311-icon": Win311Icon,
  },
  data() {
    return {
      options: ["Settings", "Help"],
      icons: [],
      title: "None",
      footerMsg: "Select an app to open",
    };
  },
  props: {
    type: {
      type: String,
      default: "None",
      required: true,
      validator: (v) => {
        return Config[v];
      },
    },
  },
  methods: {
    switchMsg() {
      let el = this.$store.state.focus;
      let children = this.$el.querySelector(".icon-list").children;

      for (let i = 0; i < children.length; i++) {
        if (children[i] === el) {
          this.footerMsg =
            children[i].childNodes[1].textContent + " has been opened.";
        }
      }
    },
  },
  mounted() {
    this.title = Config[this.type].title;
    this.icons = Config[this.type].icons;
    this.$el.addEventListener("dblclick", this.switchMsg);
  },
};
</script>

<style lang="postcss" scoped>
:root {
  --bgColor: #c2c2c2;
  --iconsColor: #404040;
  --topCenterColor: white;
  --windowContentBg: white;
}

#window {
  position: absolute;
  background-color: var(--bgColor);
  height: 450px;
  width: 600px;
  display: flex;
  flex-direction: column;
  margin: auto;

  & .header {
    width: 100%;
    height: 30px;
    display: flex;
    color: white;
    font-weight: bold;

    & .left-icon {
      height: 100%;
      width: 30px;
      display: flex;
      align-items: center;
      justify-content: center;

      & .icon {
        margin: auto;
        height: 2px;
        width: 20px;
        background-color: var(--iconsColor);
      }
    }
    & .center {
      background-color: #041c3d;
      margin-top: 2px;
      width: 540px;
      text-align: center;
      vertical-align: middle;
    }
    & .right-icon {
      height: 100%;
      width: 30px;
      background-color: black;
      clip-path: polygon(50% 70%, 30% 30%, 70% 30%);
    }
  }

  & .content {
    width: 98.5%;
    background-color: var(--windowContentBg);
    height: 390px;
    margin: auto;

    & .options {
      width: 100%;
      height: 30px;
      border-bottom: 1px solid black;
      display: flex;
      flex-direction: row;
      align-items: center;

      & span {
        margin: 0px 6px 0px 6px;
      }
    }

    & .icon-list {
      display: flex;
      flex-direction: row;
      margin: 4px;
      flex-wrap: wrap;
      justify-content: flex-start;
    }
  }
  & .footer {
    width: 100%;
    height: 30px;

    & p {
      margin: 5px 0px 0px 6px;
    }
  }
}
</style>
