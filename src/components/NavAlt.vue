<template>
    <div>
        <nav>
            <router-link to="/"><div class="big-text">TMDb</div></router-link>    
            <img class="hamburger-menu" src="../img/hamburger.svg">
        </nav>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 20px 60px;
}

.big-text {
    font-size: 80px;
    font-weight: 800;
    color: var(--accentColor);
}

.search-bar {
    width: 300px;
    background: var(--otherColor);
    height: 55px;
    display: flex;
    padding-left: 20px;
    align-items: center;
    border-radius: 20px;
    margin-right: 100px;
    color: white;
    font-size: 18px;
    font-weight: 700;
    border: none;
}

.form-hamburger-container {
    display: flex;
}

input:focus,
select:focus,
textarea:focus,
button:focus {
    outline: none;
}

::placeholder {
    color: white;
    opacity: 0.2;
}


.logo {
    position: relative;
    top: 5px;
}

.hamburger-menu {
    cursor: pointer;
}
</style>