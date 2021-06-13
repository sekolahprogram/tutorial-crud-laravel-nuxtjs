<template>
    <div>
        <div class="level">
            <div class="level-left">
                <h1 class="title is-4">All Users</h1>
            </div>
            <div class="level-right">
                <NuxtLink
                    :to="{ name: 'users-create' }"
                    class="button is-light"
                >
                    Create
                </NuxtLink>
            </div>
        </div>

        <hr>

        <div class="table-container">
            <table class="table is-fullwidth is-striped is-hoverable">
                <thead>
                    <tr>
                        <th>#</th>
                        <th>Full Name</th>
                        <th>Email Address</th>
                        <th>Verified</th>
                        <th>Created</th>
                        <th>Updated</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr
                        v-for="(user, index) in data.data"
                        :key="index"
                    >
                        <td>{{ user.id }}</td>
                        <td>{{ user.name }}</td>
                        <td>{{ user.email }}</td>
                        <td>{{ user.email_verified_at ? new Date(user.email_verified_at).toLocaleDateString() : 'Not Verified' }}</td>
                        <td>{{ new Date(user.created_at).toLocaleDateString() }}</td>
                        <td>{{ new Date(user.updated_at).toLocaleDateString() }}</td>
                        <td class="buttons">
                            <NuxtLink
                                :to="{
                                    name: 'users-id',
                                    params: { id: user.id}
                                }"
                                class="button is-small is-info"
                            >
                                Detail
                            </NuxtLink>
                            <NuxtLink
                                :to="{
                                    name: 'users-id-edit',
                                    params: { id: user.id}
                                }"
                                class="button is-small is-primary"
                            >
                                Edit
                            </NuxtLink>
                            <a
                                @click="deleteUser(user.id)"
                                class="button is-small is-danger"
                            >
                                Delete
                            </a>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <Pagination
            :links="data.links"
        />
    </div>
</template>

<script>
export default {
    head: {
        title: 'All Users'
    },

    async asyncData({ $axios, query }) {

        const { data } = await $axios.get(`/users?page=${query.page || 1}`)

        return { data }
    },

    methods: {
        deleteUser(id) {
            if (!confirm('Are you sure to delete this user?')) {
                return;
            }

            this.$axios.delete(`/users/${id}`)
            .finally(() => {
                this.$router.app.refresh()
            })
        }
    }
}
</script>