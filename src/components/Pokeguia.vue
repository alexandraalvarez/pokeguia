<template>
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <img class="mx-auto d-block" src="../assets/img/logo.png" alt="pokemon escrito con letras grandes y de color amarillo con borde azul">
            </div>
            <div class="col-lg-12">
                <h1 class="text-center mt-5">Pokeguía con Vue</h1>
                <div class="flex-row">
                    <form class="d-flex justify-content-center " action="">
                        <label class="text-center mt-4" for="">Ingresa el nombre del pokemon</label>
                        <div class="input-group mb-3 col-md-4">
                            <input type="text" v-model="character.name" @keyup.enter="fetchCharacter" class="form-control" placeholder="Ingrese nueva tarea">
                            <div class="input-group-append">
                                <button class="btn btn-outline-secondary" @click.prevent="fetchCharacter"  type="button">Buscar</button>
                            </div>
                        </div>
                    </form>
                </div>
                <div class="flex-row">
                    <div class="d-flex justify-content-center"> 
                        <img :src="image.front_default" alt="no hay foto" class="mx-auto d-block">
                        <h3 class="text-center">Movimientos</h3>
                        <ul class="lista">
                            <li v-for="(movement,index) in movements" :key="index">{{movement.move.name}}</li>
                        </ul>
                    </div>
                    <div class="d-flex justify-content-center">
                        <h3 class="text-center">Habilidades</h3>
                        <ul class="lista">
                            <li v-for="(ability,index) in abilities" :key="index">{{ability.skill.name}}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'pokedata',
    //props: {},
    data: function () {
        return {
            character: {
                name: "Pikachu",
                movements: [],
                abilities: [],
                moves: "",
                skills: "",
                sprites: {
                front_default: "",
                },
            },
        }
    },
    computed: {
        image() {
            return this.character.sprites;
        },
        movements() {
            return this.character.moves;
        },
        abilities() {
            return this.character.skills;
        }
    },
    methods: {
        fetchCharacter() {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.character.name}`) //peticion a API
                .then(response => response.json())  //transforma la data a un json, ésto equivale a un return
                .then(json => {
                    console.log(json);
                    this.character = json;
                })
                .catch(error => {
                    alert("El Pokemon que buscas no existe, revisa que esté bien escrito o prueba con otro");
                    console.log(error);
                })
        },
    },
    // components: {},
    created() {
        this.fetchCharacter();
    }
}
</script>

<style scoped>
</style>