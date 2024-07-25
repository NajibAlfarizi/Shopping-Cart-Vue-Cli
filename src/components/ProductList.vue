<template>
    <transition-group name="fade" tag="div" @beforeEnter="before" @enter="enter" @leave="leave">
        <div class="row mb-3 align-items-center" v-for="(item, index) in showItem" :key="item.id" :data-index="index">
            <div class="col-1 m-auto">
                <button class="btn btn-info" @click="$emit('add-item', item)">+</button>
            </div>
            <div class="col-sm-4">
                <img :src="item.image" :alt="item.name" class="img-fluid d-block">
            </div>
            <div class="col">
                <h3 class="text-info">{{ item.name }}</h3>
                <p class="mb-0">{{ item.description }}</p>
                <div class="h5 float-right">
                    <price :value="Number(item.price)" :precision="2"></price>
                </div>
            </div>
        </div>
    </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
    name: "product-list",
    components: {
        Price
    },
    props: ["products", "maximum"],
    computed: {
        showItem: function() {
            let max = this.maximum;
            return this.products.filter(function(item) {
                return item.price <= max;
            });
        }
    },
    methods: {
        before: function (el) {
            el.classList.add('d-none');
        },
        enter: function (el) {
            const delay = el.dataset.index * 100;
            setTimeout(() => {
                el.classList.remove('d-none');
                el.classList.add('d-flex', 'animated', 'fadeInRight');
            }, delay);
        },
        leave: function (el) {
            const delay = el.dataset.index * 100;
            setTimeout(() => {
                el.classList.add('animated', 'fadeOutRight');
                setTimeout(() => {
                    el.classList.remove('d-flex');
                    el.classList.add('d-none');
                }, 1000); // Duration of fadeOutRight animation
            }, delay);
        }
    }
};
</script>

<style>
.fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
    opacity: 0;
}

.d-none {
    display: none !important;
}

.animated {
    animation-duration: 1s;
    animation-fill-mode: both;
}

.fadeInRight {
    animation-name: fadeInRight;
}

@keyframes fadeInRight {
    from {
        opacity: 0;
        transform: translate3d(100%, 0, 0);
    }

    to {
        opacity: 1;
        transform: none;
    }
}

.fadeOutRight {
    animation-name: fadeOutRight;
}

@keyframes fadeOutRight {
    from {
        opacity: 1;
        transform: none;
    }

    to {
        opacity: 0;
        transform: translate3d(100%, 0, 0);
    }
}

</style>
