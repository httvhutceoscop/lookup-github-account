<template>
  <div class="container-fluid pb-5">
    <div class="row">
      <div class="col-md-12">
        <h1 class="text-center p-5">Looking Up Github Account Information</h1>
      </div>
      <div class="col-md-6">
        <div id="settings">
          <form>
            <div class="form-group row">
              <label
                for="github-id"
                class="col-sm-2 col-form-label font-weight-bold"
              >
                GitHub ID <em class="text-danger">(*)</em>
              </label>
              <div class="col-sm-10">
                <input
                  required
                  type="text"
                  placeholder="httvhutceoscop"
                  id="github-id"
                  v-model="githubId"
                  class="form-control"
                />
              </div>
            </div><!-- end github id -->
            <div class="form-group row">
              <label
                for="github-id"
                class="col-sm-2 col-form-label font-weight-bold"
              >
                Common
              </label>
              <div class="col-sm-10">
                <div class="small mb-2">
                  You can customize the appearance of your
                  <code>Stats Card</code> or <code>Repo Card</code> however
                  you wish with URL params.
                </div>
                <div class="common__themes mb-2">
                  <div>
                    <strong
                      >Themes:
                      <span class="text-danger">{{
                        common.selectedTheme
                      }}</span></strong
                    >
                  </div>
                  <div
                    v-for="theme in themes"
                    :key="theme"
                    class="custom-control custom-radio custom-control-inline"
                  >
                    <input
                      type="radio"
                      :id="`${theme}-theme`"
                      v-model="common.selectedTheme"
                      class="custom-control-input"
                      :value="theme"
                    />
                    <label class="custom-control-label" :for="`${theme}-theme`">
                      {{ theme }}</label
                    >
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.titleColor"
                    placeholder="000000"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Card's title color <em>(hex color)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.textColor"
                    placeholder="000000"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Body text color color <em>(hex color)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.iconColor"
                    placeholder="000000"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Icons color if available <em>(hex color)</em>
                  </div>
                </div>
                <div class="form-check mb-2">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="common.hideBorder"
                    id="custom-hide-border"
                  />
                  <label class="form-check-label" for="custom-hide-border">
                    Hides the card's border <em>(boolean)</em>
                  </label>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    :disabled="common.hideBorder"
                    type="text"
                    v-model="common.borderColor"
                    placeholder="c0c0c0"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Card's border color <em>(hex color)</em>. (Does not apply
                    when <code>hide_border</code> is enabled)
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.bgColor"
                    placeholder="c0c0c0"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Card's background color <em>(hex color)</em> or a gradient
                    in the form of <em>angle,start,end</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="number"
                    v-model="common.cacheSeconds"
                    placeholder="c0c0c0"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    set the cache header manually
                    <em>(min: 1800, max: 86400)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.locale"
                    placeholder="c0c0c0"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    set the language in the card
                    <em>(e.g. cn, de, es, etc.)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="common.borderRadius"
                    placeholder="c0c0c0"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">Corner rounding on the card_</div>
                </div>
              </div>
            </div><!-- end common -->
            <div class="form-group row">
              <label
                for="inputPassword"
                class="col-sm-2 col-form-label font-weight-bold"
              >
                Stats Card
              </label>
              <div class="col-sm-10">
                <div class="d-flex align-items-center mb-1">
                  <input
                    type="text"
                    v-model="stats.hide"
                    placeholder="Ex: stars,commits,prs,.."
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Hides the specified items from stats <em>(Comma-separated values)</em>
                  </div>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.hideTitle"
                    id="stats-hide-title"
                  />
                  <label class="form-check-label" for="stats-hide-title">
                    Hides the stats card's title <em>(boolean)</em>
                  </label>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.hideRank"
                    id="stats-hide-rank"
                  />
                  <label class="form-check-label" for="stats-hide-rank">
                    Hides the stats card's rank <em>(boolean)</em>
                  </label>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.showIcons"
                    id="stats-show-icons"
                  />
                  <label class="form-check-label" for="stats-show-icons">
                    Show icons
                  </label>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.includeAllCommits"
                    id="stats-include-all-commits"
                  />
                  <label class="form-check-label" for="stats-include-all-commits">
                    Count total commits instead of just the current year commits <em>(boolean)</em>
                  </label>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.countPrivate"
                    id="stats-count-private"
                  />
                  <label class="form-check-label" for="stats-count-private">
                    Count private commits <em>(boolean)</em>
                  </label>
                </div>
                <div class="d-flex align-items-center mb-1">
                  <input
                    type="number"
                    v-model="stats.lineHeight"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Sets the line-height between text <em>(number)</em>
                  </div>
                </div>
                <div class="d-flex align-items-center mb-1">
                  <input
                    type="text"
                    v-model="stats.customTitle"
                    placeholder="Your custom title"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Sets a custom title for the card
                  </div>
                </div>
                <div class="form-check mb-1">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="stats.disableAnimations"
                    id="stats-disable-animations"
                  />
                  <label class="form-check-label" for="stats-disable-animations">
                    Disables all animations in the card <em>(boolean)</em>
                  </label>
                </div>
              </div>
            </div><!-- end stats card -->
            <div class="form-group row">
              <label
                for="inputPassword"
                class="col-sm-2 col-form-label font-weight-bold"
              >
                Language Card
              </label>
              <div class="col-sm-10">
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="language.hide"
                    placeholder="Ex: html,javascript,php"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Hide the languages specified from the card
                    <em>(Comma-separated values)</em>. <br />
                    ⚠️ <strong>Important</strong>: Language names should be
                    uri-escaped, as specified in
                    <a
                      href="https://en.wikipedia.org/wiki/Percent-encoding"
                      target="_blank"
                      >Percent Encoding</a
                    >
                    (i.e: <code>c++</code> should become <code>c%2B%2B</code>,
                    <code>jupyter notebook</code> should become
                    <code>jupyter%20notebook</code>, etc.) You can use
                    <a href="https://www.urlencoder.org/" target="_blank"
                      >urlencoder.org</a
                    >
                    to help you do this automatically.
                  </div>
                </div>
                <div class="form-check mb-2">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="language.hideTitle"
                    id="language-hide-title"
                  />
                  <label class="form-check-label" for="language-hide-title">
                    Hides the language card's title <em>(boolean)</em>
                  </label>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="language.layout"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Switch between two available layouts <code>default</code> &
                    <code>compact</code>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="number"
                    min="500"
                    v-model="language.cardWidth"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Set the card's width manually <em>(number). Min 500</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="number"
                    min="5"
                    v-model="language.langsCount"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Show more languages on the card, between 1-10, defaults to 5
                    <em>(number)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="language.excludeRepo"
                    placeholder="Ex: repo1,repo2,repo3,..."
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Exclude specified repositories
                    <em>(Comma-separated values)</em>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="language.customTitle"
                    placeholder="Your custom title"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">Sets a custom title for the card</div>
                </div>
              </div>
            </div><!-- end language card -->
            <div class="form-group row">
              <label
                for="inputPassword"
                class="col-sm-2 col-form-label font-weight-bold"
              >
                Wakatime Card
              </label>
              <div class="col-sm-10">
                <div class="form-check mb-2">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="wakatime.hideTitle"
                    id="wakatime-hide-title"
                  />
                  <label class="form-check-label" for="wakatime-hide-title">
                    Hides the wakatime card's title <em>(boolean)</em>
                  </label>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="number"
                    v-model="wakatime.lineHeight"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Sets the line-height between text <em>(number)</em>
                  </div>
                </div>
                <div class="form-check mb-2">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-model="wakatime.hideProgress"
                    id="wakatime-hide-progress"
                  />
                  <label class="form-check-label" for="wakatime-hide-progress">
                    Hides the progress bar and percentage <em>(boolean)</em>
                  </label>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="wakatime.customTitle"
                    placeholder="Your custom title"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">Sets a custom title for the card</div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="wakatime.layout"
                    placeholder="compact"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Switch between two available layouts <code>default</code> &
                    <code>compact</code>
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="number"
                    v-model="wakatime.langsCount"
                    min="5"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Limit number of languages on the card, defaults to all
                    reported langauges
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="wakatime.apiDomain"
                    class="mr-2 form-control form-control-sm col-3"
                  />
                  <div class="small">
                    Set a custom API domain for the card, e.g. to use services
                    like
                    <a href="https://github.com/mujx/hakatime" target="_blank"
                      >Hakatime</a
                    >
                    or
                    <a href="https://github.com/muety/wakapi" target="_blank"
                      >Wakapi</a
                    >
                  </div>
                </div>
                <div class="d-flex mb-2 align-items-center">
                  <input
                    type="text"
                    v-model="wakatime.range"
                    class="mr-2 form-control form-control-sm col-3"
                    placeholder="Ex: last_7_days"
                  />
                  <div class="small">
                    Request a range different from your WakaTime default, e.g.
                    <code>last_7_days</code>. See
                    <a
                      href="https://wakatime.com/developers#stats"
                      target="_blank"
                      >WakaTime API docs</a
                    >
                    for list of available options.
                  </div>
                </div>
              </div>
            </div><!-- end wakatime card -->
            <div class="form-group row text-center">
              <div class="col-sm-10">
                <button
                  @click="showResult"
                  :disabled="isValidData"
                  class="btn btn-secondary px-5"
                  type="button"
                >
                  Get result
                </button>
              </div>
            </div>
          </form>
        </div>
        <!-- End #settings -->
      </div>
      <div class="col-md-6">
        <p class="py-3" v-if="githubId">
          You're looking up the
          <strong>
            <a target="_blank" :href="`https://github.com/${githubId}`">{{
              githubId
            }}</a> </strong
          >'s information.
        </p>
        <div v-if="isResponse" id="result">
          <StatsCard :statsUrl="statsUrl"></StatsCard>
          <TopLanguagesCard :topLangsUrl="topLangsUrl"></TopLanguagesCard>
          <WakatimeCard :wakatimeUrl="wakatimeUrl"></WakatimeCard>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12 text-center">
        Made with ❤️ and VueJS.
      </div>
    </div>
  </div>
