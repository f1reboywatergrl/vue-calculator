<template>
<div>
    <nav class="navbar">
        <a href="https://www.linkedin.com/in/vincentius-samuel/" target="_blank"><font-awesome-icon :icon="['fab', 'linkedin-in']" size="lg" /></a>
        <a href="https://github.com/f1reboywatergrl" target="_blank"><font-awesome-icon :icon="['fab', 'github']" size="lg" /></a>
        <a href="https://github.com/f1reboywatergrl/vue-calculator" target="_blank"><font-awesome-icon :icon="['fas', 'code']" size="lg" /></a> 
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
.navbar{
    width: 100%;
    background-color: #23232e;
    color: #b6b6b6;
    display:flex;
    justify-content:space-between;
    overflow:hidden;
}

.navbar a{
    float: left;
    color: #f2f2f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: 17px;
    transition-duration: 0.3s;
}

.navbar a:hover{
    background-color: #ddd;
    color: black;
}

</style>
