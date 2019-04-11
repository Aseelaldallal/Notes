Fullname.vue

```
<template>
    <div>

        <div class="form-group">
            <label for="firstname">First Name</label>
            <input class="form-control" name="firstname" type="text" v-model="firstname" @input="save">
        </div>
        <div class="form-group">
            <label for="lastname">Last Name</label>
            <input class="form-control" name="lastname" type="text" v-model="lastname" @input="save">
        </div>

    </div>

</template>

<script>
export default {
    data() {
        return {
            firstname: '',
            lastname: ''
        }
    },
    props: ['value'],
    methods: {
        save() {
            this.$emit('input', { firstname: this.firstname, lastname: this.lastname});
        }
    }
}
</script>
```
 App.vue
 
 ```
 <template>
    <div class="container">
        <form v-if="!submitted">
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <app-fullname v-model="userData.fullname"></app-fullname>
  ...
 ```
