<script setup>
import { useFavoritesStore } from "@/stores/favorites";
import VProduct from "@/components/cards/VProduct.vue";

const favoritesStore = useFavoritesStore();
</script>
<template>
    <main class="pt-6 sm:pt-10">
        <h1 class="text-3xl sm:text-[40px] font-bold mb-5">Избранное</h1>
        <div v-if="favoritesStore.items.length === 0" class="flex flex-col gap-5">
            <p>В избранном пока ничего нет 💔</p>
            <RouterLink :to="{ name: 'catalog' }" class="underline">Перейти в каталог</RouterLink>
        </div>
        <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4 sm:gap-5">
            <v-product
                v-for="item in favoritesStore.items"
                :key="item.id"
                :product="item"
            />
        </div>
    </main>
</template>
