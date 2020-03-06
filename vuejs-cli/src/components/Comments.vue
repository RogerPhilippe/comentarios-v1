<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr/>
        <div class="form-todo form-group">
            <p>
                <input v-model="name" placeholder="Nome" type="text" name="author" class="form-control"/>
            </p>
            <p>
                <textarea v-model="message" placeholder="Comentário" name="message" class="form-control"></textarea>
            </p>
            <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
        </div>
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
export default {
    data() {
        return {
            comments: [],
            name: '',
            message: ''
        }
    },
    methods: {
        addComment() {
            if (this.message.trim() === '') { return; }
            this.comments.push({
                name: this.name,
                message: this.message
            });
            this.name = '';
            this.message = '';
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