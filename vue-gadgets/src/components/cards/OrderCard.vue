<script setup>
defineProps({
    order: Object,
});
</script>
<template>
    <div class="overflow-hidden rounded-xl sm:rounded-2xl border border-slate-200 bg-white shadow-sm">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 border-b border-slate-100 bg-slate-50/70 px-4 sm:px-6 py-3 sm:py-4">
            <div class="flex flex-wrap items-center gap-2 sm:gap-4">
                <span class="text-base sm:text-lg font-bold text-slate-900">Заказ №{{ order.id }}</span>
                <span class="rounded-full bg-red-100 px-2 py-0.5 text-xs font-semibold text-red-700">
          {{ order.orderData.status }}
        </span>
            </div>
            <div class="text-xs sm:text-sm text-slate-500">от {{ order.orderData.createdAt }}</div>
        </div>
        <div class="border-b border-slate-100 px-4 sm:px-6 py-2 sm:py-3 text-xs sm:text-sm text-slate-600">
            <span class="font-medium text-slate-800">{{ order.orderData.delivery?.methodLabel }}:</span>
            {{ order.orderData.delivery?.fullAddress }}
        </div>
        <div class="divide-y divide-slate-100 px-4 sm:px-6">
            <div v-for="item in order.orderData.items" :key="item.id" class="flex items-center justify-between gap-3 py-3 sm:py-3.5">
                <div class="flex items-center gap-2 sm:gap-3.5 min-w-0">
                    <img :src="item.imageUrl" :alt="item.title" class="h-10 w-10 sm:h-12 sm:w-12 rounded-lg bg-slate-50 object-contain p-1 shrink-0" />
                    <div class="min-w-0">
                        <p class="font-medium text-sm sm:text-base text-slate-800 truncate">{{ item.title }}</p>
                        <p class="text-xs text-slate-500">{{ item.quantity }} шт. x {{ item.price.toLocaleString("ru-RU") }} ₽</p>
                    </div>
                </div>
                <div class="font-semibold text-sm sm:text-base text-slate-900 shrink-0">
                    {{ (item.price * item.quantity).toLocaleString("ru-RU") }} ₽
                </div>
            </div>
        </div>
        <div class="flex items-center justify-between border-t border-slate-100 bg-slate-50/50 px-4 sm:px-6 py-3 sm:py-4">
            <span class="text-sm font-medium text-slate-600">Итого</span>
            <span class="text-base sm:text-lg font-bold text-red-600">{{ order.orderData.totalPrice?.toLocaleString("ru-RU") }} ₽</span>
        </div>
    </div>
</template>
