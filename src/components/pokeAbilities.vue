<template>
    <div class="respuesta__habilidades_centrado">
        <div class="habilidad__texto">
            <h3>{{ name }}</h3>
            <p>{{ flavorText }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        pokeAbility: {
            type: Object,
            required: false,
            default() {
                return {
                    'name': 'Habilidad no encontrada',
                    'url': 'URL no encontrada'
                }
            }
        }
    },
    data() {
        return {
            flavorText: '',
            name: '',
        }
    },
    created() {
        const urlRqst = async () => {
            try {
                // fetch ajax al link de habilidades
                let urlAbility = this.pokeAbility.url;
                let res = await fetch(urlAbility);
                let toJson = await res.json();
                
                const langSP = function(json) { 
                    return json.language.name === 'es';
                }

                // busca el nombre en español
                this.name = toJson.names.find(langSP).name;
                
                // busca el flavor text en español
                this.flavorText = toJson.flavor_text_entries.find(langSP).flavor_text;
                
            } catch(err) {
                console.log(err);
            }
        };
        urlRqst();
    }
}
</script>

<style>
.respuesta__habilidades_centrado{
    display: flex;
    justify-content: center;
}
.habilidad__texto {
  width: 75vw;
}
.habilidad__texto h3, .habilidad__texto p {
  margin-bottom: 1rem;
}
</style>