<template>
  <header :class="['oc-header oc-header--1', { 'oc-header--sticky': sticky }]">
    <div class="oc-header__top">
      <div class="container">
        <div class="oc-header__text">
          Need help? <strong>0020 500 - MYMEDI - 000</strong>
        </div>
      </div>
    </div>
    <div class="oc-header__middle">
      <div class="container">
        <div class="oc-logo">
          <nuxt-link to="/">
            <img src="/img/logo.png" alt />
            <img class="sticky-logo" src="/img/sticky-logo.png" alt />
          </nuxt-link>
        </div>
        <div class="oc-menu--sticky" @click="handleOpenMenu()">
          <v-icon>mdi-menu</v-icon>
        </div>
        <div class="oc-header__right">
          <ul class="oc-header__icons">
            <li class="">
              <a
                href="#"
                class="active  oc-header__item open-search"
                @click.prevent="handleOpenDrawer('search')"
                ><i class="icon-magnifier"></i
              ></a>
            </li>
            <li class="oc-header__user">
              <a href="#" class="active  oc-header__item"
                ><i class="icon-user"></i
              ></a>
              <login-modal />
            </li>
            <li class="">
              <nuxt-link to="/shop/wishlist" class="oc-header__item"
                ><i class="fa fa-heart-o"></i> <span class="badge"></span
              ></nuxt-link>
            </li>
            <li class="oc-header__cart">
              <a href="#" class="active  oc-header__item"
                ><i class="icon-cart-empty"></i>
                <span class="badge"></span>
              </a>
              <cart-mini />
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div :class="['oc-navigation', { active: showNavigation }]">
      <div class="container">
        <div class="oc-navigation__left">
          <nav class="oc-main-menu">
            <render-list :list="mainMenu" className="menu" :product="product" />
          </nav>
        </div>
        <div class="oc-navigation__right">
          Need help? <strong>0020 500 - MYMEDI - 000</strong>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import { mainMenu } from "~/static/data/menu.json";
import RenderList from "~/components/elements/commons/RenderList";

export default {
  components: {
    RenderList
  },
  data() {
    return {
      mainMenu: mainMenu,
      product: null,
      showNavigation: false,
      sticky: false
    };
  },
  created() {
    if (process.browser) {
      window.addEventListener("scroll", this.handleScroll);
      this.handleScroll();
    }
  },
  destroyed() {
    if (process.browser) {
      window.removeEventListener("scroll", this.handleScroll);
    }
  },
  methods: {
    handleScroll() {
      let scroll = window.scrollY;
      if (scroll > 200) {
        this.sticky = true;
      } else {
        this.sticky = false;
      }
    },
    handleOpenMenu() {
      this.showNavigation = !this.showNavigation;
    }
  }
};
</script>
