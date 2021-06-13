<template>
    <div>
        <div class="level">
            <div class="level-left">
                <h1 class="title is-4">Edit User: {{ user.name }}</h1>
            </div>
            <div class="level-right buttons">
                <NuxtLink
                    :to="{ name: 'users-id', params: { id: user.id } }"
                    class="button is-light"
                >
                    Detail
                </NuxtLink>
                <NuxtLink
                    :to="{ name: 'users' }"
                    class="button is-light"
                >
                    Back
                </NuxtLink>
            </div>
        </div>

        <hr>

        <form @submit.prevent="submit" @keydown="form.onKeydown($event)">
            <div class="field">
                <label for="name" class="label">Full Name</label>
                <div class="control">
                    <input type="text" v-model="form.name" id="name" class="input">
                </div>
                <p v-if="form.errors.has('name')" class="help is-danger">
                    {{ form.errors.get('name') }}
                </p>
            </div>
            <div class="field">
                <label for="email" class="label">Email Address</label>
                <div class="control">
                    <input type="email" v-model="form.email" id="email" class="input">
                </div>
                <p v-if="form.errors.has('email')" class="help is-danger">
                    {{ form.errors.get('email') }}
                </p>
            </div>
            <div class="field">
                <label class="checkbox">
                    <input type="checkbox" v-model="form.is_password"> Change user password?
                </label>
            </div>
            <div v-if="form.is_password" class="field">
                <label for="password" class="label">Password</label>
                <div class="control">
                    <input type="password" v-model="form.password" id="password" class="input">
                </div>
                <p v-if="form.errors.has('password')" class="help is-danger">
                    {{ form.errors.get('password') }}
                </p>
            </div>
            <div class="field">
                <button type="submit" class="button is-primary">Save Change</button>
            </div>
        </form>
    </div>
</template>

<script>
import Form from 'vform'

export default {
    head() {
        return {
            title: `Edit User: ${this.user.name}`
        }
    },

    data() {
        return {
            form: new Form({
                name: '',
                email: '',
                is_password: false
            })
        }
    },
    
    methods: {
        async submit() {
            try {

                const { data } = await this.form.put(`/users/${this.user.id}`)

                if (this.form.successful) {
                    this.$router.push({
                        name: 'users-id',
                        params: {
                            id: data.id
                        }
                    })
                }

            } catch (e) {}
        }
    },

    async asyncData({ $axios, params}) {
        const { data } = await $axios.get(`/users/${params.id}`)

        return { user: data}
    },

    mounted() {
        this.form.name = this.user.name
        this.form.email = this.user.email
    }
}
</script>