<script setup>
import IconShopBag from "@/components/icons/IconShopBag.vue"
import IconChevronDown from "@/components/icons/IconChevronDown.vue"
import IconArrowRight from "@/components/icons/IconArrowRight.vue"
import { ref, toRefs, computed } from "vue"

const props = defineProps({
    cartItems: {
        required: true
    },
    shippingCost: {
        type: Number,
        default: 0
    }
})
const { cartItems, shippingCost } = toRefs(props)

const totalPrice = computed(() => {
    return cartItems.value.reduce((accumulator, currentCartItem) => {
        return accumulator + parseInt(currentCartItem.price)
    }, 0)
})

const grandTotalPrice = computed(() => {
    return parseInt(totalPrice.value) + parseInt(shippingCost.value)
})
</script>

<template>
    <div class="lg:basis-2/5 lg:border-l lg:border-l-neutral-300 lg:bg-neutral-200">
        <!-- order summary accordion -->
        <div class="border-b border-b-neutral-300 lg:border-b-0 lg:hidden">
            <div id="order-summary-accordion" class="p-4 bg-white flex items-center gap-x-2 md:w-8/12 mx-auto">
                <div class="grow-0">
                    <IconShopBag/>
                </div>
                <div class="flex-1">
                    <span>
                        Show order summary
                    </span>
                </div>
                <div class="grow-0">
                    <span class="text-lg font-semibold">{{ $filters.formatRupiah(totalPrice) }}</span>
                </div>
            </div>
        </div>
        <!-- cart -->
        <div class="bg-neutral-200 border-b border-b-neutral-300 lg:border-b-0">
            <div id="cart" class="p-4 flex flex-col gap-y-6 md:w-8/12 md:mx-auto lg:w-10/12 lg:pt-10">
                <div id="cart-items" class="pb-6 border-b border-b-neutral-300 flex flex-col gap-y-6">
                    <div v-for="cartItem in cartItems" :key="cartItem.id" class="flex gap-x-4 items-center">
                        <div class="grow-0 relative">
                            <span class="block h-6 w-6 text-center font-semibold text-white bg-neutral-500 rounded-full absolute -top-2.5 -right-2.5">{{ cartItem.quantity }}</span>
                            <div class="w-20 rounded-md overflow-hidden">
                                <img :src="cartItem.featured_image_url" :alt="cartItem.product_name" />
                            </div>
                        </div>
                        <div class="flex-1">
                            <h3 class="capitalize font-semibold">{{ cartItem.product_name }}</h3>
                            <p>{{ `${cartItem.weight}g ${cartItem.grind_size}` }}</p>
                        </div>
                        <div class="grow-0">
                            <span class="font-semibold">{{ $filters.formatRupiah(cartItem.price) }}</span>
                        </div>
                    </div>
                </div>
                <!-- <div id="discount-apply" class="pb-6 border-b border-b-neutral-300">
                    <form action="/src/shipping.html" method="GET" class="flex gap-x-2">
                        <input type="text" placeholder="Discount code" class="rounded-md border border-neutral-300 focus:outline-none flex-1 px-4">
                        <button type="submit" class="bg-neutral-400 text-white rounded-md py-2 px-4" title="Apply code">
                            <IconArrowRight />
                        </button>
                    </form>
                </div> -->
                <div class="pb-6 border-b border-b-neutral-300">
                    <div id="subtotal-price" class="flex justify-between items-center">
                        <span class="capitalize">subtotal</span>
                        <span class="font-semibold">{{ $filters.formatRupiah(totalPrice) }}</span>
                    </div>
                    <div id="shipping-cost" class="flex justify-between items-center mt-4">
                        <span class="capitalize">shipping</span>
                        <span class="font-semibold">{{ $filters.formatRupiah(parseInt(shippingCost)) }}</span>
                    </div>
                </div>
                <div id="total-price" class="flex justify-between items-center pb-6">
                    <span class="capitalize text-lg">total</span>
                    <span class="text-lg font-semibold">{{ $filters.formatRupiah(grandTotalPrice) }}</span>
                </div>
            </div>
        </div>
    </div>
</template>
