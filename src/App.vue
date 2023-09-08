<template>
  <div>
    <h1 class="text-center mt-5">เกมเป่ายิงฉุบ</h1>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h5 class="text-center">player 1</h5>
        <img :src="player1" alt="">
      </div>

      <div class="user2">
        <h5 class="text-center">Bot Ai</h5>
        <img :src="player2" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">เป่ายิงฉุบ</button>
      <button @click="Resetgame" class="btn btn-success mx-4">เริ่มใหม่</button>
    </div>
  </div>

  <div class="score mt-3 d-flex justify-content-center">
    <div class="d-flex justify-content-center bg-success p-2 text-dark bg-opacity-25 ">

      <p class="fs-5"> คะแนน {{ scorePlayer }} : {{ scorebotplayer }}</p>
    </div>
</div>

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">ผล</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      playerChoice: '',
      botChoice: '',
      player1: "https://im4.ezgif.com/tmp/ezgif-4-ea188a4dae.webp", 
      player2: "https://im4.ezgif.com/tmp/ezgif-4-84a7076d35.webp", 
      resultMessage: '',
      scorePlayer: 0, 
      scorebotplayer: 0,  
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.playerChoice = this.choices[randomIndex1];
      this.botChoice = this.choices[randomIndex2];

      this.player1 = this.getImagePath(this.playerChoice);
      this.player2 = this.getImagePath(this.botChoice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return "https://i.ibb.co/kyQZB68/hammer.png";
      } else if (choice === 'กระดาษ') {
        return "https://i.ibb.co/bRQWLRW/paper.png";
      } else if (choice === 'กรรไกร') {
        return "https://i.ibb.co/Wp4xgCN/scissors.png";
      }
    },
    calculateWinner() {
      if (this.playerChoice === this.botChoice) {
        this.resultMessage = 'เสมอ';        
      } else if (this.playerChoice ==="ค้อน" && this.botChoice === "กรรไกร" || 
      this.playerChoice ==="กรรไกร" && this.botChoice === "กระดาษ" ||
       this.playerChoice ==="กระดาษ" && this.botChoice === "ค้อน"  ) {
        this.resultMessage = 'player win';
        this.scorePlayer++; 
      } else {
        this.resultMessage = 'Bot Ai';
        this.scorebotplayer++;       
      }
    },
      Resetgame(){
        window.location.reload(); 
      }
    
    }
  
};
</script>

<style>
.user1,.user2{
  border: 2px solid rgb(178, 184, 182);
  padding: 50px;
}
.box-game img{
  width: 250px;
  height: 250px;
}
.user1{
  margin-right: 60px;
}
.modal-body img{
margin-left: 100px;
}
</style>