</template>

<script>
import StatsCard from "./StatsCard.vue";
import TopLanguagesCard from "./TopLanguagesCard.vue";
import WakatimeCard from "./WakatimeCard.vue";
const readmeStatsApi = "https://github-readme-stats.vercel.app/api";
export default {
  name: "HelloWorld",
  data() {
    return {
      common: {
        titleColor: "",
        textColor: "",
        iconColor: "",
        borderColor: "",
        bgColor: "",
        hideBorder: false,
        selectedTheme: "",
        cacheSeconds: 1800,
        locale: "",
        borderRadius: "",
      },
      stats: {
        hide: "",
        hideTitle: false,
        hideRank: false,
        showIcons: true,
        includeAllCommits: true,
        countPrivate: false,
        lineHeight: null,
        customTitle: "",
        disableAnimations: false,
      },
      language: {
        hide: "",
        hideTitle: false,
        layout: "default", // compact
        cardWidth: 500,
        langsCount: 5,
        excludeRepo: "",
        customTitle: "",
      },
      wakatime: {
        hideTitle: false,
        lineHeight: null,
        hideProgress: false,
        customTitle: "",
        layout: "default", // compact
        langsCount: 5,
        apiDomain: "",
        range: "",
      },
      githubId: "",
      statsUrl: "",
      topLangsUrl: "",
      wakatimeUrl: "",
      isResponse: false,
      themes: [
        "dark",
        "radical",
        "merko",
        "gruvbox",
        "tokyonight",
        "onedark",
        "cobalt",
        "synthwave",
        "highcontrast",
        "dracula",
      ],
    };
  },
  components: {
    StatsCard,
    TopLanguagesCard,
    WakatimeCard,
  },
  computed: {
    isValidData() {
      return this.githubId == "";
    },
  },
  methods: {
    showResult() {
      this.isResponse = true;
      this.statsUrl = `${readmeStatsApi}?username=${this.githubId}`;
      this.topLangsUrl = `${readmeStatsApi}/top-langs/?username=${this.githubId}`;
      this.wakatimeUrl = `${readmeStatsApi}/wakatime/?username=${this.githubId}`;
      this.renderStatsUrl();
      this.renderLanguageUrl();
      this.renderWakatimeUrl();

      // remove character # in url
      this.statsUrl = this.statsUrl.replace(/#/g, "");

      // scroll top
      const intervalId = setInterval(() => {
          if (window.pageYOffset === 0) {
              clearInterval(intervalId);
          }
          window.scroll(0, 0);
      }, 0);
      console.log(this.statsUrl);
      console.log(this.topLangsUrl);
    },
    renderWakatimeUrl() {
      if (this.wakatime.hideTitle === true) {
        this.wakatimeUrl += `&hide_title=${this.wakatime.hideTitle}`;
      }
      if (this.wakatime.lineHeight > 0) {
        this.wakatimeUrl += `&line_height=${this.wakatime.lineHeight}`;
      }
      if (this.wakatime.hideProgress === true) {
        this.wakatimeUrl += `&hide_progress=${this.wakatime.hideProgress}`;
      }
      if (this.wakatime.customTitle !== "") {
        this.wakatimeUrl += `&custom_title=${this.wakatime.customTitle}`;
      }
      if (this.wakatime.layout === "compact") {
        this.wakatimeUrl += `&layout=${this.wakatime.layout}`;
      }
      if (this.wakatime.langsCount >= 5) {
        this.wakatimeUrl += `&langs_count=${this.wakatime.langsCount}`;
      }
      if (this.wakatime.apiDomain !== "") {
        this.wakatimeUrl += `&api_domain=${this.wakatime.apiDomain}`;
      }
      if (this.wakatime.range !== "") {
        this.wakatimeUrl += `&range=${this.wakatime.range}`;
      }
    },
    renderLanguageUrl() {
      if (this.language.hide !== "") {
        this.topLangsUrl += `&hide=${this.language.hide}`;
      }
      if (this.language.hideTitle === true) {
        this.topLangsUrl += `&hide_title=${this.language.hideTitle}`;
      }
      if (this.language.layout === "compact") {
        this.topLangsUrl += `&layout=${this.language.layout}`;
      }
      if (this.language.cardWidth >= 500) {
        this.topLangsUrl += `&card_width=${this.language.cardWidth}`;
      }
      if (this.language.langsCount >= 5) {
        this.topLangsUrl += `&langs_count=${this.language.langsCount}`;
      }
      if (this.language.excludeRepo !== "") {
        this.topLangsUrl += `&exclude_repo=${this.language.excludeRepo}`;
      }
      if (this.language.customTitle !== "") {
        this.topLangsUrl += `&custom_title=${this.language.customTitle}`;
      }
    },
    renderStatsUrl() {
      if (this.stats.hide != "") {
        this.statsUrl += `&hide=${this.stats.hide}`;
      }
      if (this.stats.hideTitle === true) {
        this.statsUrl += `&hide_title=${this.stats.hideTitle}`;
      }
      if (this.stats.hideRank === true) {
        this.statsUrl += `&hide_rank=${this.stats.hideRank}`;
      }
      if (this.stats.showIcons) {
        this.statsUrl += `&show_icons=true`;
      }
      if (this.stats.includeAllCommits === true) {
        this.statsUrl += `&include_all_commits=${this.stats.includeAllCommits}`;
      }
      if (this.stats.countPrivate) {
        this.topLangsUrl += `&count_private=true`;
      }
      if (this.stats.lineHeight > 0) {
        this.statsUrl += `&include_all_commits=${this.stats.lineHeight}`;
      }
      if (this.stats.customTitle != "") {
        this.statsUrl += `&custom_title=${this.stats.customTitle}`;
      }
      if (this.stats.disableAnimations === true) {
        this.statsUrl += `&disable_animations=${this.stats.disableAnimations}`;
      }

      // Apply common style
      if (this.common.selectedTheme != "") {
        this.statsUrl += `&theme=${this.common.selectedTheme}`;
      }
      if (this.common.titleColor != "") {
        this.statsUrl += `&title_color=${this.common.titleColor}`;
      }
      if (this.common.textColor != "") {
        this.statsUrl += `&text_color=${this.common.textColor}`;
      }
      if (this.common.iconColor != "") {
        this.statsUrl += `&icon_color=${this.common.iconColor}`;
      }
      if (this.common.borderColor != "" && this.stats.hideBorder === false) {
        this.statsUrl += `&border_color=${this.common.borderColor}`;
      }
      if (this.common.bgColor != "") {
        this.statsUrl += `&bg_color=${this.common.bgColor}`;
      }
      if (this.stats.hideBorder === true) {
        this.statsUrl += `&hide_border=${this.stats.hideBorder}`;
      }
      if (this.stats.cacheSeconds >= 1800) {
        this.statsUrl += `&cache_seconds=${this.stats.cacheSeconds}`;
      }
      if (this.common.locale != "") {
        this.statsUrl += `&locale=${this.common.locale}`;
      }
      if (this.common.borderRadius != "") {
        this.statsUrl += `&border_radius=${this.common.borderRadius}`;
      }
    },
  },
};
</script>

