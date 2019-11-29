<template>
    <div class="corpo">
        <h1 class="centralizado">{{msg}}</h1>
        <input
            type="search"
            placeholder="Filtre pelo nome da foto"
            class="filtro"
            @input="filtro = $event.target.value"
        />
        <ul class="lista-fotos">
            <li v-for="user in fotosComFiltro" :key="user.id" class="lista-fotos-item">
                <meu-painel :titulo="user.first_name + ' ' +  user.last_name">
                    <img
                        class="imagem-responsiva"
                        :src="user.avatar"
                        :alt="user.first_name + ' ' + user.last_name"
                        :title="user.first_name + ' ' +  user.last_name"
                        width="187px"
                        height="128px"
                    />
                </meu-painel>
            </li>
        </ul>
    </div>

</template>

<script>

import axios from "axios";
import Painel from "./shared/Painel"
export default {
    computed: { // olha as alteracoes que houveram dentro do data()
        fotosComFiltro() {
            if(this.filtro) {
                let expressaoRegular = new RegExp(this.filtro.trim(), "i");
                return this.users.filter((user) => expressaoRegular.test(user.first_name));
            } else {
                return this.users;
            }
        }
    },
    components: {
        "meu-painel": Painel
    },
    name: "Tela",
    props: {
        msg: String,
    },
    methods: {
        reverseMessage(){
            this.message = this.message.split('').reverse().join('')
        }
    },
    created() {
        this.loading = true;
        axios
            .get("https://reqres.in/api/users")
            .then(response => {
                this.loading = false;
                this.users = response.data.data;
            }).catch(error => {
                this.loading = false;
                this.errors.push(error);
            })
    },

    data(){
        return {
            message: "Texto a ser invertido: romano acata amores a damas amadas e Roma ataca o namoro",
            titulo : "Titulo da minha página",
            seen: false,
            loading: false,
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
            ],
            users:[],
            errors: [],
            filtro: ''
        }
    },
}
</script>


<style scoped>
.filtro {
    display: block;
    width: 100%;
}

.centralizado {
  text-align: center;
}

.corpo {
  font-family: Helvetica, Arial, sans-serif;
  margin: 0 auto;
  width: 96%;
  color: gray;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

/* estilo do painel */

.imagem-responsiva {
    width: 100%;
}

</style>
