<template>
    <div class="container">
        <div class="row">
            <div class="col-lg-12 py-3 miniHeader">
                <img class="mx-auto d-block" src="../assets/img/logo.png" alt="pokemon escrito con letras grandes y de color amarillo con borde azul">
            </div>
            <div class="col-lg-12 divColCont divBgWhite">
                <h3 class="h3Title text-center my-4 divBgWhite">Pokeguía con Vue</h3>
                <div class="flex-row divForm divBgWhite">
                    <form class="d-flex justify-content-center divBgWhite" action="">
                        <label class="mt-1 divBgWhite" for="">Ingresa el nombre del pokemon</label>
                        <div class="input-group mb-3 col-md-4 divBgWhite">
                            <input type="text" v-model="character.name" @keyup.enter="fetchCharacter" class="form-control divBgWhite" placeholder="Ingrese nombre">
                            <div class="input-group-append divBgWhite">
                                <button class="btn btn-search" @click.prevent="fetchCharacter"  type="button">Buscar</button>
                            </div>
                        </div>
                    </form>
                </div>
                <div class="flex-row divPoke divBgWhite">
                    <div class="d-flex justify-content-center divBgWhite"> 
                        <img class="mx-auto d-block divBgWhite" :src="image.front_default" alt="" >
                    </div>
                    <div class="d-flex justify-content-center divBgWhite"> 
                        <h3 class="divBgWhite">{{character.name}} </h3>
                    </div>
                    <div class="d-flex justify-content-center divBgWhite"> 
                        <h3 class="text-center divBgWhite">Movimientos</h3>
                    </div>
                    <div class="d-flex justify-content-center divMoves divBgWhite"> 
                        <ul class="lista divBgWhite">
                            <li class="divBgWhite" v-for="(movement,index) in movements" :key="index">{{movement.move.name}}</li>
                        </ul>
                    </div>
                    <div class="d-flex justify-content-center divBgWhite"> 
                        <h3 class="text-center divBgWhite">Habilidades</h3>
                    </div>
                    <div class="d-flex justify-content-center divAbili divBgWhite">
                        <ul class="lista divBgWhite">
                            <li class="divBgWhite" v-for="(skill,index) in skills" :key="index">{{skill.ability.name}}</li>
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
                name: "",
                movements: [],
                skills: [],
                movement: "",
                skill: "",
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
        skills() {
            return this.character.abilities;
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
     created: function () {
      this.fetchCharacter;
    },
    mounted: function () {
        this.character.name = "pikachu";
        this.fetchCharacter();
    },
}
</script>

<style lang="scss" scoped>
.row {
    margin-right: 0;
    margin-left: 0;
}
.miniHeader {
    background-color: #E3350D;

    img {
        background-color: #E3350D;
    }
}
.divColCont {
    background-color: #FFFFFF;

    h3 {
        font-weight: bold;
    }
    .divBgWhite, form, 
    label, .input-group, .input-group-append, h3 {
        background-color: #FFFFFF;
    }
}
.btn-search {
    background-color: #4dad5b;
    color: #ffffff;
    font-weight: 600;
}
.divPoke {
    border: 5px solid #ee6b2f;
    border-radius: 5px;
    margin-bottom: 1rem;
}
</style>