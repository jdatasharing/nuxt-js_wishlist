<template lang="html">
    <div v-if="localStorage.getItem('x-token-site') != ' '" class="ps-block--user-header">
        <div class="ps-block__left">
            <i class="icon-user"></i>
        </div>
        <div class="ps-block__right">
            <nuxt-link to="/account/login">
                {{ $t('header.login') }}
            </nuxt-link>
            <nuxt-link to="/account/register">
                {{ $t('header.register') }}
            </nuxt-link>
             <a href='#' @click='logout'>
              Logout
            </a>
        </div>
    </div>
    <div v-else class="ps-block--user-account">
        <i class="icon-user"></i>
        <div class="ps-block__content">
            <ul class="ps-list--arrow">
                <li v-for="link in accountLinks" :key="link.text">
                    <nuxt-link :to="link.url">
                        {{ link.text }}
                    </nuxt-link>
                </li>
                <li class="ps-block__footer">
                    <a href="#" @click.prevent="handleLogout">
                        Logout
                    </a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
    name: 'HeaderUserArea',
    computed: {
        ...mapState({
            isLoggedIn: state => state.auth.isLoggedIn
        })
    },
    data() {
        return {
            accountLinks: [
                {
                    text: 'Account Information',
                    url: '/account/user-information'
                },
                {
                    text: 'Notifications',
                    url: '/account/notifications'
                },
                {
                    text: 'Invoices',
                    url: '/account/invoices'
                },
                {
                    text: 'Address',
                    url: '/account/addresses'
                },
                {
                    text: 'Recent Viewed Product',
                    url: '/account/recent-viewed-product'
                },
                {
                    text: 'Wishlist',
                    url: '/account/wishlist'
                }
            ]
        };
    },
    methods: {
        handleLogout() {
            this.$store.dispatch('auth/setAuthStatus', false);
        },
        logout()
        {
          
            console.log("Logout called");
            // let x = cookies.get('x-access-token');
           let x = localStorage.getItem('x-token-site');

            this.$axios.post('http://127.0.0.1:8000/api/v1/logout').then((resp) => {
         
          this.$axios.setHeader('Authorization', 'Bearer ' + x)
        })
        console.log("bdho code run thyo aama ");
        console.log("Logout Work");
        this.$axios.setToken(false);
        // cookies.remove('x-access-token');
        localStorage.removeItem('x-token-site');
        }
    }
};
</script>

<style lang="scss" scoped></style>
