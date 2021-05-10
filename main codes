var MatchSimulator = function (matchstat) {
    this.matchstat = matchstat;
    this.ballUpdates = [];
};

MatchSimulator.prototype.startMatch = function () {

    var matchstat = this.matchstat;
    console.log(matchstat.totalBalls / 6 + " over(s) left. " + matchstat.target + " to win.");

    while (matchstat.recquiredRuns > 0 && matchstat.balls < matchstat.totalBalls && matchstat.wickets < matchstat.team.players.length - 1) {
        var playerId = matchstat.team.currentPlayers[0].playerId;
        var runs = matchstat.team.getBallResult();
        matchstat.updateRuns(playerId, runs);
        this.ballUpdates.push({ 'playerId': playerId, 'runs': runs });
        MatchSimulator.printBallUpdates(matchstat);
    }
    this.endGame();
    return ({ 'matchstat': this.matchstat, 'ballUpdates': this.ballUpdates });
};

/* Prints output in console */

MatchSimulator.printBallUpdates = function (matchstat) {
    var print = Math.floor(matchstat.balls / 6) + "." + (matchstat.balls % 6) + "  " + matchstat.currentPlayer.name;
    print += (matchstat.currentRuns != "out") ? " scores " + matchstat.currentRuns + " run(s) " : " is out";

    if (matchstat.balls % 6 == 0) {
        var remainingBalls = matchstat.totalBalls - matchstat.balls;
        var recquiredRuns = matchstat.recquiredRuns ? matchstat.recquiredRuns : " - ";
        print += "\n" + remainingBalls / 6 + " over(s) left. " + recquiredRuns + " to win.";
    }

    console.log(print);
}

MatchSimulator.prototype.endGame = function () {
    var matchstat = this.matchstat;

    var winningTeam = matchstat.recquiredRuns > 0 ? matchstat.bowlingTeam : matchstat.battingTeam;
    var winsBy = (matchstat.recquiredRuns > 0) ?
        matchstat.recquiredRuns + " runs." :
        (matchstat.team.players.length - matchstat.wickets - 1) + " wickets and " + (matchstat.totalBalls - matchstat.balls) + " balls remaining";
    var print = winningTeam.name + " won by " + winsBy;

    console.log(print);
    this.printPlayers();
};

MatchSimulator.prototype.printPlayers = function () {
    var players = this.matchstat.team.players;
    players.forEach(function (player) {
        if (player.isOut || player.isPlaying) {
            print = player.name + " - " + player.score;
            print += player.isPlaying ? " * " : " ";
            print += "( " + player.ballsPlayed + " balls)";
            console.log(print);
        }
    });
};

module.exports = MatchSimulator;
