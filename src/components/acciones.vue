<template>
    <div class="acciones">
        <div class="action-box">
            <div>
                <label for="">Abrir Página</label><br>
                <input type="text" placeholder="Ingrese la URL completa">
                <button @click="sendCommand()">Enviar</button>
            </div>
            <div>
                <div v-for="lab in laboratorios" :key="lab.id">
                    <label :for="lab.name">Laboratorio {{ lab.name }}</label>
                    <input :id="lab.name" v-model="lab.value" type="checkbox">
                </div>
            </div>
            <div class="footer">
                <button @click="closeModal()">Cancelar</button>
            </div>
        </div>
        <div>
        </div>
    </div>
</template>

<script>
import { ipcRenderer } from "electron"
import Swal from "sweetalert2"
import _ from "lodash"
export default {
    name: "AccionesComponent",
    data() {
        return {
            laboratorios: [
                { name: "I", value: false },
                { name: "II", value: false },
                { name: "III", value: false },
                { name: "IV", value: false },
                { name: "V", value: false },
                { name: "VI", value: false },
                { name: "VII", value: false },
            ],

        }
    },
    methods: {
        sendCommand() {
            Swal.fire({
                title: "Confirmar Acción",
                icon: "question",
                showCancelButton: true,

            }).then(res => {
                if (res.value) {
                    let data = _.cloneDeep(this.laboratorios.filter(lab => lab.value));
                    ipcRenderer.send("sendCommand", data)
                    this.closeModal()
                }
            })
        },
        closeModal() {
            this.$emit("closeModal")
        }
    }
}
</script>

<style lang="scss">
.acciones {
    position: absolute;
    top: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.459);
    width: 100vw;
    height: 100vh;
}


.action-box {
    background-color: white;
    width: fit-content;
    margin: auto;
    padding: 1rem;
    margin-top: 2rem;

    & input {
        text-transform: lowercase;
    }

}

.footer {
    margin: 10px;

}
</style>