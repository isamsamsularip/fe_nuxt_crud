<template>
    <div>
        <nav class="navbar navbar-expand-lg bg-dark" data-bs-theme="dark">
            <div class="container">
                <NuxtLink class="navbar-brand" to="/">HOME</NuxtLink>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <NuxtLink class="nav-link active" aria-current="page" to="/posts">NOTES</NuxtLink>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>

        <!--- render page -->
        <slot />

    </div>
</template>

<style>
body { background-color: lightgray; font-family: 'Quicksand', sans-serif }
</style>
