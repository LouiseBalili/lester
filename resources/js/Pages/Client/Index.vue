<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import ClientCard from '@/Components/ClientCard.vue';
import { Head } from '@inertiajs/vue3';

defineProps({
    clients: Array
})
</script>

<template>
    <Head title="Clients" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-white leading-tight">Clients</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div>
                    <ClientCard v-for="client in clients" :key="client.id" :client="client" class="border border rounded hover:bg-gray-200"/>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
