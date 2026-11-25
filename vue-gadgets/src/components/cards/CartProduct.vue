<script setup>
import { useFavoritesStore } from "@/stores/favorites";
import { useCartStore } from "@/stores/cart";

const favoritesStore = useFavoritesStore();
const cartStore = useCartStore();
defineProps({
    product: Object,
});
</script>
<template>
    <div
        class="p-5 bg-slate-100 rounded-4xl flex items-start justify-between gap-10"
    >
        <div class="flex gap-4 flex-1">
            <div class="w-30 h-30 overflow-hidden">
                <img
                    :src="product.imageUrl"
                    alt=""
                    class="w-full h-full object-cover"
                />
            </div>
            <div class="pt-2">
                <h3 class="text-xl font-semibold mb-3">
                    {{ product.title }}
                </h3>
                <div class="flex gap-3 items-center">
                    <button
                        @click="favoritesStore.toggleFavorite(product)"
                        class="rounded-4xl shadow p-3 cursor-pointer hover:scale-110 transition"
                        :class="[
                          favoritesStore.isFavorite(product.id)
                            ? 'bg-red-500'
                            : 'bg-white',
                        ]"
                    >
                        <svg
                            width="20"
                            height="20"
                            viewBox="0 0 20 20"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.28332 17.9333C6.09999 16.8417 1.04166 12.9667 1.04166 7.00001C1.04166 4.15834 3.28332 1.95834 6.15832 1.95834C7.53332 1.95834 8.81666 2.50001 9.76666 3.44167C10.7167 2.50001 12 1.95834 13.375 1.95834C16.25 1.95834 18.4917 4.15834 18.4917 7.00001C18.4917 12.9667 13.4333 16.8417 10.25 17.9333C10.0417 18.0083 9.79166 18.0417 9.53332 18.0417H9.99999Z"
                                :fill="
                                  favoritesStore.isFavorite(product.id)
                                    ? '#fff'
                                    : '#263141'
                                "
                            />
                        </svg>
                    </button>
                    <button
                        @click="cartStore.removeFromCart(product.id)"
                        class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition"
                    >
                        <svg
                            width="20"
                            height="20"
                            viewBox="0 0 20 20"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M18 5.31667C15.225 5.04167 12.4333 4.9 9.65 4.9C8 4.9 6.35 4.98333 4.7 5.15L3 5.31667M7.58333 4.475L7.76667 3.38333C7.9 2.59167 8 2 9.40833 2H11.5917C13 2 13.1083 2.625 13.2333 3.39167L13.4167 4.475M16.2083 7.95L15.6667 16.3417C15.575 17.65 15.5 18.6667 13.175 18.6667H7.825C5.5 18.6667 5.425 17.65 5.33333 16.3417L4.79167 7.95M9.10833 14.0833H11.8833M8.41667 10.75H12.5833"
                                stroke="#263141"
                                stroke-width="1.25"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                            />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div class="pt-2">
            <b class="text-xl">{{ product.price.toLocaleString("ru-RU") }} ₽</b>
        </div>
        <div class="rounded-4xl bg-white p-1 flex items-center">
            <button
                class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                @click="cartStore.updateQuantity(product.id, -1)"
            >
                -
            </button>
            <span class="w-12 text-center">{{ product.quantity }}</span>
            <button
                class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                @click="cartStore.updateQuantity(product.id, 1)"
            >
                +
            </button>
        </div>
    </div>
</template>
