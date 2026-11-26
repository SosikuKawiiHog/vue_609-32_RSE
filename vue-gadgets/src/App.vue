<script setup>
import { onMounted } from "vue";
import { useAuthStore } from "@/stores/auth";
import { useCartStore } from "@/stores/cart";
import { useFavoritesStore } from "@/stores/favorites";
import LoginModal from "./components/modals/LoginModal.vue";
import RegisterModal from "./components/modals/RegisterModal.vue";

const authStore = useAuthStore();
const cartStore = useCartStore();
const favoritesStore = useFavoritesStore();

onMounted(() => {
    authStore.checkAuth();
});
</script>

<template>
    <div class="flex flex-col justify-between min-h-dvh bg-white">
        <div class="w-full max-w-[1440px] mx-auto px-4">
            <nav class="py-3 border-b border-b-slate-200">
                <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4">
                    <div class="flex items-center gap-3">
                        <img src="/logo.svg" alt="Логотип" class="h-8 w-auto" />
                        <p class="text-xs sm:text-sm text-slate-600">
                            Лучшие цены <br class="hidden sm:block" />
                            в интернет-магазинах
                        </p>
                    </div>
                    <ul class="flex flex-wrap items-center gap-4 sm:gap-6 lg:gap-10">
                        <li>
                            <RouterLink :to="{ name: 'catalog' }" class="flex gap-2 items-center text-sm sm:text-base">
                <span class="p-2 sm:p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/catalog-icon.svg" alt="" class="w-5 h-5" />
                </span>
                                Каталог
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink :to="{ name: 'cart' }" class="flex gap-2 items-center text-sm sm:text-base">
                <span class="p-2 sm:p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/cart-icon.svg" alt="" class="w-5 h-5" />
                </span>
                                Корзина ({{ cartStore.totalItems }})
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink :to="{ name: 'favorites' }" class="flex gap-2 items-center text-sm sm:text-base">
                <span class="p-2 sm:p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/like-outline.svg" alt="" class="w-5 h-5" />
                </span>
                                Избранное ({{ favoritesStore.items.length }})
                            </RouterLink>
                        </li>
                        <li v-if="authStore.isAuthenticated">
                            <RouterLink :to="{ name: 'orders' }" class="flex gap-2 items-center text-sm sm:text-base">
                <span class="p-2 sm:p-3.5 rounded-xl bg-slate-100 hover:bg-slate-200 transition">
                  <img src="/orders-icon.svg" alt="" class="w-5 h-5" />
                </span> Заказы
                            </RouterLink>
                        </li>
                        <li class="flex items-center gap-2 sm:gap-3">
                            <template v-if="authStore.isAuthenticated">
                                <span class="text-xs sm:text-sm font-medium text-slate-700">{{ authStore.user?.fullName }}</span>
                                <button
                                    @click="authStore.logout"
                                    class="rounded-lg border border-slate-200 px-2 sm:px-3 py-1.5 text-xs sm:text-sm font-medium text-slate-600 transition hover:bg-slate-100 hover:text-slate-900"
                                >Выйти</button>
                            </template>
                            <template v-else>
                                <button
                                    @click="authStore.activeModal = 'login'"
                                    class="rounded-lg px-2 sm:px-3.5 py-2 text-xs sm:text-sm font-medium text-slate-700 transition cursor-pointer hover:bg-slate-100"
                                >Войти</button>
                                <button
                                    @click="authStore.activeModal = 'register'"
                                    class="rounded-lg bg-red-500 px-3 sm:px-4 py-2 text-xs sm:text-sm font-medium text-white shadow-sm transition cursor-pointer hover:bg-red-400"
                                >Регистрация</button>
                            </template>
                        </li>
                    </ul>
                </div>
            </nav>

            <RouterView />

            <LoginModal
                :isOpen="authStore.activeModal === 'login'"
                @close="authStore.activeModal = null"
                @switch-to-register="authStore.activeModal = 'register'"
            />
            <RegisterModal
                :isOpen="authStore.activeModal === 'register'"
                @close="authStore.activeModal = null"
                @switch-to-login="authStore.activeModal = 'login'"
            />
        </div>

        <footer class="p-4 sm:p-6 bg-slate-100">
            <div class="text-center text-xs sm:text-sm text-slate-500">
                Copyright © 2023 Behoof, Inc. Все права защищены
            </div>
        </footer>
    </div>
</template>
