<template>
    <div>
        <form @submit="addPlayer">
            <input type ="text" v-model="firstname" name="firstname" placeholder="Enter first name">
            <input type ="text" v-model="lastname" name="lastname" placeholder="Enter last name">
            <input type="text" v-model="year" name="year" placeholder="Enter year">
            <input type="submit" value="Add Player" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: "AddPlayer",
    data() {
        return {
            playerId: '',
            firstname: '',
            lastname: '',
            year: '',
            homeruns: '',
            average: ''
        }
    },
    methods: {
        addPlayer(e) {
            e.preventDefault();
            const newPlayer = {
                playerId: this.playerId,
                firstname: this.firstname,
                lastname: this.lastname,
                year: this.year,
                homeruns: this.homeruns,
                average: this.average
            }
            this.$emit('add-player', newPlayer);

            this.firstname = '';
            this.lastname = '';
            this.year = '';
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2
    }
</style>