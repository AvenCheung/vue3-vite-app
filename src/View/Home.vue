<template>
  <div class="about">
    <v-header />
    <v-sidebar />
    <div class="content_box" :class="{ content_collapse: collapse }">
      <v-tags></v-tags>
      <div class="content">
        <router-view v-slot="{ Component }">
          <transition name="move" mode="out-in">
            <keep-alive :include="tagsList">
              <component :is="Component"></component>
            </keep-alive>
          </transition>
        </router-view>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from '@vue/reactivity'
import { useStore } from 'vuex'
import vHeader from '../components/Header.vue'
import vSidebar from '../components/Sidebar.vue'
import vTags from '../components/Tags.vue'

export default {
  components: {
    vHeader,
    vSidebar,
    vTags
  },
  setup () {
    const store = useStore()
    const tagsList = computed(() => store.state.tagsList.map(item => item.name))

    const collapse = computed(() => store.state.collapse)

    return {
      tagsList,
      collapse
    }
  }
}
</script>
