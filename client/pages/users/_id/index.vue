<template>
    <div>
        <div class="level">
            <div class="level-left">
                <h1 class="title is-4">User: {{ user.name }}</h1>
            </div>
            <div class="level-right buttons">
                <NuxtLink
                    :to="{ name: 'users-id-edit', params: { id: user.id } }"
                    class="button is-light"
                >
                    Edit
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

        <div class="field">
            <label class="label">Full Name</label>
            <pre>{{ user.name }}</pre>
        </div>

        <div class="field">
            <label class="label">Email Address</label>
            <pre>{{ user.email }}</pre>
        </div>

        <div class="field">
            <label class="label">Verified</label>
            <pre>{{ user.email_verified_at ? new Date(user.email_verified_at).toLocaleDateString() : 'Not Verified' }}</pre>
        </div>

        <div class="field">
            <label class="label">Created</label>
            <pre>{{ new Date(user.created_at).toLocaleDateString() }}</pre>
        </div>

        <div class="field">
            <label class="label">Updated</label>
            <pre>{{ new Date(user.updated_at).toLocaleDateString() }}</pre>
        </div>
        
    </div>
</template>

<script>
export default {
    head() {
        return {
            title: `User: ${this.user.name}`
        }
    },

    async asyncData({ $axios, params}) {
        const { data } = await $axios.get(`/users/${params.id}`)

        return { user: data}
    }
}
</script>