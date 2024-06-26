vue <template>
    <div class="container">
        <h3>Intentos: {{ intentos }}</h3>
        <h3>Puntaje: {{ puntaje }}</h3>
    </div>
</template>

<script>
export default {
    props: {
        intentos: {
            type: Number,
            required: true,
            default: 0,
        },
        puntaje: {
            type: Number,
            required: true,
            default: 0,
        },
    },

}
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 20vh;
    width: 100%;
    background-color: #0df0fc;
    border-radius: solid 3px;

}


</style>