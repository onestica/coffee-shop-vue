<script setup>
import IconCross from '@/components/icons/IconCross.vue'
import IconSearch from '@/components/icons/IconSearch.vue'

import { useIndexStore } from '@/stores/index.js'
const { toggleSearchModal, togglePageLoading } = useIndexStore()

import { useProductStore } from '@/stores/product.js'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()
const { fetchProductList } = useProductStore()
let searchKeyword = ref('')

function searchProduct() {
	toggleSearchModal()
	togglePageLoading()
	fetchProductList(1,'-created_at',null,searchKeyword.value)
		.then(() => {
			router.push({ name: 'search-result' })
		})
}
</script>

<template>
    <div class="bg-white w-full lg:w-1/2 absolute top-1/2 -translate-y-1/2 md:left-1/2 md:-translate-x-1/2 z-20 rounded-md">
		<div class="flex py-4 px-6 bg-gray-200">
			<div class="flex-1 text-center font-bold">
				SEARCH
			</div>
			<button @click="toggleSearchModal">
				<IconCross />
			</button>
		</div>
		<div class="p-6">
			<form @submit.prevent="searchProduct" action="#" class="p-2 border border-gray-300 rounded-sm flex items-center gap-x-4">
				<div class="flex-1">
					<input type="text" v-model="searchKeyword" placeholder="Search..." class="focus:outline-0 w-full" autofocus>
				</div>
				<button type="submit">
					<IconSearch />
				</button>
			</form>
		</div>
	</div>
</template>
