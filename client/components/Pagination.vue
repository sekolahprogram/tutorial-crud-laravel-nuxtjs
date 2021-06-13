<template>
    <div class="my-5">
        <nav class="pagination is-rounded" role="navigation" aria-label="pagination">

            <NuxtLink
                v-if="links[0].url"
                :to="url_param(links[0].url)"
                class="pagination-previous"
                v-html="links[0].label"
                @click.native="onRefesh()"
            />

            <a
                v-else
                class="pagination-previous"
                disabled
                v-html="links[0].label"
            />

            <NuxtLink
                v-if="links[links.length - 1].url"
                :to="url_param(links[links.length - 1].url)"
                class="pagination-next"
                v-html="links[links.length - 1].label"
                @click.native="onRefesh()"
            />

            <a
                v-else
                class="pagination-next"
                disabled
                v-html="links[links.length - 1].label"
            />

            <ul class="pagination-list">
                <li
                    v-for="(item, index) in links.slice(1, -1)"
                    :key="index"
                >
                    <NuxtLink
                        :to="url_param(item.url)"
                        :class="[`pagination-link`, {
                            'is-current': item.active
                        }]"
                        @click.native="onRefesh()"
                    >
                        {{ item.label }}
                    </NuxtLink>
                </li>
            </ul>

        </nav>
    </div>
</template>

<script>
export default {
    props: ['links'],

    methods: {
        url_param(url) {
            let params = url.match(/\w+=\w+/g)[0]

            return `?${params}`
        },

        onRefesh() {
            console.log('a')
            this.$router.app.refresh()
        }
    }
}
</script>