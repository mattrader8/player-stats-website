<template>
  <div id="app">
    <Header/>
    <AddPlayer v-on:add-player="addPlayer"/>
    <Players v-bind:players="players" v-on:del-player="deletePlayer"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import AddPlayer from './components/AddPlayer';
import Players from './components/Players';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    AddPlayer,
    Players
  },
  data() {
    return {
      players: []
    }
  },
  methods: {

    // deletePlayer method was for the original PlayerItem display - need to rework it for the data table

    deletePlayer(playerId) {
      this.players = this.players.filter(player => player.playerId!== playerId);
    },
    addPlayer(newPlayer) {
      const firstname = newPlayer.firstname;
      const lastname = newPlayer.lastname;
      const year = newPlayer.year;

      if(firstname == '' || lastname == '' || year == '') {
        alert('Please enter player first name, last name, and year.');
        throw 'Please enter player first name, last name, and year.';
      }

      const playerBioRequest = "http://lookup-service-prod.mlb.com/json/named.search_player_all.bam?" + "sport_code='mlb'&active_sw='Y'&name_part=%27" + firstname + "%20" + lastname + "%27"
      
      var playerBioObj;
      var playerDataObj; 
      
      var playerId;
      var homeruns;
      var average;

      axios.get(playerBioRequest)
        .then(res => {
          playerBioObj = (JSON.parse(JSON.stringify(res)));
          playerId = playerBioObj.data.search_player_all.queryResults.row.player_id;

          var playerDataRequest = "http://lookup-service-prod.mlb.com/json/named.sport_hitting_tm.bam?league_list_id='mlb'&game_type='R'&season=%27" + year.toString() + "%27&player_id=%27" + playerId.toString() + "%27"
          
          axios.get(playerDataRequest)
            .then(res => {
              playerDataObj = (JSON.parse(JSON.stringify(res)))
              newPlayer.homeruns = playerDataObj.data.sport_hitting_tm.queryResults.row.hr;
              newPlayer.average = playerDataObj.data.sport_hitting_tm.queryResults.row.avg;
              newPlayer.playerId = playerId;
              newPlayer = [playerId, firstname, lastname, year, homeruns, average];
            })
            .catch(err => console.log(err));
        })
        .catch(err => console.log(err));

      this.players = [...this.players, newPlayer];
    }
  }
}
</script>

<style>
  * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, Helvetica, sans-serif;
      line-height: 1.4;
    }

    .btn {
      display: inline-block;
      border: none;
      background: #555;
      color: #fff;
      padding: 7px 20px;
      cursor: pointer;
    }

    .btn:hover {
      background: #666;
    }
</style>