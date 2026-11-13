<script setup>
import { createBook, deleteBook, GetBooks } from '../api/books';
</script>

<script>
    export default {
        name: "BooksManager",
        data() {
            return {
                books: [],
                newBook: {
                    title: "",
                    author: "",
                    year: 2000,
                }
            };
        },

        mounted() {
            this.loadBooks();
        },

        methods: {
            async loadBooks(){
                this.books = await GetBooks();
            },
            async addBook(book){
                await createBook(book);
                await this.loadBooks();
            },
            async removeBook(id){
                await deleteBook(id);
                await this.loadBooks();
            },
            async submitCreateBook(){
                await this.addBook(this.newBook);
            }
        }

    }
</script>

<template>
    <main class="">
        <h1 class="hi">Könyv kezelő rendszer</h1>

        <form @submit.prevent="submitCreateBook" class="border-2 border-stone-200 p-2 m-2 flex flex-col gap-4">
            <div class="flex flex-col">
                <label for="title" class="">Cím:</label>
                <input v-model="newBook.title" type="text" name="title" class="border-2 border-stone-200 p-1">

            </div>
            <div class="flex flex-col">
                <label for="author" class="">Szerző:</label>
                <input v-model="newBook.author" type="text" name="author" class="border-2 border-stone-200 p-1">

            </div>
            <div class="flex flex-col">
                <label for="year" class="">Év:</label>
                <input v-model="newBook.year" type="number" name="year" class="border-2 border-stone-200 p-1">

            </div>

            <button class="border-2 border-stone-200 p-2" type="submit">Létrehozás</button>
        </form>

        <table>
            <thead>
                <tr>
                    <th class="">azonosító</th>
                    <th class="">cím</th>
                    <th class="">szerző</th>
                    <th class="">év</th>
                    <th class="">műveletek</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="book in books" :key="book.id" class="">
                    <td class="">{{ book.id }}</td>
                    <td class="">{{ book.title }}</td>
                    <td class="">{{ book.author }}</td>
                    <td class="">{{ book.year }}</td>
                    <td class="">
                        <button class="m-2 border-2 border-rose-500 text-rose-500 p-2 cursor-pointer" type="button" @click="removeBook(book.id)">Törlés</button>
                    </td>
                </tr>
            </tbody>
        </table>

    </main>



</template>