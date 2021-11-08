<template>
    <div class="container">
        <p class="not-found" v-if="notFound">not found</p>
        <ul v-else>
            <li class="country" @click="$emit('select-item', country)" v-for="(country,i) in countries" :key="i">
                {{country.name}} {{ countries.count}}
                <hr class="divider">
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                isLoading : false

            }
        },

        computed: {
            notFound: function () {
                if (this.countries.length === 0) {
                    return true
                } else {
                    return false
                }
            }
        },

        watch: {
            items: function (value, oldValue) {
                if (value.length !== oldValue.length) {
                this.results = value;
                this.isLoading = false;
                }
            },
        },

        props : {
            countries : {
                type: Array,
            }
        },

    }
</script>

<style scoped>
.container  {
    background-color: #003d61;
    width: auto;
    height: 9rem;
    overflow-y: scroll;
    overflow-x: hidden;
    text-align: left;
}

ul > li {
    list-style: none;
}

.country {
    color: white;
    margin: 0px 0px 10px 0px;
    cursor: pointer;
}

.not-found {
    display:flex;
    width: inherit;
    height: 30px;
    justify-content:center;
    align-items:center;
    color: white;
}

.divider {
    border-width: 1px;
}
</style>