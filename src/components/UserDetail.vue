<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User Name: {{ switchName() }}</p>
        <p>User Age: {{ userAge }}</p>
        <button @click="resetName">Reset Name</button>
        <button @click="resetFn()">Reset Name</button>
    </div>
</template>

<script>
    import { eventBus } from '../main';

    export default {
        props: {
            myName: {
                type: String
            },
            resetFn: {
                type: Function
            },
            userAge: {
                type: Number
            }
        },
        data: function() {
            return {
                name: this.myName
            };
        },
        methods: {
            switchName() {
                return this.myName.split("").reverse().join("");
            },
            resetName() {
                this.name = 'Marko';
                this.$emit('nameWasReset', this.name);
            },
            created() {
                eventBus.$on('ageWasEdited', (data) => {
                    this.userAge = data;
                });
            }
        }
    }
</script>

<style scoped>
    div {
        background-color: lightcoral;
    }
</style>
