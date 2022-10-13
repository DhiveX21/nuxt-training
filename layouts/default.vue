<template>
    <div>
       <header class="p-5 bg-white shadow-lg flex justify-between items-center">
            <nuxt-link to="/">InstagramClone</nuxt-link>
            <ul class="flex gap-3 items-center" v-if="isLoggedIn">
                <li>
                    <a href="/homes">Home</a>
                </li>
                <li>
                    <button class="p-3 bg-blue-500 text-white" @click="logOut">
                        Log out
                    </button>
                </li>
            </ul>
       </header>
       <main class="w-1/2 mx-auto mt-5">
            <nuxt/>
       </main>
    </div>
</template>
<script>
    import Cookie from "js-cookie";
    export default {
        data(){
            return {
                cookie : Cookie.get("idToken") || ""
            }
        },
        computed: {
            isLoggedIn(){
                return this.$store.state.auth.isLoggedIn;
            }
        },
        methods : {
            logOut(){
                this.$store.dispatch("auth/logout");
                this.cookie = ""
                Cookie.remove("idToken")
                window.location.href = "/auth/login"
            }
        }
    }
</script>