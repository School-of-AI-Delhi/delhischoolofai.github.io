<template>
    <v-app>
        <NavBar></NavBar>
        <main>
            <router-view></router-view>
        </main>
        <v-footer height="auto" color="secondary" class="footer">
            <v-layout align-center justify-center>
                <div>&copy; {{ new Date().getFullYear() }} DSOAI</div>
            </v-layout>
        </v-footer>
    </v-app>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
export default {
    components: {
        NavBar
    }
}
</script>

<style>
    .footer div{
        color: rgb(192, 192, 192);
    }
</style>
