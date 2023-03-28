<template>
    <div class="computer">
        <div>
            Estado: <span>Online</span> <span>Offline</span>
        </div>
        <div>
            Nombre: <span>Nombre Máquina</span>
        </div>
        <div>
            IP: <span>192.168.250.255</span>
        </div>
        <div>
            Acciones:
            <ul>
                <li>ventana 1<button @click="cancelAction()">Cancelar</button></li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "ComputerComponent",
    data() {
        return {
        }
    },
    methods: {
        cancelAction(action) {
            console.log(action)
        }
    }
}
</script>

<style lang="scss" scoped>
.computer {
    cursor: default;
    box-shadow: 2px 2px 10px 2px rgba(0, 0, 0, 0.479);
    border-radius: .1rem;
    padding: 1rem;
    margin: .5em;
    width: fit-content;

    & button {
        cursor: pointer;
    }
}
</style>