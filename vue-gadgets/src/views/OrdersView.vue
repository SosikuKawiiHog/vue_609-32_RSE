<script setup>
import { onMounted } from "vue";
import { useOrdersStore } from "@/stores/orders";
import OrderCardSkeletonLoader from "@/components/skeletons/OrderCardSkeletonLoader.vue";
import OrderCard from "@/components/cards/OrderCard.vue";

const ordersStore = useOrdersStore();

onMounted(() => {
    ordersStore.fetchOrders();
});
</script>

<template>
    <main class="pt-6 sm:pt-10">
        <h1 class="text-3xl sm:text-[40px] font-bold mb-5">Заказы</h1>

        <div v-if="ordersStore.isLoading" class="space-y-4">
            <template v-for="n in 3" :key="n">
                <order-card-skeleton-loader />
            </template>
        </div>
        <div v-else-if="ordersStore.orders.length === 0" class="flex flex-col gap-5">
            <p>У вас пока нет оформленных заказов</p>
            <RouterLink :to="{ name: 'catalog' }" class="underline">Перейти в каталог</RouterLink>
        </div>

        <div v-else class="space-y-4 sm:space-y-6">
            <order-card
                v-for="order in ordersStore.orders"
                :key="order.id"
                :order="order"
            />
        </div>
    </main>
</template>
