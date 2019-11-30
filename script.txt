var cellStatus = [
  [-1 , -1 , -1],
  [-1 , -1 , -1],
  [-1 , -1 , -1]
];
var toggleStatus = 1;
function makePlatform(){
  var table = "<table border = '1px solid black'>"
  for(var i = 0 ; i < 3 ; i++){
    table+="<tr>";
    for(var j = 0 ; j < 3 ; j++){
      table+="<td>";
      if(cellStatus[i][j] == 1 )table+="<div class='innerdiv' id ="+i+j+"><img src='./images/right.gif' class = 'innerImage'></div>";
      else if (cellStatus[i][j] == 0 )table+="<div class='innerdiv' id ="+i+j+"><img src='./images/wrong.gif' class = 'innerImage'></div>";
      else table+="<div class='innerdiv' id ="+i+j+"></div>";
      table+="</td>";
    }
    table+="</tr>";
  }
  document.getElementById("tictactoeground").innerHTML = table;
  if(checkWin() == -1)updatePlatform();
  else{
    document.getElementsByClassName("XClass")[0].classList.add("messageBox");
    var divContent = "";
    if(checkWin() == 1)divContent+="player 1 win !!!";
    else if(checkWin() == 0)divContent+="player 2 Win !!!";
    else if(checkWin() == 2)divContent+= "match draw ";
    divContent += "<input type = 'button' value='play again !!!' class ='message-button blue' onclick = 'restart()'></input>";
    divContent += "<input type = 'button' value='close'  class ='message-button blue' onclick = 'winclose()'></input>";
    document.getElementsByClassName("messageBox")[0].innerHTML = divContent ;
  }
}
function toggle() {
  toggleStatus = (toggleStatus == 1)?0:1;
}
function updatePlatform(){
   for(var i = 0 ; i < 3 ; i++){
     for(var j = 0 ;j < 3 ; j++){
      document.getElementById(""+i+j+"").addEventListener("click", function(){
          if(cellStatus[parseInt(this.id.charAt(0))][parseInt(this.id.charAt(1))] == -1)cellStatus[parseInt(this.id.charAt(0))][parseInt(this.id.charAt(1))] = toggleStatus;
          toggle();
          makePlatform();
      });
     }
   }
}
function restart(){
  cellStatus = [
    [-1 , -1 , -1],
    [-1 , -1 , -1],
    [-1 , -1 , -1]
  ];
  makePlatform();
  document.getElementsByClassName("XClass")[0].classList.remove("messageBox");
  document.getElementsByClassName("XClass")[0].innerHTML="";
}
function winclose()
{
window.close();
}
function checkWin(){
  var winStatus = -1;
  var counter = 0;
  for(var i = 0 ; i < 3 ; i++){
    for(var j = 0 ; j < 3 ; j++){
      if(cellStatus[i][j] == -1)counter++;
    }
  }
  if(counter == 0)return 2;
  for(var i = 0 ; i < 3 ; i++ ){
    if((cellStatus[i][0] == cellStatus[i][1]) && (cellStatus[i][1] == cellStatus[i][2])){
      //if(cellStatus[i][0] == 0 || cellStatus[i][0] == 1)alert(i+""+0+" "+i+""+1+" "+i+""+2+" are same their values are  : "+cellStatus[i][0]+" "+cellStatus[i][1]+" "+cellStatus[i][2]);
      if(cellStatus[i][0] == 1) return 1;
      else if(cellStatus[i][0] == 0)return 0;
    }
    if((cellStatus[0][i] == cellStatus[1][i]) && (cellStatus[1][i] == cellStatus[2][i])){
      //if(cellStatus[0][i] == 0 || cellStatus[0][i] == 1)alert(0+""+i+" "+1+""+i+" "+2+""+i+" are same their values are  : "+cellStatus[0][i]+" "+cellStatus[1][i]+" "+cellStatus[2][i]);
      if(cellStatus[0][i] == 1) return 1;
      else if(cellStatus[0][i] == 0)return 0;
    }
  }
  if((cellStatus[0][0] == cellStatus[1][1]) && (cellStatus[1][1] == cellStatus[2][2])){
    //if(cellStatus[0][0] == 0 || cellStatus[0][0] == 1)alert(0+""+0+" "+1+""+1+" "+2+""+2+" are same their values are  : "+cellStatus[0][0]+" "+cellStatus[1][1]+" "+cellStatus[2][2]);
    if(cellStatus[0][0] == 1) return 1;
    else if(cellStatus[0][0] == 0)return 0;
  }
  if((cellStatus[0][2] == cellStatus[1][1]) && (cellStatus[1][1] == cellStatus[2][0])){
    //if(cellStatus[0][2] == 0 || cellStatus[0][2] == 1)alert(0+""+2+" "+1+""+1+" "+2+""+0+" are same their values are  : "+cellStatus[0][2]+" "+cellStatus[1][1]+" "+cellStatus[2][0]);
    if(cellStatus[0][2] == 1) return 1;
    else if(cellStatus[0][2] == 0)return 0;
  }
  return winStatus;
}
function startGame(){
  makePlatform();
}
startGame();
