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
            <app-fullname v-model="userData.fullname"></app-fullname>
  ...
  </template>
  
  <script>
    import Fullname from './Fullname.vue'
    export default {
        data() {
            return {
                userData: {
                    fullname: {
                        firstname: '',
                        lastname: ''
                    },
                   ...
                },
                ...
            }
        },
        components: {
            appFullname: Fullname
        },
        methods: {
            storeName(fullname) {
                this.userData.fullname = fullname;
            }
        }
    }
</script>

 ```


Better ALTERNATIVE ?

```
<template>
    <div>

        <div class="form-group">
            <label for="firstname">First Name</label>
            <input class="form-control" name="firstname" type="text" :value="firstName" @input="nameChanged(true, $event)">
        </div>
        <div class="form-group">
            <label for="lastname">Last Name</label>
            <input class="form-control" name="lastname" type="text" :value="lastName" @input="nameChanged(false, $event)">
        </div>

    </div>

</template>

<script>
export default {
    props: ['value'],
    computed: {
        firstName() {
            return this.value.split(" ")[0];
        },
        lastName() {
            return this.value.split(" ")[1];
        }
    },
    methods: {
        nameChanged(isFirst, event) {
            let name='';
            if(isFirst) {
                name = event.target.value + ' ' + this.lastName;
            } else {
                name = this.firstName + ' ' + event.target.value;
            }
            this.$emit('input', name);
        }
    }
}
</script>
```
