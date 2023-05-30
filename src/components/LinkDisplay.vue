<template>
    <div class="LinkDisplay">
        <h3>Shortened Link:</h3>
        <p>{{ shortLink }}</p>
    </div>

</template>
<script>
export default{
    props: {
            shortLink: String 
    },
    data(){
        return{}
    }
}

</script>