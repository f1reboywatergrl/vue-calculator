<template>
<div>
    <nav class="navbar">
        <ul class="navbar-nav">
            <li class="nav-item">
                <a href="#" class="nav-link">
                    <svg src="../assets/github-brands.svg"></svg>
                    <span class="link-text">Cats</span>
                </a>
            </li>
        </ul>
    </nav>
</div>
</template>

<script>
export default {
    name: 'Nav'
}
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css');
:root{
    --text-primary: #b6b6b6;
    --text-secondary: #ececec;
    --bg-primary: #23232e;
    --bg-secondary: #141418;
}
main{
    margin-left: 5rem;
    padding:1rem;
}

.navbar{
    left: 5rem;
    height: 100vh;
    position: fixed;
    background-color: var(--bg-primary);
}
</style>
