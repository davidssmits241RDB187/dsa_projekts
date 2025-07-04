# Datu struktūras un algoritmi(1) Noslēguma projekts "League of Legends match winner probability analysis program" (LOLMWPAP)

## **Programmas funkcionalitātes apraksts**

### Programmas uzdevums
Programma 'LOLMWPAP' veic publiski pieejamo 'League of Legends (Riot Game 2009)' elektroniskā sporta turnīru maču un komandu datu analīzi un nolasa tuvāko maču komandu saturu lai noteiktu katras komandas iespējas uzvarēt vienai pret otru un publicē šo informāciju lietotājam.


### Programmas funkcionalitāte

Programmas funkcijas iedalās procesos:  
1.1. Komandu pamatdatu ieguve un saglabāšana  
1.2. Koeficentu datu ieguve un saglabāšana  
2. Lietotāja uzdevuma ievade  
2.1. Divu ievadītu komandu salīdzināšana  
2.2. Tuvāko maču 12 h laika diapazonā analīze  
2.3. Koeficentu datu izvade  
2.4. Komandu datu izvade  
2.5. Maču izvērtēšanas rezultātu reģistrācija  
2.6. Programmas aizvēršana  

### Izmantotās bibliotēkas
* dataclasses *Tiek izmantots datu sagrupēšanai klasē kurai nav nepieciešama inicializēšana bez _init_ metodes*
* os.path *Tiek izmantots failu rediģēšanai un datu saglabāšanai*
* json *Izmanto datu saglabāšanai un atkārtotai piekļuvei no python formāta uz json formātu, un apgriezti*
* requests *Izmanto lai iegūtu komandu analīzei nepieciešamos datus*
* unicodedata *Izmantots datu tipu nolasīšanas kļūmju atturēšanai un novēršanai*
* ast *Izmanto string datu tipa parsēšanai no string uz float vai int datiem*
* datetime *Izmanto lai noteiktu tuvākos mačus 12 h diapazonā*
* bs4 *Tiek izmantots lai rediģētu html lapas datus ko iegūst requets*
## **Programmas izmantošanas ceļvedis**
1. Lejupielādējiet repozitorijas zip failu, sekcijā 'Code'.
2. Veiciet 'Extract All...' operāciju uz lejupielādēto zip failu, saglabājiet personīgi skaidri pieejamā vietā.  
3. Atrodiet failu 'main', kurš ir Python Source File faila formātā un nokopējiet faila 'path'.
4. Palaižiet Windows termināli un ar komandu 'cd' + 'path' atveriet projekta path lokāciju.
5. Ar komandu python main.py palaižiet programmu.
6. Turpmākas instrukcijas tiks izsniegtas terminālī programmas palaišanas laikā.  
## Programmas struktūras un koda apraksts
Lietošanas komandas `main.py`:
<details>
<summary>0 - compare teams</summary>
<ul>
<li>Pieprasa 2 komandu ievadi
<li>Iegūst komandu objektus no DataService
<li>Izveido jaunu MatchController objektu no iegūtājām komandām
<li>Veic komandu sadalīdzināšanu
<li>Izvada iegūtos rezultātus
</ul>
</details>
<details>
<summary>1 - compare upcoming matches</summary>
<ul>
<li>Iegūst tūvākos mačus 12h laikā no DataService fetch_matches metodes
<li>Katram mačam iegūst abu komandu objektus, ja komandas neeksistē, izlaiž maču
<li>Izveido jaunu MatchController objektu no iegūtājām komandām
<li>Veic komandu sadalīdzināšanu
<li>Saglabā izvērtētos mačus ar DataService metodi log_matches
<li>Izvada iegūtos rezultātus
</ul>
</details>
<details>
<summary>2 - fetch coefficient data</summary>
<ul>
<li>Pielieto DataService fetch_coefficients metodi
<li>Tiek iegūti visi sezonā notikušie turnīri un to mači
<li>Aprēķina koeficientus katram mačam
<li>Saglabā datus failā pēc katra turnīra
</ul>
</details>
<details>
<summary>3 - fetch team data</summary>
<ul>
<li>Pielieto DataService fetch_teams metodi
<li>Tiek iegūtas visas komandas sezonā
<li>Izveido jaunu Team objektu katrai komandai
<li>Saglabā datus failā
</ul>
</details>
<details>
<summary>4 - update results</summary>
<ul>
<li>Pielieto DataService results_log un get_results metodes
<li>No data.json iegūst izvērtētos mačus
<li>Atbilstoši ievadītajiem komandu datiem, atjaunina datus failā result_logs.json
</ul>
</details>
<details>
<summary>5 - close</summary>
<ul>
<li>Aptur programmu
</ul>
</details>

