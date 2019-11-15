<template>
    <div>
        <h1>{{msg}}</h1>
        <h3 v-text="titulo + ' olá'"></h3>
        <input v-model="message">
        <button v-on:click="reverseMessage">Inverter</button>
        <p>{{message}}</p>
        <p v-text="titulo + new Date().toLocaleString()"></p>
        
        <span v-if="seen">Mostra Isso</span>
        <img :src="foto.url" :alt="foto.alt">
        <ul>
            <li v-for="foto in fotos" :key="foto.id">
                <img :src="foto.url" :alt="foto.alt" width="188" height="125">
            </li>
        </ul>
    </div>

</template>

<script>
export default {
    name: "Tela",
    props: {
        msg: String
    }, 
    methods: {
        reverseMessage(){
            this.message = this.message.split('').reverse().join('')
        }
    },
    data(){
        return {
            message: "Texto a ser invertido: romano acata amores a damas amadas e Roma ataca o namoro",
            titulo : "Titulo da minha página",
            seen: false,
            foto: {
                url: "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
                alt: "Cachorro"
            },
            fotos: [
                {
                    id: 0,
                    url: "https://images.pexels.com/photos/2220336/pexels-photo-2220336.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Leão"
                },
                {
                    id: 1,
                    url: "https://images.pexels.com/photos/34700/bear-animals-zoo-captivity.jpg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Urso"
                },
                {
                    id: 2,
                    url: "https://images.pexels.com/photos/35992/gorilla-monkey-ape-zoo.jpg?auto=compress&cs=tinysrgb&h=750&w=1260",
                    alt: "Gorilla"
                }
                
            ]
        }
    },
}
</script>


<style scoped>

</style>
