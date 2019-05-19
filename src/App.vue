<template>
    <div class="w-select" @mouseleave="hideCheckboxes">
        <div class="w-select-box" @click="showCheckboxes()">
            <select>
                <option>
                    <div>
                        {{namesSelected}}
                    </div>
                </option>
            </select>
            <div class="w-over-select"></div>
        </div>
        <div id="checkboxes">
            <label v-for="item in items" :key="item.id" class="w-container">
                <input v-model="selecteds" type="checkbox" :value="item"/>
                <span class="w-checkmark"></span>
                {{item.text}}
            </label>
        </div>
        <pre style="display: none">
         {{$data}}
        </pre>
    </div>
</template>
<script>
    export default {
        name: 'app',
        data: function () {
            return {
                expanded: false,
                checkboxes: '',
                selecteds: [],
                items: [
                    {id: '1', text: 'APARTAMENTO'},
                    {id: '2', text: 'CASA'},
                    {id: '3', text: 'KITNETE'},
                    {id: '4', text: 'LOFT'},
                    {id: '5', text: 'LOJA'},
                    {id: '6', text: 'SALA'}
                ]
            }
        },
        computed: {
            namesSelected() {
                var self = this
                var result = '';
                if (self.selecteds.length === 0) {
                    result = " SELECIONE";
                }
                for (var key in self.selecteds) {
                    if (self.selecteds.hasOwnProperty(key)) {
                        if (self.selecteds.length < 2) {
                            result += self.selecteds[key].text;
                        } else if (self.selecteds.length >= 2 && self.selecteds.length <= 3) {
                            result += self.selecteds[key].text + ", ";
                        } else if (self.selecteds.length > 3) {
                            result = self.selecteds.length + " SELECIONADOS";
                        } else {
                            result = " SELECIONE";
                        }
                    }
                }
                return result
            }
        },
        methods: {
            showCheckboxes() {

                if (this.expanded === true) {
                    this.checkboxes = document.getElementById("checkboxes");
                    this.checkboxes.style.display = "none";
                    this.expanded = false;
                } else {
                    this.checkboxes = document.getElementById("checkboxes");
                    this.checkboxes.style.display = "block";
                    this.expanded = true;
                }

            },
            hideCheckboxes() {
                if (this.expanded === true) {
                    this.checkboxes = document.getElementById("checkboxes");
                    this.checkboxes.style.display = "none";
                    this.expanded = false;
                }
            }
        },
        mounted() {}
    }
</script>
<style>

    .w-select {
        display: block;
        height: 30px;
    }

    .w-select-box {
        position: relative;
    }

    .w-select-box select {
        width: 100%;
        color: white;
        width: 100%;
        background-color: black;
        height: 30px;
    }

    .w-over-select {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
    }

    #checkboxes {
        display: none;
        border: 1px #dadada solid;
    }

    #checkboxes label {
        display: block;
        border-bottom: #e9e9e9 1px solid;
    }

    #checkboxes label:hover {
        background-color: #e8e8e8;
    }

    /* The w-container */
    .w-container {
        display: block;
        position: relative;
        padding-left: 27px;
        margin-bottom: 3px;
        cursor: pointer;
        padding-bottom: 4px;
        font-size: 15px;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    /* Hide the browser's default checkbox */
    .w-container input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
        height: 0;
        width: 0;
    }

    /* Create a custom checkbox */
    .w-checkmark {
        position: absolute;
        top: 0;
        left: 0;
        height: 20px;
        width: 20px;
        background-color: #eee;
    }

    /* On mouse-over, add a grey background color */
    .w-container:hover input ~ .w-checkmark {
        background-color: #ccc;
    }

    /* When the checkbox is checked, add a blue background */
    .w-container input:checked ~ .w-checkmark {
        background-color: rgba(12, 156, 23, 0.71);
    }

    /* Create the checkmark/indicator (hidden when not checked) */
    .w-checkmark:after {
        content: "";
        position: absolute;
        display: none;
    }

    /* Show the checkmark when checked */
    .w-container input:checked ~ .w-checkmark:after {
        display: block;
    }

    /* Style the checkmark/indicator */
    .w-container .w-checkmark:after {
        left: 6px;
        top: 2px;
        width: 5px;
        height: 10px;
        border: solid white;
        border-width: 0 3px 3px 0;
        -webkit-transform: rotate(45deg);
        -ms-transform: rotate(45deg);
        transform: rotate(45deg);
    }

</style>
