<template>
    <div id="app">
        <p>Имя<input v-model="cur_note.first_name"></p>
        <p>Отчество<input v-model="cur_note.third_name"></p>
        <p>Фамилия<input v-model="cur_note.second_name"></p>
        <p>Номер телефона<input v-model="cur_note.phone"></p>
        <p>Избранный<input type="checkbox" v-model="cur_note.favorite"></p>
        <p>Сортировать по имени<input value="name" type="radio" v-model="sort" v-on:click="toggleSort('name')"></p>
        <p>Сортировать по фамилии<input value="sec_name" type="radio" v-model="sort" v-on:click="toggleSort('sec_name')"></p>
        <p><button v-on:click="toggleSave()">Сохранить</button></p>
        <li v-for="(item, index) in notes" v-bind:key=index>{{item.first_name}} {{item.third_name}} {{item.second_name}} {{item.phone}} <span v-if="item.favorite"> Избранный</span><button v-on:click="toggleEdit(index)">Изменить</button><button v-on:click="toggleDelete(index)">Удалить</button></li>

    </div>
</template>

<script>
    export default {
        name: "phone_book",
        data() {
            return {
                sort: "name",
                cur_note: {
                    first_name: "",
                    second_name: "",
                    third_name: "",
                    phone: "",
                    favorite: false
                },
                notes: [],
                editing: -1 //состояние при новой записи
            }
        },
        methods: {
            toggleSave: function () {
                if (this.cur_note.phone !== "") {
                    if (this.editing === -1) {
                        this.notes.push({
                            first_name: this.cur_note.first_name,
                            second_name: this.cur_note.second_name,
                            third_name: this.cur_note.third_name,
                            phone: this.cur_note.phone,
                            favorite: this.cur_note.favorite});
                    }
                    else {
                        this.notes[this.editing] = {
                            first_name: this.cur_note.first_name,
                            second_name: this.cur_note.second_name,
                            third_name: this.cur_note.third_name,
                            phone: this.cur_note.phone,
                            favorite: this.cur_note.favorite};
                        this.editing = -1;
                    }
                    if(this.sort === "name")
                        this.notes.sort((a, b) => a.first_name < b.first_name ? 1 : -1);
                    else if (this.sort === "sec_name")
                        this.notes.sort((a, b) => a.second_name < b.second_name ? 1 : -1);
                    this.notes.sort((a, b) => a.favorite < b.favorite ? 1 : -1);
                    this.cur_note.first_name = "";
                    this.cur_note.second_name = "";
                    this.cur_note.third_name = "";
                    this.cur_note.phone = "";
                    this.cur_note.favorite = "";
                }else{
                    alert("Заметка не может быть пустой");
                }
            },
            toggleEdit : function (id) {
                this.cur_note = this.notes[id];
                this.editing = id;
            },
            toggleDelete : function (id) {
                this.notes.splice(id, 1);
            },
            toggleSort : function (value) {
                if(value === "name")
                    this.notes.sort((a, b) => a.first_name < b.first_name ? 1 : -1);
                else if (value === "sec_name")
                    this.notes.sort((a, b) => a.second_name < b.second_name ? 1 : -1);
                this.notes.sort((a, b) => a.favorite < b.favorite ? 1 : -1);
            }
        }
    }
</script>

<style scoped>

</style>