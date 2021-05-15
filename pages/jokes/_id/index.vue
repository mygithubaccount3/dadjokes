<template>
    <div>
        <nuxt-link to="/jokes">Back To Jokes</nuxt-link>
        <h2>{{ joke }}</h2>
        <hr />
        <small>Joke ID: {{$route.params.id}}</small>
    </div>
</template>

<script>
export default {
    head() {
        return {
            title: this.joke,
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Best place for corny dad jokes'
                }
            ]
        }
    },

    data() {
        return {
            joke: {}
        }
    },

    async created() {
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await this.$axios.$get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config)
            this.joke = res.joke
            console.log(res)
            
        } catch (err) {
            console.log(err)   
        }
    }

}
</script>

<style>

</style>