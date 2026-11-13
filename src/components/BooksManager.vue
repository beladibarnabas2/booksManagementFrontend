<script setup>
import { GetBooks } from '../api/books';
</script>

<script>
    export default {
        name: "BooksManager",
        data() {
            return {
                books: [],
            };
        },

        mounted() {
            this.loadBooks();
        },

        methods: {
            async loadBooks(){
                this.books = await GetBooks();
            }
        }

    }
</script>

<template>
    <main class="">
        <div class="hi">Könyv kezelő rendszer</div>

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
                    <td class="">-</td>
                </tr>
            </tbody>
        </table>

    </main>



</template>