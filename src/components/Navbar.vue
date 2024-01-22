<template>
    <nav>
        <a href="https://copybase.com.br" target="_blank"><img src="../assets/copybase-logo.svg" alt="Logo da empresa Copybase"></a>
        <a id="about-me" target="_blank" href="https://programadorinteligente.com.br">Sobre o criador</a>
    </nav>
</template>

<style scoped>
nav {
    width: 100%;
    background-color: #41167F;
    padding: 20px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#about-me {
    color: #ffffff;
    text-decoration: none;
    transition: 0.3s;
}

#about-me {
    background-color: #0D9D68;
    padding: 7px;
    border-radius: 7px;
}

#about-me:hover {
    opacity: 0.75;
}

@media screen and (max-width: 500px) {
    nav {
        flex-direction: column;
        gap: 15px;
    }
}

@media screen and (max-width: 250px) {
    nav {
        padding: 20px 10px;
    }

    #about-me {
        max-width: 85vw;
        text-align: center;
        font-size: 0.7em;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis; 
    }
}

@media screen and (max-width: 200px) {
    img {
        max-width: 90vw;
    }
}

</style>