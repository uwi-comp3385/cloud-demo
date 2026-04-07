<script setup lang="ts">
import { Head, Link, usePage } from '@inertiajs/vue3';
import { computed } from 'vue';
import { dashboard, login, register } from '@/routes';

withDefaults(
    defineProps<{
        canRegister: boolean;
    }>(),
    {
        canRegister: true,
    },
);

const page = usePage();
const dashboardUrl = computed(() =>
    page.props.currentTeam ? dashboard(page.props.currentTeam.slug).url : '/',
);
</script>

<template>
    <Head title="Welcome" />

    <div class="min-h-screen bg-background text-foreground flex flex-col">
        <!-- Nav -->
        <header class="border-b border-border px-6 py-4">
            <div class="mx-auto flex max-w-5xl items-center justify-between">
                <div class="flex items-center gap-2">
                    <svg class="h-7 w-7 text-primary" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                        <path d="M6.5 20Q4.22 20 2.61 18.43Q1 16.85 1 14.58Q1 12.63 2.17 11.1Q3.35 9.57 5.25 9.15Q5.88 6.85 7.75 5.43Q9.63 4 12 4Q14.93 4 16.96 6.04Q19 8.07 19 11Q20.73 11.2 21.86 12.5Q23 13.78 23 15.5Q23 17.38 21.69 18.69Q20.38 20 18.5 20Z" />
                    </svg>
                    <span class="text-lg font-semibold tracking-tight">COMP3385 Laravel Cloud Demo</span>
                </div>

                <nav class="flex items-center gap-3">
                    <template v-if="$page.props.auth.user">
                        <Link
                            :href="dashboardUrl"
                            class="rounded-md bg-primary px-4 py-1.5 text-sm font-medium text-primary-foreground hover:bg-primary/90 transition-colors"
                        >
                            Dashboard
                        </Link>
                    </template>
                    <template v-else>
                        <Link
                            :href="login()"
                            class="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors"
                        >
                            Log in
                        </Link>
                        <Link
                            v-if="canRegister"
                            :href="register()"
                            class="rounded-md bg-primary px-4 py-1.5 text-sm font-medium text-primary-foreground hover:bg-primary/90 transition-colors"
                        >
                            Get started
                        </Link>
                    </template>
                </nav>
            </div>
        </header>

        <!-- Hero -->
        <main class="flex flex-1 flex-col items-center justify-center px-6 py-20 text-center">
            <div class="mx-auto max-w-2xl">
                <h1 class="text-5xl font-bold tracking-tight text-foreground lg:text-6xl">
                    Build and deploy<br />
                    <span class="text-primary">at cloud speed</span>
                </h1>

                <p class="mt-6 text-lg text-muted-foreground">
                    A demo application showcasing Laravel Cloud — the fastest way to
                    deploy, scale, and manage your Laravel applications in production.
                </p>

                <div class="mt-10 flex flex-col items-center gap-3 sm:flex-row sm:justify-center">
                    <Link
                        v-if="!$page.props.auth.user && canRegister"
                        :href="register()"
                        class="rounded-md bg-primary px-6 py-2.5 text-sm font-semibold text-primary-foreground shadow-sm hover:bg-primary/90 transition-colors"
                    >
                        Create an account
                    </Link>
                    <Link
                        v-if="$page.props.auth.user"
                        :href="dashboardUrl"
                        class="rounded-md bg-primary px-6 py-2.5 text-sm font-semibold text-primary-foreground shadow-sm hover:bg-primary/90 transition-colors"
                    >
                        Go to Dashboard
                    </Link>
                    <Link
                        v-if="!$page.props.auth.user"
                        :href="login()"
                        class="rounded-md border border-border px-6 py-2.5 text-sm font-semibold text-foreground hover:bg-accent transition-colors"
                    >
                        Log in
                    </Link>
                </div>
            </div>
        </main>

        <!-- Features -->
        <section class="border-t border-border px-6 py-16">
            <div class="mx-auto max-w-5xl">
                <div class="grid gap-6 sm:grid-cols-3">
                    <div class="rounded-xl border border-border bg-card p-6">
                        <div class="mb-4 flex h-10 w-10 items-center justify-center rounded-lg bg-primary/10">
                            <svg class="h-5 w-5 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
                            </svg>
                        </div>
                        <h3 class="font-semibold text-foreground">Instant Deployments</h3>
                        <p class="mt-2 text-sm text-muted-foreground">
                            Push your code and go live in seconds. Zero-downtime deployments with automatic rollbacks.
                        </p>
                    </div>

                    <div class="rounded-xl border border-border bg-card p-6">
                        <div class="mb-4 flex h-10 w-10 items-center justify-center rounded-lg bg-primary/10">
                            <svg class="h-5 w-5 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0z" />
                            </svg>
                        </div>
                        <h3 class="font-semibold text-foreground">Team Collaboration</h3>
                        <p class="mt-2 text-sm text-muted-foreground">
                            Invite your team, manage roles, and collaborate seamlessly across projects.
                        </p>
                    </div>

                    <div class="rounded-xl border border-border bg-card p-6">
                        <div class="mb-4 flex h-10 w-10 items-center justify-center rounded-lg bg-primary/10">
                            <svg class="h-5 w-5 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                            </svg>
                        </div>
                        <h3 class="font-semibold text-foreground">Auto Scaling</h3>
                        <p class="mt-2 text-sm text-muted-foreground">
                            Handle any traffic spike automatically. Scale up or down based on real demand.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="border-t border-border px-6 py-6">
            <div class="mx-auto flex max-w-5xl items-center justify-between text-xs text-muted-foreground">
                <span>© 2026 COMP3385 Laravel Cloud Demo</span>
                <a
                    href="https://cloud.laravel.com"
                    target="_blank"
                    class="hover:text-foreground transition-colors"
                >
                    cloud.laravel.com →
                </a>
            </div>
        </footer>
    </div>
</template>
