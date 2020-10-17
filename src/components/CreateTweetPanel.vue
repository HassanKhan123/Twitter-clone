<template>
<form class="create-tweet-panel" @submit.prevent="createNewTweet" :class="{ '--exceeded': newTweetCharacterCount > 180 }">
    <label for="newTweet"><strong>New Tweet</strong> ({{ newTweetCharacterCount }}/180)</label>
    <textarea id="newTweet" rows="4" v-model="this.newTweetContent" />

    <div class="create-tweet-panel__submit">
        <div class="create-tweet-type">
            <label for="newTweetType"><strong>Type: </strong></label>
            <select id="newTweetType" v-model="this.selectedTweetType">
                <option :value="option.value" v-for="(option, index) in this.tweetTypes" :key="index">
                    {{ option.name }}
                </option>
            </select>
        </div>

        <button>Tweet It!</button>
    </div>
</form>
</template>

<script>
export default {
    name: "CreateTweetPanel",
    data() {
        return {
            newTweetContent: "",
            selectedTweetType: "instant",
            tweetTypes: [{
                    value: "draft",
                    name: "Draft",
                },
                {
                    value: "instant",
                    name: "Instant Tweet",
                },
            ],
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
    computed: {
        newTweetCharacterCount() {
            return this.newTweetContent.length;
        },
    },
    methods: {
        createNewTweet() {
            if (this.newTweetContent && this.selectedTweetType !== "draft") {
                this.$emit("add-tweet", this.newTweetContent);

                this.newTweetContent = "";
            }
        },
    },
};
</script>

<style lang="scss" scoped>
.create-tweet-panel {
    margin-top: 20px;
    padding: 20px 0;
    display: flex;
    flex-direction: column;

    textarea {
        border: 1px solid #dfe3e8;
        border-radius: 5px;
    }

    .create-tweet-panel__submit {
        display: flex;
        justify-content: space-between;

        .create-tweet-type {
            padding: 10px 0;
        }

        button {
            padding: 5px 20px;
            margin: auto 0;
            border-radius: 5px;
            border: none;
            background-color: deeppink;
            color: white;
            font-weight: bold;
        }
    }

    &.--exceeded {
        color: red;
        border-color: red;

        .create-tweet-panel__submit {
            button {
                background-color: red;
                color: white;
            }
        }
    }
}
</style>