<br>
Programma ir strukturizēta 3 pamatpgrupās:
<details>
<summary>classes</summary>
<ul>
<details>
<summary>team.py</summary>
<ul>Team
<ul>
<details>
<summary>atribūti</summary>
<ul>
<li>name: str = ""</li>
<li>region: str = ""</li>
<li>season: str = ""</li>
<li>winrate: str = ""</li>
<li>_winrate: float = 0.0</li>
<li>game_duration: float = 0.0</li>
<li>gold_per_minute_or_gold_lead: int = 0</li>
<li>gold_differential_per_minute: int = 0</li>
<li>gold_differential_at_15_min: int = 0</li>
<li>_winrate_at_15_min: float = 0.0</li>
<li>cspm: float = 0.0</li>
<li>cs_differential_at_15_min: int = 0</li>
<li>tower_differential_at_15_min: float = 0.0</li>
<li>avg_tower_difference: float = 0.0</li>
<li>_first_tower: float = 0.0</li>
<li>damage_per_minute: int = 0</li>
<li>_first_blood: float = 0.0</li>
<li>kills_per_game: float = 0.0</li>
<li>deaths_per_game: float = 0.0</li>
<li>avg_kd: float = 0.0</li>
<li>avg_ak: float = 0.0</li>
<li>plates_per_game: float = 0.0</li>
<li>dragons_per_game: float = 0.0</li>
<li>dragons_at_15_min: float = 0.0</li>
<li>void_grubs_per_game: float = 0.0</li>
<li>atakhan_per_game: float = 0.0</li>
<li>herald_per_game: float = 0.0</li>
<li>nashor_per_game: float = 0.0</li>
<li>_feats_of_strength: float = 0.0</li>
<li>vision_score_per_minute: float = 0.0</li>
<li>wards_per_minute: float = 0.0</li>
<li>vision_wards_per_minute: float = 0.0</li>
<li>wards_cleared_per_minute: float = 0.0</li>
<li>_wards_cleared: float = 0.0</li>
<li>top: Player | None = None</li>
<li>jungle: Player | None = None</li>
<li>mid: Player | None = None</li>
<li>bot: Player | None = None</li>
<li>support: Player | None = None</li>

</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Saglabāt lokāli iegūtos komandu datus turpmākai analīzei
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>
<ul>
<details>
<summary>add_player</summary>
<ul>
<details>
<summary>parametri</summary>
<ul>
<li>self</li>
<li>player_role:str</li>
<li>player:Player</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Secīgi pievieno iedotos Player objektus atsevišķās lomās
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
---
</details>
</ul>
</details>
</ul>
</details>
</ul>
</details>
</ul>





<ul>
<details>
<summary>player.py</summary>
<ul>Player
<ul>
<details>
<summary>atribūti</summary>
<ul>
<em>Komandas spēlētāja atsevišķie dati</em>
<li>team:str=""</li>
<li>role:str=""</li>
<li>name:str=""</li>
<li>kda:float=0.0</li>
<li>kp:float=0.0</li>
<li>vspm:float=0.0</li>
<li>dmg:float=0.0</li>
<li>gold:float=0.0</li>
<li>champions:dic=field(default_factory=dict)</li>
<li>matches_played:int:0</li>
<li>player_evaluation:float=0.0</li>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Tiek izmantots lai saglabātu spēlētāja datus
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>
<ul>
<details>
<summary>add_champion</summary>
<ul>
<details>
<summary>parametri</summary>
<ul>
<li>self</li>
<li>champion_name:str</li>
<li>matches_played:int</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Papildina <code>champions_played</code> dict <code>champion_name</code> ar asociēto maču skaitu
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
<ul>---</ul>
</details>
</ul>
</details>
</ul>
</details>
</ul>
</ul>

</ul>

<ul>

<details>
<summary>coefficients.py</summary>
<ul>Coefficients
<ul>
<details>
<summary>atribūti</summary>
<ul>
<em>Komandas statistikas koeficienti (kopā 5), visi atribūti ir saraksti, inicializēti kā [1.0,1.0]:</em>

