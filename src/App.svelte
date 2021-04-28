<script>
	let numero =0
	import {fade} from 'svelte/transition'
	let tulos =0
	let vanhaNumero =0
	const vanhat = []
	let kerroin = [0.3937,"in","cm"]
	let asia = kerroin[1]
	let tokaAsia = kerroin[2]
	const laske = () =>{
tulos = numero*kerroin[0]
vanhaNumero = numero
numero =0
vanhat.push(' '+vanhaNumero+ kerroin[2]+'='+parseFloat(tulos.toFixed(2))+kerroin[1])
asia = kerroin[1]
tokaAsia = kerroin[2]
	}
	const previous = () =>{
console.log(vanhat)

vanhat = vanhat
	}
</script>
<!-- vanhat taulukko näytetään koko ajan, mutta koska se on perusarvoltaan tyhjä, mitään ei näy. 
	Siihen lisätään tehdyt laskut automaatisesti laske function mukana. "näytä vanhat tulokset"
	napilla päivitetään taulukko mikä tuo tehdyt laskut näkyviin -->
<main>
	<h1>Muuntaja</h1>
	<div class="header">
		<p><button on:click="{previous}">Näytä vanhat tulokset</button></p>

		<div class="flex-container">
			{vanhat}
		</div>	
	

	</div>
	<div class="flex-container">
	<input
  type=number
  bind:value={numero}
/>
 
<!-- Jokaisella vaihtoehdolla on arvot muuntajan lukuun, mihin muutetaan ja mistä muutetaan.
	Muuntajan luku on ainoa jolla on väliä tuloksen saamiseen, mistä ja mihin ovat vain visuaalista -->
<div class="flex-container">
<select bind:value={kerroin}>
	<option value={[0.3937,"in", "cm"]}>Sentti->Tuuma</option>
	<option value={[2.54, "cm","in"]}>Tuuma->Sentti</option>
	<option value={[0.4535,"kg","lb"]}>Pauna->Kilo</option>
	<option value={[2.2046,"lb","kg"]}>Kilo->Pauna</option>
	<option value={[1.21,"€","$"]}>Euro->USD</option>
	<option value={[0.83,"$","€"]}>USD->Euro</option>
</div>
<!-- Nappi tulee näkyviin vain jos munnettava numero ei ole 0, koska nollaa on turha kertoa millään.
	Muunna nappia painamalla, lasketaan tulos, kirjataan se ylös vanhat functiota varten ja nollataan
	muunnettava numero. Tulos pyöristetään enintään kahteen desimaaliin -->
{#if numero !== 0}
<div in:fade={{delay:0}}>
<button on:click="{laske}">Muunna</button>
</div>
{/if}
<h2>
{vanhaNumero} {tokaAsia} = {parseFloat(tulos.toFixed(2))} {asia}
</h2>

</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	button:hover {
		color: rgb(20, 0, 68);
		border-color: rgb(20, 0, 68);
		background-color: rgb(214, 214, 214);
		transition: 0.5s;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>