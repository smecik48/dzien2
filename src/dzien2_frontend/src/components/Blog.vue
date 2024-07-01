<template>
    <div>
        <h1 class="text-blue-600">Wpisy na bloga</h1>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-blue-600 rounded text-white p-4">refresh</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
        <div v-for="(wpis, index) in wpisy" class="drop-shadow-x1 bg-stone-300 p-4">
            <p>{{ wpis }}</p>
            <button @click="usunWpis(index)" class="bg-blue-600 rounded text-white p-4">Usun</button>
            <div>
                <input type="text" v-model="edycja[index]" class="border-2 border-blue-600 p-4">
                <button @click="edytujWpis(index, edycja[index])" class="bg-blue-600 rounded text-white p-4">Edytuj</button>
            </div>

        </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="nowyBlog" type="text" class="border-2 border-blue-600 p-4">
            <button @click="dodajWpis" class="bg-blue-600 rounded text-white p-4">Dodaj</button>
        </div>
    </div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';
    export default{
        data(){
            return{
                wpisy: [],
                nowyBlog: "",
                edycja: []
            }
        },
        methods: {
            async dodajWpis(){
                await dzien2_backend.dodaj_wpis(this.nowyBlog);
                await this.pobierzWpisy();
            },
            async usunWpis(index){
                await dzien2_backend.usun_wpis(index);
                await this.pobierzWpisy();
            },
            async pobierzWpisy(){
                this.wpisy = await dzien2_backend.odczytaj_wpisy();
            },
            async edytujWpis(index, nowyWpis){
                await dzien2_backend.edytuj_wpis(index, nowyWpis);
                await this.pobierzWpisy();
            },
            async mounted(){
                this.pobierzWpisy();
            }
            
    }}
</script>