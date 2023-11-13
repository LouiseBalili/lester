<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link } from '@inertiajs/vue3';
import { ref, computed } from 'vue';

const props = defineProps({
    client: Object,
    sales: Array,
})

const totalAmount = computed(() => {
    let sum = 0;
    props.sales.map(obj => sum += obj.amount);

    return sum;
})

</script>

<template>
    <Head :title="client.first_name + ' ' + client.last_name" />

    <AuthenticatedLayout>
        <template #header>
            <div class="flex items-center">
            <Link href="/products" class="inline-flex items-center px-4 py-2 text-sm mr-3 dark:text-white">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="3" stroke="currentColor" class="w-4 h-4">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18" />
                  </svg>
                </Link>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-white leading-tight">View Client</h2>
            </div>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-[#1f1f1f] overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6">
                        <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white flex items-center">
                            {{ client.first_name }} {{ client.last_name }}
                        </h5>

                        <div class="flex items-start">
                            <div class="max-w-md">
                                <h4 class="mb-2 text-md font-semibold tracking-tight text-gray-700 dark:text-gray-50">Client Details</h4>
                                <div class="mb-2">
                                    <p class="font-semibold text-gray-700 dark:text-gray-50 text-sm">Address</p>
                                    <p class="text-sm text-gray-700 dark:text-gray-50 font-light">{{ client.address }}</p>
                                </div>
                                <div class="mb-2">
                                    <p class="font-semibold text-gray-700 dark:text-gray-50 text-sm">Phone</p>
                                    <p class="text-sm text-gray-700 dark:text-gray-50 font-light">{{ client.phone }}</p>
                                </div>
                                <div>
                                    <p class="font-semibold text-gray-700 dark:text-gray-50 text-sm">Credit Limit</p>
                                    <p class="text-sm text-gray-700 dark:text-gray-50 font-light">{{ client.credit_limit }}</p>
                                </div>
                            </div>

                            <div class="flex-1 ml-4">
                                <h4 class="text-md font-semibold tracking-tight text-gray-700 dark:text-gray-50">Sales Transactions</h4>
                                <table class="table-fixed w-full mt-3">
                                    <thead class="bg-green-200 dark:bg-blue-500 dark:text-white">
                                        <th class="text-center px-4 py-2">Date</th>
                                        <th class="text-center px-4 py-2">Cash/Credit</th>
                                        <th class="text-center px-4 py-2">Total</th>
                                    </thead>
                                    <tbody>
                                        <tr class="border-b border-gray-200" v-for="sale in sales" :key="sale.id">
                                            <td class="text-center py-2 dark:text-white">
                                                {{ sale.date }}
                                            </td>
                                            <td class="text-center py-2 dark:text-white">
                                                {{ sale.is_credit ? 'Credit' : 'Cash' }}
                                            </td>
                                            <td class="text-center py-2 dark:text-white">
                                                {{ sale.amount }}
                                            </td>
                                        </tr>
                                        <tr>
                                            <td colspan="2" class="text-end py-2 dark:text-white">
                                                Sum:
                                            </td>
                                            <td class="text-center py-2 font-semibold text-xl dark:text-white">
                                                {{ totalAmount }}
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
