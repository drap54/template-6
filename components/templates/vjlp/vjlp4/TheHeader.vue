<template>
  <header id="strip-container" class="container-flex h-100">
    <a id="login-btn" :href="loginURL" class="login hvr-pulse">
      <div class="animated fadeIn">
        <i class="material-icons">exit_to_app</i>
        <div class="login-txt">{{ loginText }}</div>
      </div>
    </a>
    <div class="container">
      <div class="row row-eq-height">
        <div id="strip" class="col-12 strip">
          <div class="strip-container animated fadeIn" style="margin-top: 56.5px;">
            <div class="logo animated fadeIn"></div>
            <div class="game-logo animated bounce delay-1s"></div>
            <div class="title animated fadeIn delay-1s"></div>
            <div>
              <h2>
                <p style="text-align: center;">
                  <b>
                    <br />
                  </b>
                </p>
                <p style="text-align: center;">
                  <b>
                    <font color="#ffff02">{{ gameLargeSubtitle }}</font>
                  </b>
                </p>
                <div style="text-align: center;">
                  <span style="font-size: 0.75em; background-color: initial;"
                    v-html="bannerSubtitle"
                  >
                  </span>
                </div>
                <p>
                  <br />
                </p>
              </h2>
            </div>
            <!-- <div class="co-brand"></div>-->
            
            <!-- id="signup-btn" -->
            <a
              :href="signUpURL"
              class="button button-lrg"
              style="display:block;margin-top: 0px;"
            >{{ signUpText }}</a>
            <!-- show button-->
          </div>
          <div class="small-terms" v-html="bannerTerms">
            <!-- <a href="#terms" class="link-terms-conditions ctac">利用規約</a>に同意します。 -->
          </div>
        </div>
      </div>
    </div>
    <style>
    :root {
      --bg-image: url("{{ images.promo_bg_desktop }}");
      --bg-image-m: url("{{ images.promo_bg_mobile }}");
      --game-logo: url("{{ images.promo_game_logo }}");
      --game-title: url("{{ images.promo_game_image }}");
    }
    </style>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    loginText: {
      type: String,
      required: true,
    },
    loginURL: {
      type: String,
      required: true,
    },
    gameLargeSubtitle: {
      type: String,
      required: true,
    },
    gameSmallSubtitle: {
      type: String,
      required: true,
    },
    gameSmallSubtitleHighlighted: {
      type: Array,
      required: false,
    },
    signUpText: {
      type: String,
      required: true,
    },
    signUpURL: {
      type: String,
      required: true,
    },
    termsLinkText: {
      type: Array,
      required: false,
    },
    termsText: {
      type: String,
      required: true,
    },
    images: {
      type: Object,
      required: true,
    }
  },
  computed: {
    bannerSubtitle: function () {
      let gameSubtitles = this.gameSmallSubtitle
        .split(/\r?\n/)
        .filter(sub => sub)
        .map(sub => sub.slice(-1) === '\\'
          ? sub.substring(0, sub.length - 1) : sub
        );
      let idx = 0;
      this.gameSmallSubtitleHighlighted.filter(phrase => phrase)
        .forEach(phrase => {
          while (gameSubtitles.length > idx) {
            if (gameSubtitles[idx].includes(phrase)) {
              gameSubtitles[idx] = gameSubtitles[idx].replace(phrase, `<font color="#ffff02"><b>${phrase}</b></font>`);
              break;
            } else {
              idx++;
            }
          }
        });
      return gameSubtitles.reduce((oldVal, newVal) => {
        return oldVal + '<br />' + newVal;
      });
    },
    bannerTerms: function () {
      let termsText = this.termsText;
      this.termsLinkText.filter(linkText => linkText)
        .forEach(linkText => {
          if (this.termsText.includes(linkText)) {
            termsText = termsText.replace(linkText, `<a href="#terms" class="link-terms-conditions ctac">${linkText}</a>`);
          }
        });
      return termsText;
    }
  }
};
</script>

<style scoped>
#strip-container {
  background: var(--bg-image) no-repeat top center;
  background-size: cover;
}
@media only screen and (max-width: 575px) {
  #strip-container {
    background: var(--bg-image-m) no-repeat center;
    background-size: cover;
  }
}
.game-logo {
  background: var(--game-logo) no-repeat center;
  background-size: contain;
  width: auto;
  height: 200px;
  z-index: 999999;
}
.title {
  background: var(--game-title) no-repeat center;
  background-size: contain;
  width: auto;
  height: 50px;
  z-index: 999999;
}
/* .co-brand {
  background: url("co-branded-logo.png") no-repeat center;
  background-size: contain;
  width: 100%;
  height: 100px;
} */
.painbg {
  background: rgb(0, 79, 184);
  background: linear-gradient(
    180deg,
    rgba(0, 79, 184, 1) 0%,
    rgba(0, 175, 255, 1) 50%
  );
}
</style>