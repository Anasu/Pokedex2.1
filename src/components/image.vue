<template>
    <img :src="imageURL" 
            alt="Pokemon Image" :id="pokeImgUrl">
</template>

<script>
export default {
    props: {
        pokeImgUrl: {
            type: Number,
            required: false,
            default() {
                return 0
            }
        }
    },
    data (){
        return {
            imageURL: 'assets/not-found.png',
        }
    },
    updated() {
        const imgRqst = async () => {
            try {
                // fetch ajax al link de habilidades
                let urlAbility = 'https://www.serebii.net/art/th/' + this.pokeImgUrl + '.png';
                let res = await fetch('https://corsanywhere.herokuapp.com/' + urlAbility);
                
                if(res.status == 200){
                    this.imageURL = urlAbility;
                } else {
                    this.imageURL = 'assets/not-found.png';
                }
                
                //console.log(this.imageURL)
            } catch(err) {
                this.imageURL = 'assets/not-found.png';
            }
        };
        imgRqst();
    }
}
</script>