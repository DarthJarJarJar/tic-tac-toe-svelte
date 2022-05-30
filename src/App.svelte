<script>
	let winner = ""; 
	$: buttonsDict = {
		"11": "",
		"12": "",
		"13": "",
		"21": "",
		"22": "",
		"23": "",
		"31": "",
		"32": "",
		"33": "",
	}

	let rows = [['11','12','13'], ['21','22','23'],['31','32','33']]
	let cols = [['11','21','31'], ['12','22','32'],['13','23','33']]
	let diagonals = [['11', '22', '33'], ['13','22','31']]

	let playerNumber = true
	let move = {
		true:"X",
		false:"O"
	}

	$: currentPlayer = move[playerNumber]
	let draw = false
	function buttonClick(coordiantes) {
		if(winner == ""){
		if(buttonsDict[coordiantes]==""){
			buttonsDict[coordiantes]=move[playerNumber]
			playerNumber = !playerNumber
			checkWinnerCol()
			checkWinnerDiagonal()
			checkWinnerRow()
			draw = checkDraw()
			
		} 
	} }
	function checkWinnerRow(){for(let i= 0; i<=2;i++ ){
			
			if(buttonsDict[rows[i][0]]==buttonsDict[rows[i][1]] && buttonsDict[rows[i][1]]==buttonsDict[rows[i][2]] ){
				winner = buttonsDict[rows[i][0]]
				if(winner != ''){
						break
					}
				}
				}}
	function checkWinnerCol(){for(let j= 0; j<=2;j++ ){
			
		if(buttonsDict[cols[j][0]]==buttonsDict[cols[j][1]] && buttonsDict[cols[j][1]]==buttonsDict[cols[j][2]] ){
			winner = buttonsDict[cols[j][0]]
			if(winner != ''){
					break
				}
			}
			}}
			
		
	function checkWinnerDiagonal(){	for(let k = 0; k<=1;k++ ){
		if(buttonsDict[diagonals[k][0]]==buttonsDict[diagonals[k][1]] && buttonsDict[diagonals[k][1]]==buttonsDict[diagonals[k][2]]){
			winner = buttonsDict[diagonals[k][0]]
		
			}
			}	
		}
	function newGame () {
		winner=""
		buttonsDict = {
		"11": "",
		"12": "",
		"13": "",
		"21": "",
		"22": "",
		"23": "",
		"31": "",
		"32": "",
		"33": "",
	}
		playerNumber = true
		draw = false
	}
	$: fullboard = false
	function checkDraw(){
		for(let prop in buttonsDict){
			if(buttonsDict[prop]==""){
				fullboard = false
				break
			} else{
				fullboard = true
			}
		}
		return fullboard
	}
	
	


</script>
<body>
<main>
	
	{#if winner != "" }
		<p class="message">{winner} has won!</p>
	{:else if draw==true} <p class="message">It's a draw!</p>
	{:else if draw==false} <p class="message">Current player: {currentPlayer}</p>
		
	{/if}
		
	

		<br>
	<div>
		<span>
			<button on:click={ () => buttonClick("11")} class={buttonsDict[11]}>{buttonsDict[11]}</button>
			<button on:click={ () => buttonClick("12")} class={buttonsDict[12]} >{buttonsDict[12]}</button>
			<button on:click={() => buttonClick("13")} class={buttonsDict[13]}>{buttonsDict[13]}</button>
		</span>
	</div>

	<div>
		<span>
			<button on:click={() => buttonClick("21") } class={buttonsDict[21]} >{buttonsDict[21]}</button>
			<button on:click={() => buttonClick("22")} class={buttonsDict[22]} >{buttonsDict[22]}</button>
			<button on:click={() => buttonClick("23")} class={buttonsDict[23]}>{buttonsDict[23]}</button>
		</span>
	</div>

	<div>
		<span>
			<button on:click={() => buttonClick("31")} class={buttonsDict[31]}>{buttonsDict[31]}</button>
			<button on:click={() => buttonClick("32")} class={buttonsDict[32]}>{buttonsDict[32]}</button>
			<button on:click={() => buttonClick("33")} class={buttonsDict[33]}>{buttonsDict[33]}</button>
		</span>
	</div>
	<br>
	<button on:click={() => newGame()} class="newgame">New Game</button>
	
</main>
</body>

<style>
body {
	background-color: white;
}

	button {
		height: 4cm;
		width: 4cm;	
		margin: 3px;
		margin-left: 3px;
		margin-right: 3px;
		text-align: center;
		vertical-align: top;
		font-size:500%;
		border-radius: 0.5rem;

		
	}
	.X {
		background-color: #00203fff;
		color: white;
	}
	.O {
		background-color: #adefd1ff;
	}
	
	
	.message {
		font-size: 0.75cm;
		font-weight: bold;
		margin-left: 3px;

	}
	.newgame {
		height: 1cm;
		width: 4cm;	
		font-size: 100%;
		background-color: red;
		color: white;
	}
</style>