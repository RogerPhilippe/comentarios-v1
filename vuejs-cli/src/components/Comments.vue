<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr/>
        <FormTodo v-on:add-todo="addComment"></FormTodo>
        <div class="list-group">
            <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="comment.id">
                <span class="comment_author">Autor: <strong>{{comment.name}}</strong></span>
                <p>{{comment.message}}</p>
                <div>
                    <a href="#" v-on:click.prevent="remove(index)" title="Excluir">Excluir</a>
                </div>
            </div>
        </div>
        <hr/>
    </div>
</template>

<script>

import FormTodo from './FormTodo'

export default {
    components: {
        FormTodo
    },
    data() {
        return {
            comments: []
        }
    },
    methods: {
        addComment(comment) {
            this.comments.push(comment);
        },
        remove(index) {
            this.comments.splice(index, 1);
        }
    },
    computed: {
        allComments() {
            return this.comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === '' ? 'Anônimo' : comment.name
            }))
        }
    },
    watch: {
        comments() {
            console.log('Comentário adicionado ou excluido.')
        }
    }
}
</script>