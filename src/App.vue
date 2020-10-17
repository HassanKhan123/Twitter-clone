<template>
<div id="app">
    {{ user.userName }} - {{ fullName }} <strong>Followers: </strong>{{ followers }}
    <button @click="followUser">Follow</button>
</div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                userName: "HassanKhan123",
                firstName: "Hassan",
                lastName: "Khan",
                email: "hassan@gmail.com",
                isAdmin: true,
            },
        };
    },
    watch: {
        followers(newFollowers, oldFollowers) {
            if (oldFollowers < newFollowers) {
                console.log(`${this.user.userName} has gained followers`)
            }
        }
    },
    computed: {
        fullName() {
            return `${this.user.firstName} ${this.user.lastName}`;
        },
    },
    methods: {
        followUser() {
            this.followers++;
        },
    },
    mounted() {
        this.followUser()
    }
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    display: flex;
    flex-direction: column;
    text-align: center;
}
</style>
