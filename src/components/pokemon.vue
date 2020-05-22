<template>
    <div class="respuesta" >
        <div class="pokemon__card">
            <div class="respuesta__titulo">
                <poke-image :pokeImgUrl="objRqstd.id"></poke-image>
                <poke-data :pokeName="pokemonName" :pokeID="pokemonID"></poke-data>
            </div>
            <div v-if="status == 'ok'">
                <div class="respuesta__habilidades">
                    <h2>Habilidades</h2>
                    <poke-abilities 
                        v-for="ability in abilities"
                        :pokeAbility="ability.ability"
                        :key="ability.name">
                    </poke-abilities>
                </div>
                <div class="respuesta__movimientos">
                    <h2>Movimientos</h2>
                    <poke-moves
                        v-for="move in moves"
                        :pokeMove="move.move"
                        :key="move.name">
                    </poke-moves>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import pokeImage from './image.vue';
import pokeData from './pokeData.vue';
import pokeAbilities from './pokeAbilities.vue';
import pokeMoves from './pokeMoves.vue';

export default {
    data() {
        return {
            abilities: [],
            moves: [],
            pokemonName: '',
            pokemonID: 0,
        }
    },
    components: {
        pokeImage,
        pokeData,
        pokeAbilities,
        pokeMoves
    },
    props: {
        objRqstd: {
            type: Object,
            required: false,
            default() {
                return {};
            }
        },
        status: {
            type: String,
            required: true,
            default() {
                return 'hidden';
            }
        }
    }, 
    created() {

    },
    updated() {
        this.abilities = this.objRqstd.abilities;
        this.moves = this.objRqstd.moves;
        this.pokemonName = this.objRqstd.name;
        this.pokemonID = this.objRqstd.id;
    }
}
</script>