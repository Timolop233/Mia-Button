<template>
  <transition name="fade" appear>
    <div class="footer">
      <div>
        <div class="author">
          <div>©2020</div>
          <template v-for="(item, index) in author" :key="index">
            <a style="margin-left: 5px" v-if="index > 0">&</a>
            <a
              style="margin-left: 5px"
              :href="item.url"
              target="_blank"
              >{{ item.name }}</a
            >
          </template>
        </div>
        <div class="info">
          <template v-for="(item, index) in info" :key="index">
            <div v-html="item"></div>
          </template>
        </div>
        <div>
            Created by
            <a href="https://github.com/blacktunes/voices-button-cli"
              >voices-button-cli</a
            >{{ " / "
            }}<a href="https://github.com/blacktunes/hiiro-button"
              >hiiro-button</a
            >
          </div>
      </div>
      <div class="text-right">
        <div class="git">
          <IBtn
            class="btn"
            :url="githubUrl"
            :img="githubPng"
          />
          <a :href="githubUrl" target="_blank">{{ t(INFO_I18N.toGithub) }}</a>
        </div>
        <div>{{ t(INFO_I18N.notOfficial) }}</div>
      </div>
    </div>
  </transition>
</template>

<script lang="ts">
import { useI18n } from 'vue-i18n'
import { INFO_I18N } from '@/assets/script/type'
import IBtn from '@/components/common/IconBtn.vue'
import Setting from '@/../setting/setting.json'
import githubPng from '@/assets/image/github-fill.png'

const FOOTER: {
  author?: {
    name: string;
    url?: string;
  }[];
  info?: string[];
  githubUrl?: string;
} = Setting['footer']

export default {
  components: {
    IBtn
  },
  setup() {
    const { t } = useI18n()

    return {
      INFO_I18N,
      t,
      author: FOOTER && FOOTER.author ? FOOTER.author : [],
      info: FOOTER && FOOTER.info ? FOOTER.info : [],
      githubUrl: FOOTER && FOOTER.githubUrl ? FOOTER.githubUrl : undefined,
      githubPng
    }
  }
}
</script>

<style lang="stylus" scoped>
.footer
  display flex
  justify-content space-between
  flex-wrap wrap
  padding 5px
  background-color #ebebeb
  font-size 12px
  color #333

  .author
    display flex
    align-items center

  .info
    margin-top 5px
    line-height 18px

  .text-right
    text-align right

    .git
      display flex
      align-items center

      a
        margin 0

      .btn
        margin 0 5px

@media only screen and (max-width 600px)
  .footer
    flex-direction column

    .text-right
      text-align left

      .git
        display flex
        align-items center

        .btn
          order 10

@media (prefers-color-scheme dark)
  .footer
    background-color #ddd
</style>