<li>gold_per_minute_or_gold_lead</li>

<li>kills_per_game</li>

<li>avg_tower_difference</li>

<li>dragons_per_game</li>

<li>nashor_per_game</li>
<p></p>
<em> Spēlētāju specifiskie koeficienti katrai lomai (kopā 5), visi atribūti ir saraksti, inicializēti kā [1.0,1.0]: </em>
<li>_kda</li>

<li>_csm</li>

<li>_dmg</li>

<li>vspm</li>

</ul>
</details>

</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
<ul>
Tiek izmantots lai sekotu līdzi komandu un spēlētāju atsevišķu datu ietekmes līmenim mača iznākumam.
</ul>
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>
<ul>
<details>
<summary>evaluate_coefficients</summary>
<ul>
<details>
<summary>parametri</summary>
<ul>
<li>self</li>
</ul>
<ul>
<li>winning_team:Team</li>
</ul>
<ul>
<li>losing_team:Team</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
<ul>
Salīdzināt iedoto komandu datus, kuriem var izveidot koeficientus, un atjaunina koeficentus,sekojot algoritmam:
1. Higher value on winning_team -> values coefficient[0]+=1
2.Higher value on losing_team -> values coefficient[1]+=1
</ul>
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
<ul>
---
</ul>
</details>
</ul>
</details>
</ul>
</details>
</ul>
</ul>



</details>
</details>
</details>
</details>
</ul>


<details>
<summary>services</summary>
<ul>
<details>
<summary>data_service.py</summary>


<ul>Serialization
<ul>
<details>
<summary>atribūti</summary>
---
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Datu tipu pārbaude programas drošībai
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>

<ul>
<details>
<summary>@staticmethod encode_value</summary>
<ul>
<details>
<summary>parametri</summary>
<ul>
<li>x</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Convert dataclass to dict
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
x as dict or x
</details>
</ul>
</details>
</ul>

<ul>
<details>
<summary>@staticmethod get_float</summary>

<ul>
<details>
<summary>parametri</summary>
<ul>
<li>x</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Replace x as percentage to float decimal value
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
x as float
</details>
</ul>
</details>
</ul>

<ul>
<details>
<summary>@staticmethod parse_str</summary>

<ul>
<details>
<summary>parametri</summary>
<ul>
<li>s</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Converts s to automatically deduced data type
</details>
</ul>
<ul>
<details>
<summary>izvade</summary>
s
</details>
</ul>
</details>
</ul>









</details>
</ul>


DataService
<ul>
<details>
<summary>atribūti</summary>
<ul>
<li>teams</li>
<li>coefficients</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Iegūst datus un tos saglabā.
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>

<ul>
<details>
<summary>__init__</summary>
</details>
</ul>

<ul>
<details>
<summary>fetch_data</summary>
</details>
</ul>

<ul>
<details>
<summary>fetch_data_api</summary>
</details>
</ul>

<ul>
<details>
<summary>fetch_teams</summary>
</details>
</ul>

<ul>
<details>
<summary>fetch_matches</summary>
</details>
</ul>

<ul>
<details>
<summary>fetch_coefficients</summary>
</details>
</ul>

<ul>
<details>
<summary>get_team</summary>
</details>
</ul>

<ul>
<details>
<summary>get_coefficients</summary>
</details>
</ul>

</details>

</ul>






</details>

</ul>
</details>




<details>
<summary>controllers</summary>
<ul>
<details>
<summary>match_controller.py</summary>
<ul>MatchController
<ul>
<details>
<summary>atribūti</summary>
<ul>
<em>Dotie dati tiek inicializēti __init__ metodē</em>
<li>self.DS = DS</li>
<li>self.team1 = team1</li>
<li>self.team2 = team2</li>
<li>self.team1_evaluation = 0</li>
<li>self.team2_evaluation = 0</li>
<li>self.history = [0,0]</li>
</ul>
</details>
</ul>
<ul>
<details>
<summary>funkcionalitāte</summary>
Saglabā lokāli iedotās komandas datus kuras būs pretinieku pozīcijās mačā. Ar klases metodēm veic komandu analīzi un lietotājam sniedz tās rezultātus terminālī.
</details>
</ul>
<ul>
<details>
<summary>metodes</summary>
<ul>
<details>
<summary>__init__</summary>
<ul>
<details>
<summary>parametri</summary>
<li>self</li>
<li>team1:Team</li>
<li>team2:Team</li>
<li>DS:DataService</li>
</details>
</ul>

