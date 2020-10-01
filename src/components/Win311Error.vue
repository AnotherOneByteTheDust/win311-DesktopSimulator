<template>
  <div id="window">
    <div class="inner">
      <div class="header">
        <div class="button">
          <div class="icon"></div>
        </div>
        <div class="text">{{ this.title }}</div>
      </div>
      <div class="content">
        <div class="header">
          <div class="stop-icon">
            <div class="inside">
              <span>STOP</span>
            </div>
          </div>
          <div class="description">
            <p>{{ this.description }}</p>
          </div>
        </div>
        <div class="footer">
          <button>OK</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import WinErrors from "@/assets/errors.json";

export default {
  name: "Win311Error",
  data() {
    return {
      title: {
        type: String,
        default: "",
      },
      description: {
        type: String,
        default: "",
      },
    };
  },
  mounted() {
    let i = Math.floor(Math.random() * WinErrors["title"].length);
    this.title = WinErrors["title"][i];
    this.description = WinErrors["description"][i];
  },
};
</script>

<style lang="postcss" scoped>
#window {
  position: absolute;
  height: 180px;
  width: 400px;
  background-color: blue;
  z-index: 1;
  top: 300px;
  left: 100px;
  display: flex;
  justify-content: center;
  align-items: center;

  & .inner {
    height: 170px;
    width: 390px;

    & .header {
      heigth: 20px;
      width: 100%;
      display: flex;
      flex-direction: row;

      & .button {
        height: 20px;
        width: 20px;
        background-color: #c2c2c2;
        display: flex;
        align-items: center;
        justify-content: center;

        & .icon {
          margin: auto;
          height: 2px;
          width: 14px;
          background-color: #404040;
        }
      }

      & .text {
        width: 369px;
        height: 20px;
        color: white;
        text-align: center;
        font-weight: bold;
      }
    }

    & .content {
      background-color: white;
      width: 100%;
      height: 149px;
      border-top: 1px solid #404040;

      & .header {
        display: flex;
        flex-direction: row;
        margin-top: 10px;
        width: 100%;
        heigth: 120px;

        & .stop-icon {
          width: 80px;
          height: 80px;
          display: flex;
          align-items: center;
          justify-content: center;
          color: white;

          & .inside {
            width: 50px;
            height: 50px;
            background-color: red;
            text-align: center;
            clip-path: polygon(
              30% 0%,
              70% 0%,
              100% 30%,
              100% 70%,
              70% 100%,
              30% 100%,
              0% 70%,
              0% 30%
            );

            & span {
              display: block;
              margin-top: 14px;
              font-weight: bold;
            }
          }
        }

        & .description {
          width: 300px;
          height: 90px;

          & p {
            margin: 10px;
            font-weight: bold;
          }
        }
      }

      & .footer {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 50px;
        width: 100%;

        & button {
          display: inline-block;
          border-color: black;
          font-weight: bold;
          height: 30px;
          width: 65px;
        }
      }
    }
  }
}
</style>
