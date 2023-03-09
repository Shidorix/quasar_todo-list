<template>
  <q-layout view="lHh lpR fFf">

    <q-header bordered class="bg-grey-7 text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
      </q-toolbar>
        
      <div class="text-h6 absolute q-pl-xl q-pt-sm ">
        {{ todayDate }}
      </div>

        <div class="q-px-lg q-pt-xl q-mb-md items-center row">
          <q-img src="../assets/logo2.png" style="width: 70px; height: 70px;" ></q-img>
          <div class="text-h3 q-pl-md">
            Shidorix's App
          </div>
          <q-img class="header-image absolute-top" src="../assets/header-img2.jpg"></q-img>
          
        </div>  

      <!-- <q-tabs align="left">
        <q-route-tab to="/page1" label="Page One" />
        <q-route-tab to="/page2" label="Page Two" />
        <q-route-tab to="/page3" label="Page Three" />
      </q-tabs> -->
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="200"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 185px); margin-top: 185px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item clickable v-ripple
            to="/" exact>
              <q-item-section avatar>
                <q-icon name="event" />
              </q-item-section>

              <q-item-section>
                ToDo
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple
            to="/help" exact>
              <q-item-section avatar>
                <q-icon name="help_outline" />
              </q-item-section>

              <q-item-section>
                Помощь
              </q-item-section>
            </q-item>
            
            <q-item clickable v-ripple
            to="/about" exact>
              <q-item-section avatar>
                <q-icon name="info" />
              </q-item-section>

              <q-item-section>
                Про нас
              </q-item-section>
            </q-item>

            
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/fon.jpg" style="height: 185px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../assets/monk.jpg">
            </q-avatar>
            <div class="text-weight-bold">Danila Mazepa</div>
            <div>@shidorix</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <router-view v-slot="{ Component }">
        <keep-alive>
          <transition name="route" mode="out-in">
          <component :is="Component" />
          </transition>
        </keep-alive>
      </router-view>
    </q-page-container>

    <q-footer bordered class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          <div>Ne pridumal</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { ref } from 'vue'
import { date } from 'quasar'

export default {
  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    }
  },
  computed: {
    todayDate() {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'D MMM YYYY')
    }
  }
}
</script>

<style lang="sass">
.header-image
  height: 100%
  z-index: -1
  opacity: 0.2

// .route-enter-active
//   opacity: 0
//   transform: translateY(-100px)


.route-enter-active,
.route-leave-active
  transition: all 0.2s ease-out

.route-leave-to,
.route-enter-from
  opacity: 0
  transform: translateY(100px)    
</style>