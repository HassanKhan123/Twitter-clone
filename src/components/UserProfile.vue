<template>
<div class="user-profile">
    <div class="user-profile__user-panel">
        <h1 class="user-profile__user-name">@{{ user.userName }}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__follower-count">
            <strong>Followers: </strong>{{ followers }}
        </div>
        <CreateTweetPanel @add-tweet="addTweet" />
    </div>

    <div class="user-profile__tweets-wrapper">
        <div class="user-profile__tweets">
            <TweetItem v-for="tweet in user.tweets" :key="tweet.id" :userName="user.userName" :tweet="tweet" @favourite="toggleFavourite" />
        </div>
    </div>
</div>
</template>

<script>
import TweetItem from "./TweetItem";
import CreateTweetPanel from "./CreateTweetPanel";
export default {
    name: "UserProfile",
    components: {
        TweetItem,
        CreateTweetPanel,
    },
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                userName: "_HassanKhan123",
                firstName: "Hassan",
                lastName: "Khan",
                email: "hassan@gmail.com",
                isAdmin: true,
                tweets: [{
                        id: 1,
                        content: "Twitter is amazing",
                    },
                    {
                        id: 2,
                        content: "Learning Vue",
                    },
                ],
            },
        };
    },
    watch: {
        followers(newFollowers, oldFollowers) {
            if (oldFollowers < newFollowers) {
                console.log(`${this.user.userName} has gained followers`);
            }
        },
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
        toggleFavourite(id) {
            console.log(`Favourited tweet #${id}`);
        },
        addTweet(content) {
            this.user.tweets.unshift({
                id: this.user.tweets.length + 1,
                content,
            });
        },
    },
    mounted() {
        this.followUser();
    },
};
</script>

<style lang="scss" scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 90%;
    padding: 50px 5%;

    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #dfe3e8;

        h1 {
            margin: 10px;
        }

        .user-profile__admin-badge {
            background-color: purple;
            color: white;
            border-radius: 5px;
            margin-right: auto;
            padding: 0 10px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .user-profile__follower-count {
            margin-top: 5px;
            margin-bottom: 10px;
        }

        .user-profile__create-tweet {
            display: flex;
            flex-direction: column;
            border-top: 1px solid #dfe3e8;
            padding-top: 10px;

            &.--exceeded {
                color: red;
                // border: 1px solid red;

                button {
                    background-color: red;
                    border: none;
                    color: white;
                }
            }
        }
    }

    .user-profile__tweets-wrapper {
        display: grid;
        grid-gap: 10px;
    }
}
</style>
