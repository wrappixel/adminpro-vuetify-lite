<script setup lang="ts">
import { ref, shallowRef, onMounted } from 'vue';
import { RouterView } from 'vue-router';
import { useDisplay } from "vuetify";
import sidebarItems from './vertical-sidebar/sidebarItem';
import NavGroup from './vertical-sidebar/NavGroup/index.vue';
import NavItem from './vertical-sidebar/NavItem/index.vue';
import Logo from './logo/Logo.vue';
// Icon Imports
import Header from '@/components/Layout/header/index.vue'
import BuyNow from '@/components/Layout/sidebar/Buynow/index.vue'
const drawer = ref(undefined || true);
const innerW = window.innerWidth;
const { mdAndUp, mdAndDown } = useDisplay();
onMounted(() => {
    if (innerW < 950) {
        drawer.value = !drawer.value;
    }
});
const sidebarMenu = shallowRef(sidebarItems);
const sDrawer = ref(true);

</script>

<template>
    <v-app-bar elevation="10">
        <div class="pe-5">
            <div class="">
                <Logo />
            </div>
        </div>
        <v-app-bar-nav-icon class="" @click="sDrawer = !sDrawer" />
        <v-spacer />
        <Header />
    </v-app-bar>
    <v-main>
        <!-- ---------------------------------------------- -->
        <!---Sidebar -->
        <!-- ---------------------------------------------- -->
        <v-navigation-drawer left :permanent="mdAndUp" class="leftSidebar bg-muted border-right-0" elevation="10" app
            :temporary="mdAndDown" v-model="sDrawer" expand-on-hover>
            <perfect-scrollbar class="scrollnavbar">
                <div class="sidebar_profile border-bottom">
                    <v-list class="bg-muted">
                        <v-list-item class="pa-4 pb-0 ml-1">
                            <v-list-item-title class="text-h6 mb-1">Julia Roberts</v-list-item-title>
                            <v-list-item-subtitle class="text-subtitle-1">Web Designer</v-list-item-subtitle>
                            <template v-slot:prepend class="me-0">
                                <v-avatar size="45" class="me-0">
                                    <img src="@/assets/images/profile/user2.jpg" width="50" />
                                </v-avatar>
                            </template>

                        </v-list-item>
                    </v-list>
                </div>
                <v-list class="py-5 px-4 bg-muted" density="compact">
                    <!---Menu Loop -->
                    <template v-for="(item, i) in sidebarMenu">
                        <!---Item Sub Header -->
                        <NavGroup :item="item" v-if="item.header" :key="item.title" />
                        <!---Single Item-->
                        <NavItem :item="item" v-else class="leftPadding" />
                        <!---End Single Item-->
                    </template>
                    <!-- <Moreoption/> -->
                </v-list>
                <div>
                    <BuyNow/>
                </div>
            </perfect-scrollbar>
        </v-navigation-drawer>
        <v-container fluid class="page-wrapper">
            <div class="maxWidth">
                <RouterView />
            </div>
        </v-container>
    </v-main>
</template>
