<template>
<div class="tweet-item" @click="favouriteTweet(tweet.id)">
    <div class="user-profile__tweet">
        <div class="tweet-item__user">
            @{{userName}}
        </div>
        <div class="tweet-item__content">
            {{tweet.content}}
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'TweetItem',
    props: {
        userName: {
            type: String,
            required: true
        },
        tweet: {
            type: Object,
            required: true
        }
    },
    methods:{
        favouriteTweet(id){
            this.$emit('favourite',id)
        }
    }
}
</script>

<style scoped>
.tweet-item {
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
    margin-bottom: 10px;
}

.tweet-item:hover {
    transform: scale(1.1, 1.1)
}

.tweet-item__user {
    font-weight: bold
}

.tweet-item__content {
    margin-top: 5px;
}
</style>
