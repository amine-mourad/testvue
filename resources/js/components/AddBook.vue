<template>
    <div>
        <h3 class="text-center">Add Book</h3>
        <div class="row">
            <div class="col-md-12" v-for="(bok, index) in book" :key="index">
                    <div class="form-group col-md-6">
                        <label>Name</label>
                        <input type="text" class="form-control" v-model="bok.name">
                    </div>
                    <div class="form-group col-md-5">
                        <label>Author</label>
                        <input type="text" class="form-control" v-model="bok.author">
                    </div>
                    <div class="form-group col-md-1">
                        <label>Remove</label>
                        <button class="btn btn-success" @click="removeItem(index)">X</button>
                    </div>
            </div> 
            <div class="col-md-12">
                <div class="form-group col-md-1">
                    <button class="btn btn-success" @click="addItem()">add</button>
                    <button type="submit" class="btn btn-primary" @click="addBook()">Add Book</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                book: [{
                    name: "",
                    author:""}
                    ],
            }
        },
        methods: {
            addBook() {
                this.axios
                    .post('/api/book/add', this.book)
                    .then(response => (
                        this.$router.push({name: 'home'})
                        // console.log(response.data)
                    ))
                    .catch(error => console.log(error))
                    .finally(() => this.loading = false)
                    console.log(this.book)
            },
            addItem(){
                this.book.push({name: "",author:""})
            },
            removeItem (index) {
               this.book.splice(index, 1);
            },
        }
    }
</script>