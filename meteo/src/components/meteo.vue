<template>
    <div class="container">
        <div class="row">
            <div class="d-flex justify-content-center">
                <select v-model="selectedCity">
                    <option value="" disabled>Wybierz stacje:</option>
                    <option v-for="item in meteoData" :value="item">{{ item["stacja"] }}</option>
                </select>
            </div>
        </div>
        <div class="row mt-4">
            <div class="d-flex flex-wrap justify-content-center">
                <div v-for="item, key in selectedCity" :key="key">
                    <div class="card m-2" style="width: 15rem; height: 7rem; ">
                        <div class="card-body">
                            <h5 class="card-title">{{ key }}:</h5>
                            <h6 class="card-subtitle mb-2 text-muted">{{ item }}</h6>
                            <p class="card-text">
                                <i v-if="key == 'temperatura' && item <= 0" id="coldTemp" class="card-title icofont-snow-temp"></i>
                                <i v-if="key == 'temperatura' && item > 0" id="hotTemp" class="card-title icofont-sunny-day-temp"></i>
                                <i v-if="key == 'kierunek_wiatru'" style="font-size: var(--set-size);" class="icofont-compass"></i>
                                <i v-if="key == 'predkosc_wiatru'" style="font-size: var(--set-size);" class="icofont-wind"></i>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- <h3>Data pomiaru: {{selectedCity["data_pomiaru"]}}</h3>
    <h4>Godzina: {{selectedCity["godzina_pomiaru"]}}</h4> -->
</template>

<script>

export default {
    name: "meteo",
    data() {
        return {
            meteoData: [],
            selectedCity: "",
        }
    },
    mounted() {
        fetch("https://danepubliczne.imgw.pl/api/data/synop/format/json")
            .then(res => res.json())
            .then(data => this.meteoData = data)
            .catch(err => console.log(err.message))
    },
}
</script>

<style>
:root{
    --set-size: 150%;
}

#hotTemp{
    font-size: var(--set-size);
}

#coldTemp{
    font-size: var(--set-size);
}

</style>