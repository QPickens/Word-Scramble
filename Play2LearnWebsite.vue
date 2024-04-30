<template>
    <div>
        <div v-html="play2LearnWebsiteHtml"></div>
    </div>
</template>

<script>
export default {
    name: 'Play2LearnWebsite',
    data() {
        return {
            play2LearnWebsiteHtml: ''
        };
    },
    mounted() {
        fetch('./components/Play2Learn Website-bootstrap.html')
        .then(response => response.text())
        .then(html => {
            this.play2LearnWebsiteHtml = html;
        })
        .catch(error => {
            console.error('Error fetching Play2Learn Website-bootstrap.html:', error);
        });
    }
};
</script>

<style scoped>
#play2learn-website {
    border: none;
}
</style>
