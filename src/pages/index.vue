<template>
  <div class="container home-page">
    <section class="section header clearfix">
      <header class="header__title color--white">
        <h2>
          {{ $t('nouns.adidas') }}
          <br/>
          {{ $t('meta.title') }}
        </h2>
        <h5>{{ $t('meta.description') }}</h5>
      </header>
      <adidoescode/>
    </section>
    <section class="section kpis color--white" v-if="orderedKpis.length">
      <div class="kpi__list">
        <kpi-item class="kpi"
            v-for="(kpi, index) in orderedKpis"
            :key="index"
            :title="kpi.title"
            :value="kpi.value"/>
      </div>
    </section>
    <section class="section open-source" id="open-source">
      <div class="links">
        <nuxt-link :to="localePath('contributing')" class="btn btn--blue">
          {{ $t('links.guidelines') }}
        </nuxt-link>
        <a class="btn btn-tertiary-dark"
            :href="$t('href.github')"
            target="_blank"
            rel="nofollow noreferrer noopener">
          <i class="fab fa-github"></i>
          {{ $t('links.github') }}
        </a>
      </div>
      <div class="tiles grid">
        <a class="link grid-item"
            v-for="item in openSource"
            :class="{ 'grid-item--large': item.name === featuredFlag.name }"
            :key="item.id"
            :href="item.url"
            target="_blank"
            rel="nofollow noreferrer noopener">
          <card :title="(item.config && item.config.display && item.config.display.name) || item.name"
              :image="item.config.imageUrl"
              :background-color="item.config.backgroundColor"
              :type="item.type">
            <div class="tile__footer__subheader__text">
              {{ (item.config && item.config.display && item.config.display.description) || item.description }}
            </div>
          </card>
        </a>
      </div>
    </section>
    <section class="section tech-stack" id="tech-stack">
      <div class="deco">
        <div class="title">
          {{ $t('views.home.platformTechStack') }}
        </div>
        <div class="separator separator--right"></div>
      </div>
      <tech-stack-block v-for="(techStackBlock, index) in orderedTechStack"
          :key="index"
          :title="techStackBlock.title"
          :tags="techStackBlock.tags"
          :image-url="techStackBlock.imageUrl">
        <div v-html="techStackBlock.summary.html"></div>
      </tech-stack-block>
    </section>
    <section class="section events" id="events">
      <div class="deco">
        <div class="title">
          {{ $t('views.home.events') }}
        </div>
        <div class="separator separator--right"></div>
      </div>
      <div class="events__video">
        <iframe title="youtube-sample"
            frameborder="0"
            height="100%"
            width="100%"
            :src="$t('href.eventVideo')"
            allowfullscreen>
        </iframe>
      </div>
      <div class="publications">
        <blog-post v-for="(post, index) in events"
            :key="index"
            :title="post.title"
            :subtitle="post.subtitle"
            :summary="post.summary.html"
            :url="post.url"
            :url-label="post.urlLabel"
            :likes="post.likes"/>
      </div>
    </section>
    <section class="section careers" id="careers">
      <div class="deco">
        <div class="title">
          {{ $t('views.home.careers') }}
        </div>
        <div class="separator separator--right"></div>
      </div>
      <div class="careers__locations tiles">
        <a class="careers__location"
            v-for="item in orderedCareers"
            :key="item.id"
            :href="item.url"
            target="_blank"
            rel="nofollow noreferrer noopener">
          <card :title="item.title"
              :image="item.imageUrl"
              :type="item.location"
              :footer="false"/>
        </a>
      </div>
      <div class="careers__btn">
        <a class="btn btn-primary"
            :href="$t('href.careers.openPositions')"
            target="_blank"
            rel="nofollow noreferrer noopener">
          {{ $t('links.openPositions') }}
        </a>
      </div>
    </section>
  </div>
</template>

<script src="./index.js"></script>
<style lang="scss" src="./index.scss"></style>
