<template>
    <div class="player-item">
        <!--
        
        *** this code is for the original display of the player data ***
        
        <p>
            {{player.firstname}} {{player.lastname}} ({{player.year}}) - HR: {{player.homeruns}}, Avg: {{player.average}}
            <button @click="$emit('del-player', player.playerId)" class="del">x</button>
        </p>
        -->
    </div>
</template>

<script>
export default {
    name: "PlayerItem",
    props: ["player"]
}
</script>

<style scoped>
    .player-item {  
        background: #f4f4f4;
        padding: 20px;
        border-bottom: 1px #ccc dotted;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px, 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>