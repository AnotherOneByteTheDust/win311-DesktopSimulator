<template>
  <div id="icon">
    <img :src="setUrl(name)" />
    <p v-bind:class="isSelected">{{ name }}</p>
  </div>
</template>

<script>
export default {
  name: "Win311Icon",
  props: {
    name: {
      type: String,
      default: "None",
      required: true,
    },
  },
  methods: {
    setUrl(name) {
      let images = require.context("../assets/icons/", false, /\.png$/);
      return images("./" + name + ".png");
    },
    switchFocus(ev) {
      this.$store.commit("switchFocus", ev.currentTarget);
    },
  },
  computed: {
    isSelected() {
      let stored = this.$store.state.focus;
      return stored === this.$el ? "active" : "unactive";
    },
  },
  mounted() {
    this.$el.addEventListener("dblclick", this.switchFocus);
  },
};
</script>

<style lang="postcss" scoped>
#icon {
  display: flex;
  flex-direction: column;
  width: 80px;
  height: 80px;
  text-align: center;
  justify-content: center;

  & img {
    align-self: center;
  }

  & p {
    margin: 0;
  }
}

.active {
  background-color: #1484fc;
}
</style>
