<template>
    <div>
        <!--
        
        *** commented out code creates PlayerItem or DataTable instance for every player added - not how I want this to work ***

        <div v-bind:key="player.playerId" v-for="player in players">
            <PlayerItem v-bind:player="player" v-on:del-player="$emit('del-player', player.playerId)"/>
            <DataTable v-bind:player="player"/>
        </div>
        -->
        <table id="DataTable">
            <thead>
                <tr>
                    <th>Player Id</th>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>Year</th>
                    <th>HR</th>
                    <th>Avg</th>
                </tr>
            </thead>
            <tbody>
                <tr v-bind:key="player.playerId" v-for="player in players">
                    <td>{{player.playerId}}</td>
                    <td>{{player.firstname}}</td>
                    <td>{{player.lastname}}</td>
                    <td>{{player.year}}</td>
                    <td>{{player.homeruns}}</td>
                    <td>{{player.average}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
//import PlayerItem from './PlayerItem.vue';
//import DataTable from './layout/DataTable';
export default {
    name: "Players",
    components: {
        //PlayerItem
        //DataTable
    },
    props: ["players"]
}
</script>

<style scoped>
    table {
        font-family: Arial, Helvetica, sans-serif;
        width: 750px;
        border-collapse: collapse;
        border: 3px solid #333;
        margin: 10px 10px 0 10px;
    }

    table th {
        text-transform: uppercase;
        text-align: left;
        background: #333;
        color: #FFF;
        padding: 8px;
        min-width: 30px;
    }

    table td {
        text-align: left;
        padding: 8px;
        border-right: 2px solid #333;
    }
    table td:last-child {
        border-right: none;
    }
        table tbody tr:nth-child(2n) td {
        background: #D4D8F9;
    }
</style>