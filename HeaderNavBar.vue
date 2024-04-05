<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
                <div class="container-fluid">
                    <a class="navbar-brand" href="#play2learn">Play2Learn</a>
                    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbar-content">
                        <span class="navbar-toggler-icon"></span>
                    </button>
                    <div class="collapse navbar-collapse" id="navbar-content">
                        <ul class="navbar-nav">
                            <li class="nav-item">
                                <a class="nav-link" href="#home">Home</a>
                            </li>
                            <li class="nav-item dropdown">
                                <a class="nav-link dropdown-toggle" href="#" role="button" id="navbar-dropdown" data-bs-toggle="dropdown">Games</a>
                                <div class="dropdown-menu">
                                    <a class="dropdown-item" href="#anagramhunt">Anagram Hunt</a>
                                    <a class="dropdown-item" href="#mathfactspractice">Math Facts Practice</a>
                                </div>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" href="#about">About</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" href="#login">Login</a>
                            </li>
                        </ul>
                    </div>
                </div>
              </nav>
</template>

<script>
export default {
    name: 'HeaderNavBar',
}
</script>

<style scoped></style>