<ul>
<details>
<summary>funkcionalitāte</summary>
Inicializē MatchController objektu un pievieno iedotos parametrus objektam.
</details>
</ul>

<ul>
<details>
<summary>izvade</summary>
---
</details>
</ul>

</details>
</ul>

<ul>
<details>
<summary>dict_to_player</summary>
<ul>
<details>
<summary>parametri</summary>
<li>self</li>
<li>player_dict</li>
</details>
</ul>

<ul>
<details>
<summary>funkcionalitāte</summary>
Izvadīt Player objektu kas iegūts no iedota dict datu tipa
</details>
</ul>

<ul>
<details>
<summary>izvade</summary>
Player objekts
</details>
</ul>
</details>




<details>
<summary>evaluate_team1_vs_team2</summary>
<ul>
<details>
<summary>parametri</summary>
<li>self</li>
</details>
</ul>

<ul>
<details>
<summary>funkcionalitāte</summary>
Izveidot vērtējumu divām self saglabātām komandām, ejot cauri to pamatdatiem, salīdzinot tos un atbilstoši palielināt stiprākas komandas punktu skaitu ar koeficientu dotajam datu tipam.
</details>
</ul>

<ul>
<details>
<summary>izvade</summary>
Terminālī izprintēts punktu skaits katrai komandai
</details>
</ul>
</details>

<details>
<summary>evaluate_values</summary>
<ul>
<details>
<summary>parametri</summary>
<li>self</li>
<li>key_for_coeff</li>
<li>value_for_team1</li>
<li>value_for_team2</li>
</details>
</ul>

<ul>
<details>
<summary>funkcionalitāte</summary>
Salīdzina iedotos datus atbilstoši to veidam (1.float datu tips, 2.Player datu tips) un pievieno stiprākajai komandai punktu atbilstoši koeficentam.
</details>
</ul>

<ul>
<details>
<summary>izvade</summary>
self.team1_evaluation+=multiplier | self.team2_evaluation+=multiplier
</details>
</ul>


</details>
</ul>





</details>
</ul>
</details>
</ul>
</details>



## *Iespējamās programmas kļūmes*
* Saitu [[season](season-S15/split-Spring/tournament-ALL/), [teams_list_address](https://gol.gg/teams/list/),[teams_stats_address](https://gol.gg/teams/),[tournament_list_address](https://gol.gg/tournament/ajax.trlist.php),[tournament_address](https://gol.gg/tournament/tournament-matchlist/),[golgg_address](https://gol.gg/),[leaguepedia_address](https://lol.fandom.com/wiki/League_of_Legends_Esports_Wiki)] nobrukšana, slēgšanās ciet, datu privatizēšana, datu atrašanās vietas un etiķetes izmainīšana, kā arī datu novecošana.
* `Team` klases objektu izvērtēšanā funkcijā `evaluate_coefficients` un klasē `match_controller`, atribūts `deaths_per_game` tiek izvērtēts kā visiem citiem datiem, tas var sniegt apgrieztu punktu komandas izvērtēšanā.
* Nepareizu manuāla maču rezultātu reģistrācija var novest pie nepatiesiem datiem.
## Potenciālie programmas uzlabojumi
* `MatchController` klases `self.history` atribūta pievienošana komandu izvērtēšanas procesā.
* `Player` klases komandas biedru un pretinieku vēstures izveidošana un pievienošana `MatchController` komandu izvērtēšanas procesā.
* Tiešraides mača komandu izanalizēšana, salīdzīnot mača stāvokli ar komandu datiem, klasēs `Team` un `Player`, kā arī izveidot jaunus koeficientus klasē `Coefficients`.
* Koeficentu aprēķināšanas algoritmā iekļaut `matches_played` parametru lai noteiktu datu ietekmi.
* Jāpārveido `Team` klases `deaths_per_game` atribūta izmantošana izvērtēšanas algoritmā.
* Izveidot komandu un spēlētāju datu līmeņu sarakstus.
* Implementēt koeficientu adaptivitāti maču rezultātu `result_logs.json` datiem.
