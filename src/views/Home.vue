
<script>
import { ref, reactive } from "vue";

export default {
    name: "Home",
    setup() {
        const TABLES = {
            race: [
                "Human",
                "Human",
                "Human",
                "Human",
                "Aen Seidhe",
                "Aen Seidhe",
                "Aen Seidhe",
                "Dwarf",
                "Dwarf",
                "Dwarf"
            ],
            gender: [
                "Male",
                "Female",
                "Male",
                "Female",
                "Male",
                "Female",
                "Male",
                "Female",
                "Male",
                "Female"
            ],
            age: [
                "Child",
                "Child",
                "Teen",
                "Teen",
                "Young Adult",
                "Young Adult",
                "Adult",
                "Adult",
                "Elder",
                "Elder"
            ],
            personality: [
                "Shy",
                "Rebellious",
                "Arrogant",
                "Headstrong",
                "Friendly",
                "Secretive",
                "Nervous",
                "Flirtatious",
                "Eccentric",
                "Aloof"
            ],
            history: [
                "Lost everything",
                "Family was killed",
                "Fought in the Northern War",
                "Thinks they have magic",
                "Almost died",
                "Saved by a witcher",
                "Used to be a priest",
                "Once ruled a small town",
                "Lived as a bandit",
                "Killed a dangerous monster"
            ],
            standing: [
                "Slave",
                "Slave",
                "Poor",
                "Poor",
                "Poor",
                "Average",
                "Well to do",
                "Well to do",
                "Rich",
                "Nobility"
            ],
            romance: [
                "None",
                "None",
                "None",
                "Uninterested in love",
                "Debauchery",
                "Playboy",
                "Interested in a player",
                "A dedicated lover",
                "Married",
                "Star-crossed lovers"
            ],
            secret: [
                "Is secretly a mage",
                "Found a lost treasure",
                "Is a wanted criminal",
                "Is a secret service agent",
                "Has a secret life",
                "Has a Secret Profession",
                "Is a cross-dresser",
                "Is a deserter",
                "Has a secret lover",
                "Has a hex or curse"
            ]
        };

        let npc = reactive({});
        let saved_properties = reactive({});

        function rollD(sides) {
            return Math.floor(Math.random() * sides);
        }

        function regenerate() {
            for (let property in TABLES) {
                if (!saved_properties[property]) {
                    npc[property] = TABLES[property][rollD(10)];
                }
            }
        }

        function capitalize(text) {
            return text.substring(0, 1).toUpperCase() + text.substr(1);
        }

        regenerate();
        return {
            TABLES,
            npc,
            saved_properties,

            regenerate,
            capitalize
        };
    }
};
</script>



<template>
    <div class="home">
        <h1>The Witcher TTRPG NPC Generator</h1>

        <button class="btn btn-primary"
                @click="regenerate">Regenerate</button>

        <hr />

        <div class="container">
            <div class="row">
                <div class="text-right col-1">Save</div>
                <div class="text-right col-2"></div>
                <div class="text-left col-9"></div>
            </div>
            <div class="row"
                 v-for="(table_values, table_name) in TABLES"
                 :key="`row_${table_name}`">
                <div class="text-right col-1"><input type="checkbox"
                           class="form-control"
                           v-model="saved_properties[table_name]"></div>
                <div class="text-right col-2"
                     v-text="`${capitalize(table_name)}:`"></div>
                <div class="text-left col-9 font-weight-bold"
                     v-text="npc[table_name]"></div>
            </div>
        </div>

        <hr />

        <footer class="container">
            Content &copy; R. Talsorian Games, Inc., 2018
            <br />
            The Witcher TTRPG Core Rule Book, Page 226
        </footer>
    </div>
</template>
