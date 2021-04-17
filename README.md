tarea3\_ayudantia
================

## Estivaliz Rosales

## Actividad 3:

Replicar el analisis de outliers, debes elegir uno de los dos csv
disponibles (pokemon o titanic) y realizar el analisis con algunas de
las variables numericas y realizar un pequeño analisis en relacion a los
datos encontrados como outliers (en caso de que eligas el csv del
titanic solo debes evaluar las columnas AGE y FNLWGT)

## Cargar datos

Como bien sabemos, lo primero que debemos hacer es cargar los datos a
nuestro R

``` r
wd = setwd("C:/Users/JuanRosales/OneDrive/Mineria de datos/tarea 3")
pk = read.csv("pokemon.csv")
pk
```

    ##      X.                      Name   Type.1   Type.2 Total  HP Attack Defense
    ## 1     1                 Bulbasaur    Grass   Poison   318  45     49      49
    ## 2     2                   Ivysaur    Grass   Poison   405  60     62      63
    ## 3     3                  Venusaur    Grass   Poison   525  80     82      83
    ## 4     3     VenusaurMega Venusaur    Grass   Poison   625  80    100     123
    ## 5     4                Charmander     Fire            309  39     52      43
    ## 6     5                Charmeleon     Fire            405  58     64      58
    ## 7     6                 Charizard     Fire   Flying   534  78     84      78
    ## 8     6 CharizardMega Charizard X     Fire   Dragon   634  78    130     111
    ## 9     6 CharizardMega Charizard Y     Fire   Flying   634  78    104      78
    ## 10    7                  Squirtle    Water            314  44     48      65
    ## 11    8                 Wartortle    Water            405  59     63      80
    ## 12    9                 Blastoise    Water            530  79     83     100
    ## 13    9   BlastoiseMega Blastoise    Water            630  79    103     120
    ## 14   10                  Caterpie      Bug            195  45     30      35
    ## 15   11                   Metapod      Bug            205  50     20      55
    ## 16   12                Butterfree      Bug   Flying   395  60     45      50
    ## 17   13                    Weedle      Bug   Poison   195  40     35      30
    ## 18   14                    Kakuna      Bug   Poison   205  45     25      50
    ## 19   15                  Beedrill      Bug   Poison   395  65     90      40
    ## 20   15     BeedrillMega Beedrill      Bug   Poison   495  65    150      40
    ## 21   16                    Pidgey   Normal   Flying   251  40     45      40
    ## 22   17                 Pidgeotto   Normal   Flying   349  63     60      55
    ## 23   18                   Pidgeot   Normal   Flying   479  83     80      75
    ## 24   18       PidgeotMega Pidgeot   Normal   Flying   579  83     80      80
    ## 25   19                   Rattata   Normal            253  30     56      35
    ## 26   20                  Raticate   Normal            413  55     81      60
    ## 27   21                   Spearow   Normal   Flying   262  40     60      30
    ## 28   22                    Fearow   Normal   Flying   442  65     90      65
    ## 29   23                     Ekans   Poison            288  35     60      44
    ## 30   24                     Arbok   Poison            438  60     85      69
    ## 31   25                   Pikachu Electric            320  35     55      40
    ## 32   26                    Raichu Electric            485  60     90      55
    ## 33   27                 Sandshrew   Ground            300  50     75      85
    ## 34   28                 Sandslash   Ground            450  75    100     110
    ## 35   29                Nidoranâ\231\200   Poison            275  55     47      52
    ## 36   30                  Nidorina   Poison            365  70     62      67
    ## 37   31                 Nidoqueen   Poison   Ground   505  90     92      87
    ## 38   32                Nidoranâ\231‚   Poison            273  46     57      40
    ## 39   33                  Nidorino   Poison            365  61     72      57
    ## 40   34                  Nidoking   Poison   Ground   505  81    102      77
    ## 41   35                  Clefairy    Fairy            323  70     45      48
    ## 42   36                  Clefable    Fairy            483  95     70      73
    ## 43   37                    Vulpix     Fire            299  38     41      40
    ## 44   38                 Ninetales     Fire            505  73     76      75
    ## 45   39                Jigglypuff   Normal    Fairy   270 115     45      20
    ## 46   40                Wigglytuff   Normal    Fairy   435 140     70      45
    ## 47   41                     Zubat   Poison   Flying   245  40     45      35
    ## 48   42                    Golbat   Poison   Flying   455  75     80      70
    ## 49   43                    Oddish    Grass   Poison   320  45     50      55
    ## 50   44                     Gloom    Grass   Poison   395  60     65      70
    ## 51   45                 Vileplume    Grass   Poison   490  75     80      85
    ## 52   46                     Paras      Bug    Grass   285  35     70      55
    ## 53   47                  Parasect      Bug    Grass   405  60     95      80
    ## 54   48                   Venonat      Bug   Poison   305  60     55      50
    ## 55   49                  Venomoth      Bug   Poison   450  70     65      60
    ## 56   50                   Diglett   Ground            265  10     55      25
    ## 57   51                   Dugtrio   Ground            405  35     80      50
    ## 58   52                    Meowth   Normal            290  40     45      35
    ## 59   53                   Persian   Normal            440  65     70      60
    ## 60   54                   Psyduck    Water            320  50     52      48
    ## 61   55                   Golduck    Water            500  80     82      78
    ## 62   56                    Mankey Fighting            305  40     80      35
    ## 63   57                  Primeape Fighting            455  65    105      60
    ## 64   58                 Growlithe     Fire            350  55     70      45
    ## 65   59                  Arcanine     Fire            555  90    110      80
    ## 66   60                   Poliwag    Water            300  40     50      40
    ## 67   61                 Poliwhirl    Water            385  65     65      65
    ## 68   62                 Poliwrath    Water Fighting   510  90     95      95
    ## 69   63                      Abra  Psychic            310  25     20      15
    ## 70   64                   Kadabra  Psychic            400  40     35      30
    ## 71   65                  Alakazam  Psychic            500  55     50      45
    ## 72   65     AlakazamMega Alakazam  Psychic            590  55     50      65
    ## 73   66                    Machop Fighting            305  70     80      50
    ## 74   67                   Machoke Fighting            405  80    100      70
    ## 75   68                   Machamp Fighting            505  90    130      80
    ## 76   69                Bellsprout    Grass   Poison   300  50     75      35
    ## 77   70                Weepinbell    Grass   Poison   390  65     90      50
    ## 78   71                Victreebel    Grass   Poison   490  80    105      65
    ## 79   72                 Tentacool    Water   Poison   335  40     40      35
    ## 80   73                Tentacruel    Water   Poison   515  80     70      65
    ## 81   74                   Geodude     Rock   Ground   300  40     80     100
    ## 82   75                  Graveler     Rock   Ground   390  55     95     115
    ## 83   76                     Golem     Rock   Ground   495  80    120     130
    ## 84   77                    Ponyta     Fire            410  50     85      55
    ## 85   78                  Rapidash     Fire            500  65    100      70
    ## 86   79                  Slowpoke    Water  Psychic   315  90     65      65
    ## 87   80                   Slowbro    Water  Psychic   490  95     75     110
    ## 88   80       SlowbroMega Slowbro    Water  Psychic   590  95     75     180
    ## 89   81                 Magnemite Electric    Steel   325  25     35      70
    ## 90   82                  Magneton Electric    Steel   465  50     60      95
    ## 91   83                Farfetch'd   Normal   Flying   352  52     65      55
    ## 92   84                     Doduo   Normal   Flying   310  35     85      45
    ## 93   85                    Dodrio   Normal   Flying   460  60    110      70
    ## 94   86                      Seel    Water            325  65     45      55
    ## 95   87                   Dewgong    Water      Ice   475  90     70      80
    ## 96   88                    Grimer   Poison            325  80     80      50
    ## 97   89                       Muk   Poison            500 105    105      75
    ## 98   90                  Shellder    Water            305  30     65     100
    ## 99   91                  Cloyster    Water      Ice   525  50     95     180
    ## 100  92                    Gastly    Ghost   Poison   310  30     35      30
    ## 101  93                   Haunter    Ghost   Poison   405  45     50      45
    ## 102  94                    Gengar    Ghost   Poison   500  60     65      60
    ## 103  94         GengarMega Gengar    Ghost   Poison   600  60     65      80
    ## 104  95                      Onix     Rock   Ground   385  35     45     160
    ## 105  96                   Drowzee  Psychic            328  60     48      45
    ## 106  97                     Hypno  Psychic            483  85     73      70
    ## 107  98                    Krabby    Water            325  30    105      90
    ## 108  99                   Kingler    Water            475  55    130     115
    ## 109 100                   Voltorb Electric            330  40     30      50
    ## 110 101                 Electrode Electric            480  60     50      70
    ## 111 102                 Exeggcute    Grass  Psychic   325  60     40      80
    ## 112 103                 Exeggutor    Grass  Psychic   520  95     95      85
    ## 113 104                    Cubone   Ground            320  50     50      95
    ## 114 105                   Marowak   Ground            425  60     80     110
    ## 115 106                 Hitmonlee Fighting            455  50    120      53
    ## 116 107                Hitmonchan Fighting            455  50    105      79
    ## 117 108                 Lickitung   Normal            385  90     55      75
    ## 118 109                   Koffing   Poison            340  40     65      95
    ## 119 110                   Weezing   Poison            490  65     90     120
    ## 120 111                   Rhyhorn   Ground     Rock   345  80     85      95
    ## 121 112                    Rhydon   Ground     Rock   485 105    130     120
    ## 122 113                   Chansey   Normal            450 250      5       5
    ## 123 114                   Tangela    Grass            435  65     55     115
    ## 124 115                Kangaskhan   Normal            490 105     95      80
    ## 125 115 KangaskhanMega Kangaskhan   Normal            590 105    125     100
    ## 126 116                    Horsea    Water            295  30     40      70
    ## 127 117                    Seadra    Water            440  55     65      95
    ## 128 118                   Goldeen    Water            320  45     67      60
    ## 129 119                   Seaking    Water            450  80     92      65
    ## 130 120                    Staryu    Water            340  30     45      55
    ## 131 121                   Starmie    Water  Psychic   520  60     75      85
    ## 132 122                  Mr. Mime  Psychic    Fairy   460  40     45      65
    ## 133 123                   Scyther      Bug   Flying   500  70    110      80
    ## 134 124                      Jynx      Ice  Psychic   455  65     50      35
    ## 135 125                Electabuzz Electric            490  65     83      57
    ## 136 126                    Magmar     Fire            495  65     95      57
    ## 137 127                    Pinsir      Bug            500  65    125     100
    ## 138 127         PinsirMega Pinsir      Bug   Flying   600  65    155     120
    ## 139 128                    Tauros   Normal            490  75    100      95
    ## 140 129                  Magikarp    Water            200  20     10      55
    ## 141 130                  Gyarados    Water   Flying   540  95    125      79
    ## 142 130     GyaradosMega Gyarados    Water     Dark   640  95    155     109
    ## 143 131                    Lapras    Water      Ice   535 130     85      80
    ## 144 132                     Ditto   Normal            288  48     48      48
    ## 145 133                     Eevee   Normal            325  55     55      50
    ## 146 134                  Vaporeon    Water            525 130     65      60
    ## 147 135                   Jolteon Electric            525  65     65      60
    ## 148 136                   Flareon     Fire            525  65    130      60
    ## 149 137                   Porygon   Normal            395  65     60      70
    ## 150 138                   Omanyte     Rock    Water   355  35     40     100
    ## 151 139                   Omastar     Rock    Water   495  70     60     125
    ## 152 140                    Kabuto     Rock    Water   355  30     80      90
    ## 153 141                  Kabutops     Rock    Water   495  60    115     105
    ## 154 142                Aerodactyl     Rock   Flying   515  80    105      65
    ## 155 142 AerodactylMega Aerodactyl     Rock   Flying   615  80    135      85
    ## 156 143                   Snorlax   Normal            540 160    110      65
    ## 157 144                  Articuno      Ice   Flying   580  90     85     100
    ## 158 145                    Zapdos Electric   Flying   580  90     90      85
    ## 159 146                   Moltres     Fire   Flying   580  90    100      90
    ## 160 147                   Dratini   Dragon            300  41     64      45
    ## 161 148                 Dragonair   Dragon            420  61     84      65
    ## 162 149                 Dragonite   Dragon   Flying   600  91    134      95
    ## 163 150                    Mewtwo  Psychic            680 106    110      90
    ## 164 150       MewtwoMega Mewtwo X  Psychic Fighting   780 106    190     100
    ## 165 150       MewtwoMega Mewtwo Y  Psychic            780 106    150      70
    ## 166 151                       Mew  Psychic            600 100    100     100
    ## 167 152                 Chikorita    Grass            318  45     49      65
    ## 168 153                   Bayleef    Grass            405  60     62      80
    ## 169 154                  Meganium    Grass            525  80     82     100
    ## 170 155                 Cyndaquil     Fire            309  39     52      43
    ## 171 156                   Quilava     Fire            405  58     64      58
    ## 172 157                Typhlosion     Fire            534  78     84      78
    ## 173 158                  Totodile    Water            314  50     65      64
    ## 174 159                  Croconaw    Water            405  65     80      80
    ## 175 160                Feraligatr    Water            530  85    105     100
    ## 176 161                   Sentret   Normal            215  35     46      34
    ## 177 162                    Furret   Normal            415  85     76      64
    ## 178 163                  Hoothoot   Normal   Flying   262  60     30      30
    ## 179 164                   Noctowl   Normal   Flying   442 100     50      50
    ## 180 165                    Ledyba      Bug   Flying   265  40     20      30
    ## 181 166                    Ledian      Bug   Flying   390  55     35      50
    ## 182 167                  Spinarak      Bug   Poison   250  40     60      40
    ## 183 168                   Ariados      Bug   Poison   390  70     90      70
    ## 184 169                    Crobat   Poison   Flying   535  85     90      80
    ## 185 170                  Chinchou    Water Electric   330  75     38      38
    ## 186 171                   Lanturn    Water Electric   460 125     58      58
    ## 187 172                     Pichu Electric            205  20     40      15
    ## 188 173                    Cleffa    Fairy            218  50     25      28
    ## 189 174                 Igglybuff   Normal    Fairy   210  90     30      15
    ## 190 175                    Togepi    Fairy            245  35     20      65
    ## 191 176                   Togetic    Fairy   Flying   405  55     40      85
    ## 192 177                      Natu  Psychic   Flying   320  40     50      45
    ## 193 178                      Xatu  Psychic   Flying   470  65     75      70
    ## 194 179                    Mareep Electric            280  55     40      40
    ## 195 180                   Flaaffy Electric            365  70     55      55
    ## 196 181                  Ampharos Electric            510  90     75      85
    ## 197 181     AmpharosMega Ampharos Electric   Dragon   610  90     95     105
    ## 198 182                 Bellossom    Grass            490  75     80      95
    ## 199 183                    Marill    Water    Fairy   250  70     20      50
    ## 200 184                 Azumarill    Water    Fairy   420 100     50      80
    ## 201 185                 Sudowoodo     Rock            410  70    100     115
    ## 202 186                  Politoed    Water            500  90     75      75
    ## 203 187                    Hoppip    Grass   Flying   250  35     35      40
    ## 204 188                  Skiploom    Grass   Flying   340  55     45      50
    ## 205 189                  Jumpluff    Grass   Flying   460  75     55      70
    ## 206 190                     Aipom   Normal            360  55     70      55
    ## 207 191                   Sunkern    Grass            180  30     30      30
    ## 208 192                  Sunflora    Grass            425  75     75      55
    ## 209 193                     Yanma      Bug   Flying   390  65     65      45
    ## 210 194                    Wooper    Water   Ground   210  55     45      45
    ## 211 195                  Quagsire    Water   Ground   430  95     85      85
    ## 212 196                    Espeon  Psychic            525  65     65      60
    ## 213 197                   Umbreon     Dark            525  95     65     110
    ## 214 198                   Murkrow     Dark   Flying   405  60     85      42
    ## 215 199                  Slowking    Water  Psychic   490  95     75      80
    ## 216 200                Misdreavus    Ghost            435  60     60      60
    ## 217 201                     Unown  Psychic            336  48     72      48
    ## 218 202                 Wobbuffet  Psychic            405 190     33      58
    ## 219 203                 Girafarig   Normal  Psychic   455  70     80      65
    ## 220 204                    Pineco      Bug            290  50     65      90
    ## 221 205                Forretress      Bug    Steel   465  75     90     140
    ## 222 206                 Dunsparce   Normal            415 100     70      70
    ## 223 207                    Gligar   Ground   Flying   430  65     75     105
    ## 224 208                   Steelix    Steel   Ground   510  75     85     200
    ## 225 208       SteelixMega Steelix    Steel   Ground   610  75    125     230
    ## 226 209                  Snubbull    Fairy            300  60     80      50
    ## 227 210                  Granbull    Fairy            450  90    120      75
    ## 228 211                  Qwilfish    Water   Poison   430  65     95      75
    ## 229 212                    Scizor      Bug    Steel   500  70    130     100
    ## 230 212         ScizorMega Scizor      Bug    Steel   600  70    150     140
    ## 231 213                   Shuckle      Bug     Rock   505  20     10     230
    ## 232 214                 Heracross      Bug Fighting   500  80    125      75
    ## 233 214   HeracrossMega Heracross      Bug Fighting   600  80    185     115
    ## 234 215                   Sneasel     Dark      Ice   430  55     95      55
    ## 235 216                 Teddiursa   Normal            330  60     80      50
    ## 236 217                  Ursaring   Normal            500  90    130      75
    ## 237 218                    Slugma     Fire            250  40     40      40
    ## 238 219                  Magcargo     Fire     Rock   410  50     50     120
    ## 239 220                    Swinub      Ice   Ground   250  50     50      40
    ## 240 221                 Piloswine      Ice   Ground   450 100    100      80
    ## 241 222                   Corsola    Water     Rock   380  55     55      85
    ## 242 223                  Remoraid    Water            300  35     65      35
    ## 243 224                 Octillery    Water            480  75    105      75
    ## 244 225                  Delibird      Ice   Flying   330  45     55      45
    ## 245 226                   Mantine    Water   Flying   465  65     40      70
    ## 246 227                  Skarmory    Steel   Flying   465  65     80     140
    ## 247 228                  Houndour     Dark     Fire   330  45     60      30
    ## 248 229                  Houndoom     Dark     Fire   500  75     90      50
    ## 249 229     HoundoomMega Houndoom     Dark     Fire   600  75     90      90
    ## 250 230                   Kingdra    Water   Dragon   540  75     95      95
    ## 251 231                    Phanpy   Ground            330  90     60      60
    ## 252 232                   Donphan   Ground            500  90    120     120
    ## 253 233                  Porygon2   Normal            515  85     80      90
    ## 254 234                  Stantler   Normal            465  73     95      62
    ## 255 235                  Smeargle   Normal            250  55     20      35
    ## 256 236                   Tyrogue Fighting            210  35     35      35
    ## 257 237                 Hitmontop Fighting            455  50     95      95
    ## 258 238                  Smoochum      Ice  Psychic   305  45     30      15
    ## 259 239                    Elekid Electric            360  45     63      37
    ## 260 240                     Magby     Fire            365  45     75      37
    ## 261 241                   Miltank   Normal            490  95     80     105
    ## 262 242                   Blissey   Normal            540 255     10      10
    ## 263 243                    Raikou Electric            580  90     85      75
    ## 264 244                     Entei     Fire            580 115    115      85
    ## 265 245                   Suicune    Water            580 100     75     115
    ## 266 246                  Larvitar     Rock   Ground   300  50     64      50
    ## 267 247                   Pupitar     Rock   Ground   410  70     84      70
    ## 268 248                 Tyranitar     Rock     Dark   600 100    134     110
    ## 269 248   TyranitarMega Tyranitar     Rock     Dark   700 100    164     150
    ## 270 249                     Lugia  Psychic   Flying   680 106     90     130
    ## 271 250                     Ho-oh     Fire   Flying   680 106    130      90
    ## 272 251                    Celebi  Psychic    Grass   600 100    100     100
    ## 273 252                   Treecko    Grass            310  40     45      35
    ## 274 253                   Grovyle    Grass            405  50     65      45
    ## 275 254                  Sceptile    Grass            530  70     85      65
    ## 276 254     SceptileMega Sceptile    Grass   Dragon   630  70    110      75
    ## 277 255                   Torchic     Fire            310  45     60      40
    ## 278 256                 Combusken     Fire Fighting   405  60     85      60
    ## 279 257                  Blaziken     Fire Fighting   530  80    120      70
    ## 280 257     BlazikenMega Blaziken     Fire Fighting   630  80    160      80
    ## 281 258                    Mudkip    Water            310  50     70      50
    ## 282 259                 Marshtomp    Water   Ground   405  70     85      70
    ## 283 260                  Swampert    Water   Ground   535 100    110      90
    ## 284 260     SwampertMega Swampert    Water   Ground   635 100    150     110
    ## 285 261                 Poochyena     Dark            220  35     55      35
    ## 286 262                 Mightyena     Dark            420  70     90      70
    ## 287 263                 Zigzagoon   Normal            240  38     30      41
    ## 288 264                   Linoone   Normal            420  78     70      61
    ## 289 265                   Wurmple      Bug            195  45     45      35
    ## 290 266                   Silcoon      Bug            205  50     35      55
    ## 291 267                 Beautifly      Bug   Flying   395  60     70      50
    ## 292 268                   Cascoon      Bug            205  50     35      55
    ## 293 269                    Dustox      Bug   Poison   385  60     50      70
    ## 294 270                     Lotad    Water    Grass   220  40     30      30
    ## 295 271                    Lombre    Water    Grass   340  60     50      50
    ## 296 272                  Ludicolo    Water    Grass   480  80     70      70
    ## 297 273                    Seedot    Grass            220  40     40      50
    ## 298 274                   Nuzleaf    Grass     Dark   340  70     70      40
    ## 299 275                   Shiftry    Grass     Dark   480  90    100      60
    ## 300 276                   Taillow   Normal   Flying   270  40     55      30
    ## 301 277                   Swellow   Normal   Flying   430  60     85      60
    ## 302 278                   Wingull    Water   Flying   270  40     30      30
    ## 303 279                  Pelipper    Water   Flying   430  60     50     100
    ## 304 280                     Ralts  Psychic    Fairy   198  28     25      25
    ## 305 281                    Kirlia  Psychic    Fairy   278  38     35      35
    ## 306 282                 Gardevoir  Psychic    Fairy   518  68     65      65
    ## 307 282   GardevoirMega Gardevoir  Psychic    Fairy   618  68     85      65
    ## 308 283                   Surskit      Bug    Water   269  40     30      32
    ## 309 284                Masquerain      Bug   Flying   414  70     60      62
    ## 310 285                 Shroomish    Grass            295  60     40      60
    ## 311 286                   Breloom    Grass Fighting   460  60    130      80
    ## 312 287                   Slakoth   Normal            280  60     60      60
    ## 313 288                  Vigoroth   Normal            440  80     80      80
    ## 314 289                   Slaking   Normal            670 150    160     100
    ## 315 290                   Nincada      Bug   Ground   266  31     45      90
    ## 316 291                   Ninjask      Bug   Flying   456  61     90      45
    ## 317 292                  Shedinja      Bug    Ghost   236   1     90      45
    ## 318 293                   Whismur   Normal            240  64     51      23
    ## 319 294                   Loudred   Normal            360  84     71      43
    ## 320 295                   Exploud   Normal            490 104     91      63
    ## 321 296                  Makuhita Fighting            237  72     60      30
    ## 322 297                  Hariyama Fighting            474 144    120      60
    ## 323 298                   Azurill   Normal    Fairy   190  50     20      40
    ## 324 299                  Nosepass     Rock            375  30     45     135
    ## 325 300                    Skitty   Normal            260  50     45      45
    ## 326 301                  Delcatty   Normal            380  70     65      65
    ## 327 302                   Sableye     Dark    Ghost   380  50     75      75
    ## 328 302       SableyeMega Sableye     Dark    Ghost   480  50     85     125
    ## 329 303                    Mawile    Steel    Fairy   380  50     85      85
    ## 330 303         MawileMega Mawile    Steel    Fairy   480  50    105     125
    ## 331 304                      Aron    Steel     Rock   330  50     70     100
    ## 332 305                    Lairon    Steel     Rock   430  60     90     140
    ## 333 306                    Aggron    Steel     Rock   530  70    110     180
    ## 334 306         AggronMega Aggron    Steel            630  70    140     230
    ## 335 307                  Meditite Fighting  Psychic   280  30     40      55
    ## 336 308                  Medicham Fighting  Psychic   410  60     60      75
    ## 337 308     MedichamMega Medicham Fighting  Psychic   510  60    100      85
    ## 338 309                 Electrike Electric            295  40     45      40
    ## 339 310                 Manectric Electric            475  70     75      60
    ## 340 310   ManectricMega Manectric Electric            575  70     75      80
    ## 341 311                    Plusle Electric            405  60     50      40
    ## 342 312                     Minun Electric            405  60     40      50
    ## 343 313                   Volbeat      Bug            400  65     73      55
    ## 344 314                  Illumise      Bug            400  65     47      55
    ## 345 315                   Roselia    Grass   Poison   400  50     60      45
    ## 346 316                    Gulpin   Poison            302  70     43      53
    ## 347 317                    Swalot   Poison            467 100     73      83
    ## 348 318                  Carvanha    Water     Dark   305  45     90      20
    ## 349 319                  Sharpedo    Water     Dark   460  70    120      40
    ## 350 319     SharpedoMega Sharpedo    Water     Dark   560  70    140      70
    ## 351 320                   Wailmer    Water            400 130     70      35
    ## 352 321                   Wailord    Water            500 170     90      45
    ## 353 322                     Numel     Fire   Ground   305  60     60      40
    ## 354 323                  Camerupt     Fire   Ground   460  70    100      70
    ## 355 323     CameruptMega Camerupt     Fire   Ground   560  70    120     100
    ## 356 324                   Torkoal     Fire            470  70     85     140
    ## 357 325                    Spoink  Psychic            330  60     25      35
    ## 358 326                   Grumpig  Psychic            470  80     45      65
    ## 359 327                    Spinda   Normal            360  60     60      60
    ## 360 328                  Trapinch   Ground            290  45    100      45
    ## 361 329                   Vibrava   Ground   Dragon   340  50     70      50
    ## 362 330                    Flygon   Ground   Dragon   520  80    100      80
    ## 363 331                    Cacnea    Grass            335  50     85      40
    ## 364 332                  Cacturne    Grass     Dark   475  70    115      60
    ## 365 333                    Swablu   Normal   Flying   310  45     40      60
    ## 366 334                   Altaria   Dragon   Flying   490  75     70      90
    ## 367 334       AltariaMega Altaria   Dragon    Fairy   590  75    110     110
    ## 368 335                  Zangoose   Normal            458  73    115      60
    ## 369 336                   Seviper   Poison            458  73    100      60
    ## 370 337                  Lunatone     Rock  Psychic   440  70     55      65
    ## 371 338                   Solrock     Rock  Psychic   440  70     95      85
    ## 372 339                  Barboach    Water   Ground   288  50     48      43
    ## 373 340                  Whiscash    Water   Ground   468 110     78      73
    ## 374 341                  Corphish    Water            308  43     80      65
    ## 375 342                 Crawdaunt    Water     Dark   468  63    120      85
    ## 376 343                    Baltoy   Ground  Psychic   300  40     40      55
    ## 377 344                   Claydol   Ground  Psychic   500  60     70     105
    ## 378 345                    Lileep     Rock    Grass   355  66     41      77
    ## 379 346                   Cradily     Rock    Grass   495  86     81      97
    ## 380 347                   Anorith     Rock      Bug   355  45     95      50
    ## 381 348                   Armaldo     Rock      Bug   495  75    125     100
    ## 382 349                    Feebas    Water            200  20     15      20
    ## 383 350                   Milotic    Water            540  95     60      79
    ## 384 351                  Castform   Normal            420  70     70      70
    ## 385 352                   Kecleon   Normal            440  60     90      70
    ## 386 353                   Shuppet    Ghost            295  44     75      35
    ## 387 354                   Banette    Ghost            455  64    115      65
    ## 388 354       BanetteMega Banette    Ghost            555  64    165      75
    ## 389 355                   Duskull    Ghost            295  20     40      90
    ## 390 356                  Dusclops    Ghost            455  40     70     130
    ## 391 357                   Tropius    Grass   Flying   460  99     68      83
    ## 392 358                  Chimecho  Psychic            425  65     50      70
    ## 393 359                     Absol     Dark            465  65    130      60
    ## 394 359           AbsolMega Absol     Dark            565  65    150      60
    ## 395 360                    Wynaut  Psychic            260  95     23      48
    ## 396 361                   Snorunt      Ice            300  50     50      50
    ## 397 362                    Glalie      Ice            480  80     80      80
    ## 398 362         GlalieMega Glalie      Ice            580  80    120      80
    ## 399 363                    Spheal      Ice    Water   290  70     40      50
    ## 400 364                    Sealeo      Ice    Water   410  90     60      70
    ## 401 365                   Walrein      Ice    Water   530 110     80      90
    ## 402 366                  Clamperl    Water            345  35     64      85
    ## 403 367                   Huntail    Water            485  55    104     105
    ## 404 368                  Gorebyss    Water            485  55     84     105
    ## 405 369                 Relicanth    Water     Rock   485 100     90     130
    ## 406 370                   Luvdisc    Water            330  43     30      55
    ## 407 371                     Bagon   Dragon            300  45     75      60
    ## 408 372                   Shelgon   Dragon            420  65     95     100
    ## 409 373                 Salamence   Dragon   Flying   600  95    135      80
    ## 410 373   SalamenceMega Salamence   Dragon   Flying   700  95    145     130
    ## 411 374                    Beldum    Steel  Psychic   300  40     55      80
    ## 412 375                    Metang    Steel  Psychic   420  60     75     100
    ## 413 376                 Metagross    Steel  Psychic   600  80    135     130
    ## 414 376   MetagrossMega Metagross    Steel  Psychic   700  80    145     150
    ## 415 377                  Regirock     Rock            580  80    100     200
    ## 416 378                    Regice      Ice            580  80     50     100
    ## 417 379                 Registeel    Steel            580  80     75     150
    ## 418 380                    Latias   Dragon  Psychic   600  80     80      90
    ## 419 380         LatiasMega Latias   Dragon  Psychic   700  80    100     120
    ## 420 381                    Latios   Dragon  Psychic   600  80     90      80
    ## 421 381         LatiosMega Latios   Dragon  Psychic   700  80    130     100
    ## 422 382                    Kyogre    Water            670 100    100      90
    ## 423 382       KyogrePrimal Kyogre    Water            770 100    150      90
    ## 424 383                   Groudon   Ground            670 100    150     140
    ## 425 383     GroudonPrimal Groudon   Ground     Fire   770 100    180     160
    ## 426 384                  Rayquaza   Dragon   Flying   680 105    150      90
    ## 427 384     RayquazaMega Rayquaza   Dragon   Flying   780 105    180     100
    ## 428 385                   Jirachi    Steel  Psychic   600 100    100     100
    ## 429 386        DeoxysNormal Forme  Psychic            600  50    150      50
    ## 430 386        DeoxysAttack Forme  Psychic            600  50    180      20
    ## 431 386       DeoxysDefense Forme  Psychic            600  50     70     160
    ## 432 386         DeoxysSpeed Forme  Psychic            600  50     95      90
    ## 433 387                   Turtwig    Grass            318  55     68      64
    ## 434 388                    Grotle    Grass            405  75     89      85
    ## 435 389                  Torterra    Grass   Ground   525  95    109     105
    ## 436 390                  Chimchar     Fire            309  44     58      44
    ## 437 391                  Monferno     Fire Fighting   405  64     78      52
    ## 438 392                 Infernape     Fire Fighting   534  76    104      71
    ## 439 393                    Piplup    Water            314  53     51      53
    ## 440 394                  Prinplup    Water            405  64     66      68
    ## 441 395                  Empoleon    Water    Steel   530  84     86      88
    ## 442 396                    Starly   Normal   Flying   245  40     55      30
    ## 443 397                  Staravia   Normal   Flying   340  55     75      50
    ## 444 398                 Staraptor   Normal   Flying   485  85    120      70
    ## 445 399                    Bidoof   Normal            250  59     45      40
    ## 446 400                   Bibarel   Normal    Water   410  79     85      60
    ## 447 401                 Kricketot      Bug            194  37     25      41
    ## 448 402                Kricketune      Bug            384  77     85      51
    ## 449 403                     Shinx Electric            263  45     65      34
    ## 450 404                     Luxio Electric            363  60     85      49
    ## 451 405                    Luxray Electric            523  80    120      79
    ## 452 406                     Budew    Grass   Poison   280  40     30      35
    ## 453 407                  Roserade    Grass   Poison   515  60     70      65
    ## 454 408                  Cranidos     Rock            350  67    125      40
    ## 455 409                 Rampardos     Rock            495  97    165      60
    ## 456 410                  Shieldon     Rock    Steel   350  30     42     118
    ## 457 411                 Bastiodon     Rock    Steel   495  60     52     168
    ## 458 412                     Burmy      Bug            224  40     29      45
    ## 459 413       WormadamPlant Cloak      Bug    Grass   424  60     59      85
    ## 460 413       WormadamSandy Cloak      Bug   Ground   424  60     79     105
    ## 461 413       WormadamTrash Cloak      Bug    Steel   424  60     69      95
    ## 462 414                    Mothim      Bug   Flying   424  70     94      50
    ## 463 415                    Combee      Bug   Flying   244  30     30      42
    ## 464 416                 Vespiquen      Bug   Flying   474  70     80     102
    ## 465 417                 Pachirisu Electric            405  60     45      70
    ## 466 418                    Buizel    Water            330  55     65      35
    ## 467 419                  Floatzel    Water            495  85    105      55
    ## 468 420                   Cherubi    Grass            275  45     35      45
    ## 469 421                   Cherrim    Grass            450  70     60      70
    ## 470 422                   Shellos    Water            325  76     48      48
    ## 471 423                 Gastrodon    Water   Ground   475 111     83      68
    ## 472 424                   Ambipom   Normal            482  75    100      66
    ## 473 425                  Drifloon    Ghost   Flying   348  90     50      34
    ## 474 426                  Drifblim    Ghost   Flying   498 150     80      44
    ## 475 427                   Buneary   Normal            350  55     66      44
    ## 476 428                   Lopunny   Normal            480  65     76      84
    ## 477 428       LopunnyMega Lopunny   Normal Fighting   580  65    136      94
    ## 478 429                 Mismagius    Ghost            495  60     60      60
    ## 479 430                 Honchkrow     Dark   Flying   505 100    125      52
    ## 480 431                   Glameow   Normal            310  49     55      42
    ## 481 432                   Purugly   Normal            452  71     82      64
    ## 482 433                 Chingling  Psychic            285  45     30      50
    ## 483 434                    Stunky   Poison     Dark   329  63     63      47
    ## 484 435                  Skuntank   Poison     Dark   479 103     93      67
    ## 485 436                   Bronzor    Steel  Psychic   300  57     24      86
    ## 486 437                  Bronzong    Steel  Psychic   500  67     89     116
    ## 487 438                    Bonsly     Rock            290  50     80      95
    ## 488 439                  Mime Jr.  Psychic    Fairy   310  20     25      45
    ## 489 440                   Happiny   Normal            220 100      5       5
    ## 490 441                    Chatot   Normal   Flying   411  76     65      45
    ## 491 442                 Spiritomb    Ghost     Dark   485  50     92     108
    ## 492 443                     Gible   Dragon   Ground   300  58     70      45
    ## 493 444                    Gabite   Dragon   Ground   410  68     90      65
    ## 494 445                  Garchomp   Dragon   Ground   600 108    130      95
    ## 495 445     GarchompMega Garchomp   Dragon   Ground   700 108    170     115
    ## 496 446                  Munchlax   Normal            390 135     85      40
    ## 497 447                     Riolu Fighting            285  40     70      40
    ## 498 448                   Lucario Fighting    Steel   525  70    110      70
    ## 499 448       LucarioMega Lucario Fighting    Steel   625  70    145      88
    ## 500 449                Hippopotas   Ground            330  68     72      78
    ## 501 450                 Hippowdon   Ground            525 108    112     118
    ## 502 451                   Skorupi   Poison      Bug   330  40     50      90
    ## 503 452                   Drapion   Poison     Dark   500  70     90     110
    ## 504 453                  Croagunk   Poison Fighting   300  48     61      40
    ## 505 454                 Toxicroak   Poison Fighting   490  83    106      65
    ## 506 455                 Carnivine    Grass            454  74    100      72
    ## 507 456                   Finneon    Water            330  49     49      56
    ## 508 457                  Lumineon    Water            460  69     69      76
    ## 509 458                   Mantyke    Water   Flying   345  45     20      50
    ## 510 459                    Snover    Grass      Ice   334  60     62      50
    ## 511 460                 Abomasnow    Grass      Ice   494  90     92      75
    ## 512 460   AbomasnowMega Abomasnow    Grass      Ice   594  90    132     105
    ## 513 461                   Weavile     Dark      Ice   510  70    120      65
    ## 514 462                 Magnezone Electric    Steel   535  70     70     115
    ## 515 463                Lickilicky   Normal            515 110     85      95
    ## 516 464                 Rhyperior   Ground     Rock   535 115    140     130
    ## 517 465                 Tangrowth    Grass            535 100    100     125
    ## 518 466                Electivire Electric            540  75    123      67
    ## 519 467                 Magmortar     Fire            540  75     95      67
    ## 520 468                  Togekiss    Fairy   Flying   545  85     50      95
    ## 521 469                   Yanmega      Bug   Flying   515  86     76      86
    ## 522 470                   Leafeon    Grass            525  65    110     130
    ## 523 471                   Glaceon      Ice            525  65     60     110
    ## 524 472                   Gliscor   Ground   Flying   510  75     95     125
    ## 525 473                 Mamoswine      Ice   Ground   530 110    130      80
    ## 526 474                 Porygon-Z   Normal            535  85     80      70
    ## 527 475                   Gallade  Psychic Fighting   518  68    125      65
    ## 528 475       GalladeMega Gallade  Psychic Fighting   618  68    165      95
    ## 529 476                 Probopass     Rock    Steel   525  60     55     145
    ## 530 477                  Dusknoir    Ghost            525  45    100     135
    ## 531 478                  Froslass      Ice    Ghost   480  70     80      70
    ## 532 479                     Rotom Electric    Ghost   440  50     50      77
    ## 533 479           RotomHeat Rotom Electric     Fire   520  50     65     107
    ## 534 479           RotomWash Rotom Electric    Water   520  50     65     107
    ## 535 479          RotomFrost Rotom Electric      Ice   520  50     65     107
    ## 536 479            RotomFan Rotom Electric   Flying   520  50     65     107
    ## 537 479            RotomMow Rotom Electric    Grass   520  50     65     107
    ## 538 480                      Uxie  Psychic            580  75     75     130
    ## 539 481                   Mesprit  Psychic            580  80    105     105
    ## 540 482                     Azelf  Psychic            580  75    125      70
    ## 541 483                    Dialga    Steel   Dragon   680 100    120     120
    ## 542 484                    Palkia    Water   Dragon   680  90    120     100
    ## 543 485                   Heatran     Fire    Steel   600  91     90     106
    ## 544 486                 Regigigas   Normal            670 110    160     110
    ## 545 487     GiratinaAltered Forme    Ghost   Dragon   680 150    100     120
    ## 546 487      GiratinaOrigin Forme    Ghost   Dragon   680 150    120     100
    ## 547 488                 Cresselia  Psychic            600 120     70     120
    ## 548 489                    Phione    Water            480  80     80      80
    ## 549 490                   Manaphy    Water            600 100    100     100
    ## 550 491                   Darkrai     Dark            600  70     90      90
    ## 551 492         ShayminLand Forme    Grass            600 100    100     100
    ## 552 492          ShayminSky Forme    Grass   Flying   600 100    103      75
    ## 553 493                    Arceus   Normal            720 120    120     120
    ## 554 494                   Victini  Psychic     Fire   600 100    100     100
    ## 555 495                     Snivy    Grass            308  45     45      55
    ## 556 496                   Servine    Grass            413  60     60      75
    ## 557 497                 Serperior    Grass            528  75     75      95
    ## 558 498                     Tepig     Fire            308  65     63      45
    ## 559 499                   Pignite     Fire Fighting   418  90     93      55
    ## 560 500                    Emboar     Fire Fighting   528 110    123      65
    ## 561 501                  Oshawott    Water            308  55     55      45
    ## 562 502                    Dewott    Water            413  75     75      60
    ## 563 503                  Samurott    Water            528  95    100      85
    ## 564 504                    Patrat   Normal            255  45     55      39
    ## 565 505                   Watchog   Normal            420  60     85      69
    ## 566 506                  Lillipup   Normal            275  45     60      45
    ## 567 507                   Herdier   Normal            370  65     80      65
    ## 568 508                 Stoutland   Normal            500  85    110      90
    ## 569 509                  Purrloin     Dark            281  41     50      37
    ## 570 510                   Liepard     Dark            446  64     88      50
    ## 571 511                   Pansage    Grass            316  50     53      48
    ## 572 512                  Simisage    Grass            498  75     98      63
    ## 573 513                   Pansear     Fire            316  50     53      48
    ## 574 514                  Simisear     Fire            498  75     98      63
    ## 575 515                   Panpour    Water            316  50     53      48
    ## 576 516                  Simipour    Water            498  75     98      63
    ## 577 517                     Munna  Psychic            292  76     25      45
    ## 578 518                  Musharna  Psychic            487 116     55      85
    ## 579 519                    Pidove   Normal   Flying   264  50     55      50
    ## 580 520                 Tranquill   Normal   Flying   358  62     77      62
    ## 581 521                  Unfezant   Normal   Flying   488  80    115      80
    ## 582 522                   Blitzle Electric            295  45     60      32
    ## 583 523                 Zebstrika Electric            497  75    100      63
    ## 584 524                Roggenrola     Rock            280  55     75      85
    ## 585 525                   Boldore     Rock            390  70    105     105
    ## 586 526                  Gigalith     Rock            515  85    135     130
    ## 587 527                    Woobat  Psychic   Flying   313  55     45      43
    ## 588 528                   Swoobat  Psychic   Flying   425  67     57      55
    ## 589 529                   Drilbur   Ground            328  60     85      40
    ## 590 530                 Excadrill   Ground    Steel   508 110    135      60
    ## 591 531                    Audino   Normal            445 103     60      86
    ## 592 531         AudinoMega Audino   Normal    Fairy   545 103     60     126
    ## 593 532                   Timburr Fighting            305  75     80      55
    ## 594 533                   Gurdurr Fighting            405  85    105      85
    ## 595 534                Conkeldurr Fighting            505 105    140      95
    ## 596 535                   Tympole    Water            294  50     50      40
    ## 597 536                 Palpitoad    Water   Ground   384  75     65      55
    ## 598 537                Seismitoad    Water   Ground   509 105     95      75
    ## 599 538                     Throh Fighting            465 120    100      85
    ## 600 539                      Sawk Fighting            465  75    125      75
    ## 601 540                  Sewaddle      Bug    Grass   310  45     53      70
    ## 602 541                  Swadloon      Bug    Grass   380  55     63      90
    ## 603 542                  Leavanny      Bug    Grass   500  75    103      80
    ## 604 543                  Venipede      Bug   Poison   260  30     45      59
    ## 605 544                Whirlipede      Bug   Poison   360  40     55      99
    ## 606 545                 Scolipede      Bug   Poison   485  60    100      89
    ## 607 546                  Cottonee    Grass    Fairy   280  40     27      60
    ## 608 547                Whimsicott    Grass    Fairy   480  60     67      85
    ## 609 548                   Petilil    Grass            280  45     35      50
    ## 610 549                 Lilligant    Grass            480  70     60      75
    ## 611 550                  Basculin    Water            460  70     92      65
    ## 612 551                   Sandile   Ground     Dark   292  50     72      35
    ## 613 552                  Krokorok   Ground     Dark   351  60     82      45
    ## 614 553                Krookodile   Ground     Dark   519  95    117      80
    ## 615 554                  Darumaka     Fire            315  70     90      45
    ## 616 555   DarmanitanStandard Mode     Fire            480 105    140      55
    ## 617 555        DarmanitanZen Mode     Fire  Psychic   540 105     30     105
    ## 618 556                  Maractus    Grass            461  75     86      67
    ## 619 557                   Dwebble      Bug     Rock   325  50     65      85
    ## 620 558                   Crustle      Bug     Rock   475  70     95     125
    ## 621 559                   Scraggy     Dark Fighting   348  50     75      70
    ## 622 560                   Scrafty     Dark Fighting   488  65     90     115
    ## 623 561                  Sigilyph  Psychic   Flying   490  72     58      80
    ## 624 562                    Yamask    Ghost            303  38     30      85
    ## 625 563                Cofagrigus    Ghost            483  58     50     145
    ## 626 564                  Tirtouga    Water     Rock   355  54     78     103
    ## 627 565                Carracosta    Water     Rock   495  74    108     133
    ## 628 566                    Archen     Rock   Flying   401  55    112      45
    ## 629 567                  Archeops     Rock   Flying   567  75    140      65
    ## 630 568                  Trubbish   Poison            329  50     50      62
    ## 631 569                  Garbodor   Poison            474  80     95      82
    ## 632 570                     Zorua     Dark            330  40     65      40
    ## 633 571                   Zoroark     Dark            510  60    105      60
    ## 634 572                  Minccino   Normal            300  55     50      40
    ## 635 573                  Cinccino   Normal            470  75     95      60
    ## 636 574                   Gothita  Psychic            290  45     30      50
    ## 637 575                 Gothorita  Psychic            390  60     45      70
    ## 638 576                Gothitelle  Psychic            490  70     55      95
    ## 639 577                   Solosis  Psychic            290  45     30      40
    ## 640 578                   Duosion  Psychic            370  65     40      50
    ## 641 579                 Reuniclus  Psychic            490 110     65      75
    ## 642 580                  Ducklett    Water   Flying   305  62     44      50
    ## 643 581                    Swanna    Water   Flying   473  75     87      63
    ## 644 582                 Vanillite      Ice            305  36     50      50
    ## 645 583                 Vanillish      Ice            395  51     65      65
    ## 646 584                 Vanilluxe      Ice            535  71     95      85
    ## 647 585                  Deerling   Normal    Grass   335  60     60      50
    ## 648 586                  Sawsbuck   Normal    Grass   475  80    100      70
    ## 649 587                    Emolga Electric   Flying   428  55     75      60
    ## 650 588                Karrablast      Bug            315  50     75      45
    ## 651 589                Escavalier      Bug    Steel   495  70    135     105
    ## 652 590                   Foongus    Grass   Poison   294  69     55      45
    ## 653 591                 Amoonguss    Grass   Poison   464 114     85      70
    ## 654 592                  Frillish    Water    Ghost   335  55     40      50
    ## 655 593                 Jellicent    Water    Ghost   480 100     60      70
    ## 656 594                 Alomomola    Water            470 165     75      80
    ## 657 595                    Joltik      Bug Electric   319  50     47      50
    ## 658 596                Galvantula      Bug Electric   472  70     77      60
    ## 659 597                 Ferroseed    Grass    Steel   305  44     50      91
    ## 660 598                Ferrothorn    Grass    Steel   489  74     94     131
    ## 661 599                     Klink    Steel            300  40     55      70
    ## 662 600                     Klang    Steel            440  60     80      95
    ## 663 601                 Klinklang    Steel            520  60    100     115
    ## 664 602                    Tynamo Electric            275  35     55      40
    ## 665 603                 Eelektrik Electric            405  65     85      70
    ## 666 604                Eelektross Electric            515  85    115      80
    ## 667 605                    Elgyem  Psychic            335  55     55      55
    ## 668 606                  Beheeyem  Psychic            485  75     75      75
    ## 669 607                   Litwick    Ghost     Fire   275  50     30      55
    ## 670 608                   Lampent    Ghost     Fire   370  60     40      60
    ## 671 609                Chandelure    Ghost     Fire   520  60     55      90
    ## 672 610                      Axew   Dragon            320  46     87      60
    ## 673 611                   Fraxure   Dragon            410  66    117      70
    ## 674 612                   Haxorus   Dragon            540  76    147      90
    ## 675 613                   Cubchoo      Ice            305  55     70      40
    ## 676 614                   Beartic      Ice            485  95    110      80
    ## 677 615                 Cryogonal      Ice            485  70     50      30
    ## 678 616                   Shelmet      Bug            305  50     40      85
    ## 679 617                  Accelgor      Bug            495  80     70      40
    ## 680 618                  Stunfisk   Ground Electric   471 109     66      84
    ## 681 619                   Mienfoo Fighting            350  45     85      50
    ## 682 620                  Mienshao Fighting            510  65    125      60
    ## 683 621                 Druddigon   Dragon            485  77    120      90
    ## 684 622                    Golett   Ground    Ghost   303  59     74      50
    ## 685 623                    Golurk   Ground    Ghost   483  89    124      80
    ## 686 624                  Pawniard     Dark    Steel   340  45     85      70
    ## 687 625                   Bisharp     Dark    Steel   490  65    125     100
    ## 688 626                Bouffalant   Normal            490  95    110      95
    ## 689 627                   Rufflet   Normal   Flying   350  70     83      50
    ## 690 628                  Braviary   Normal   Flying   510 100    123      75
    ## 691 629                   Vullaby     Dark   Flying   370  70     55      75
    ## 692 630                 Mandibuzz     Dark   Flying   510 110     65     105
    ## 693 631                   Heatmor     Fire            484  85     97      66
    ## 694 632                    Durant      Bug    Steel   484  58    109     112
    ## 695 633                     Deino     Dark   Dragon   300  52     65      50
    ## 696 634                  Zweilous     Dark   Dragon   420  72     85      70
    ## 697 635                 Hydreigon     Dark   Dragon   600  92    105      90
    ## 698 636                  Larvesta      Bug     Fire   360  55     85      55
    ## 699 637                 Volcarona      Bug     Fire   550  85     60      65
    ## 700 638                  Cobalion    Steel Fighting   580  91     90     129
    ## 701 639                 Terrakion     Rock Fighting   580  91    129      90
    ## 702 640                  Virizion    Grass Fighting   580  91     90      72
    ## 703 641   TornadusIncarnate Forme   Flying            580  79    115      70
    ## 704 641     TornadusTherian Forme   Flying            580  79    100      80
    ## 705 642  ThundurusIncarnate Forme Electric   Flying   580  79    115      70
    ## 706 642    ThundurusTherian Forme Electric   Flying   580  79    105      70
    ## 707 643                  Reshiram   Dragon     Fire   680 100    120     100
    ## 708 644                    Zekrom   Dragon Electric   680 100    150     120
    ## 709 645   LandorusIncarnate Forme   Ground   Flying   600  89    125      90
    ## 710 645     LandorusTherian Forme   Ground   Flying   600  89    145      90
    ## 711 646                    Kyurem   Dragon      Ice   660 125    130      90
    ## 712 646        KyuremBlack Kyurem   Dragon      Ice   700 125    170     100
    ## 713 646        KyuremWhite Kyurem   Dragon      Ice   700 125    120      90
    ## 714 647      KeldeoOrdinary Forme    Water Fighting   580  91     72      90
    ## 715 647      KeldeoResolute Forme    Water Fighting   580  91     72      90
    ## 716 648        MeloettaAria Forme   Normal  Psychic   600 100     77      77
    ## 717 648   MeloettaPirouette Forme   Normal Fighting   600 100    128      90
    ## 718 649                  Genesect      Bug    Steel   600  71    120      95
    ## 719 650                   Chespin    Grass            313  56     61      65
    ## 720 651                 Quilladin    Grass            405  61     78      95
    ## 721 652                Chesnaught    Grass Fighting   530  88    107     122
    ## 722 653                  Fennekin     Fire            307  40     45      40
    ## 723 654                   Braixen     Fire            409  59     59      58
    ## 724 655                   Delphox     Fire  Psychic   534  75     69      72
    ## 725 656                   Froakie    Water            314  41     56      40
    ## 726 657                 Frogadier    Water            405  54     63      52
    ## 727 658                  Greninja    Water     Dark   530  72     95      67
    ## 728 659                  Bunnelby   Normal            237  38     36      38
    ## 729 660                 Diggersby   Normal   Ground   423  85     56      77
    ## 730 661                Fletchling   Normal   Flying   278  45     50      43
    ## 731 662               Fletchinder     Fire   Flying   382  62     73      55
    ## 732 663                Talonflame     Fire   Flying   499  78     81      71
    ## 733 664                Scatterbug      Bug            200  38     35      40
    ## 734 665                    Spewpa      Bug            213  45     22      60
    ## 735 666                  Vivillon      Bug   Flying   411  80     52      50
    ## 736 667                    Litleo     Fire   Normal   369  62     50      58
    ## 737 668                    Pyroar     Fire   Normal   507  86     68      72
    ## 738 669                 FlabÃ©bÃ©    Fairy            303  44     38      39
    ## 739 670                   Floette    Fairy            371  54     45      47
    ## 740 671                   Florges    Fairy            552  78     65      68
    ## 741 672                    Skiddo    Grass            350  66     65      48
    ## 742 673                    Gogoat    Grass            531 123    100      62
    ## 743 674                   Pancham Fighting            348  67     82      62
    ## 744 675                   Pangoro Fighting     Dark   495  95    124      78
    ## 745 676                   Furfrou   Normal            472  75     80      60
    ## 746 677                    Espurr  Psychic            355  62     48      54
    ## 747 678              MeowsticMale  Psychic            466  74     48      76
    ## 748 678            MeowsticFemale  Psychic            466  74     48      76
    ## 749 679                   Honedge    Steel    Ghost   325  45     80     100
    ## 750 680                  Doublade    Steel    Ghost   448  59    110     150
    ## 751 681      AegislashBlade Forme    Steel    Ghost   520  60    150      50
    ## 752 681     AegislashShield Forme    Steel    Ghost   520  60     50     150
    ## 753 682                  Spritzee    Fairy            341  78     52      60
    ## 754 683                Aromatisse    Fairy            462 101     72      72
    ## 755 684                   Swirlix    Fairy            341  62     48      66
    ## 756 685                  Slurpuff    Fairy            480  82     80      86
    ## 757 686                     Inkay     Dark  Psychic   288  53     54      53
    ## 758 687                   Malamar     Dark  Psychic   482  86     92      88
    ## 759 688                   Binacle     Rock    Water   306  42     52      67
    ## 760 689                Barbaracle     Rock    Water   500  72    105     115
    ## 761 690                    Skrelp   Poison    Water   320  50     60      60
    ## 762 691                  Dragalge   Poison   Dragon   494  65     75      90
    ## 763 692                 Clauncher    Water            330  50     53      62
    ## 764 693                 Clawitzer    Water            500  71     73      88
    ## 765 694                Helioptile Electric   Normal   289  44     38      33
    ## 766 695                 Heliolisk Electric   Normal   481  62     55      52
    ## 767 696                    Tyrunt     Rock   Dragon   362  58     89      77
    ## 768 697                 Tyrantrum     Rock   Dragon   521  82    121     119
    ## 769 698                    Amaura     Rock      Ice   362  77     59      50
    ## 770 699                   Aurorus     Rock      Ice   521 123     77      72
    ## 771 700                   Sylveon    Fairy            525  95     65      65
    ## 772 701                  Hawlucha Fighting   Flying   500  78     92      75
    ## 773 702                   Dedenne Electric    Fairy   431  67     58      57
    ## 774 703                   Carbink     Rock    Fairy   500  50     50     150
    ## 775 704                     Goomy   Dragon            300  45     50      35
    ## 776 705                   Sliggoo   Dragon            452  68     75      53
    ## 777 706                    Goodra   Dragon            600  90    100      70
    ## 778 707                    Klefki    Steel    Fairy   470  57     80      91
    ## 779 708                  Phantump    Ghost    Grass   309  43     70      48
    ## 780 709                 Trevenant    Ghost    Grass   474  85    110      76
    ## 781 710     PumpkabooAverage Size    Ghost    Grass   335  49     66      70
    ## 782 710       PumpkabooSmall Size    Ghost    Grass   335  44     66      70
    ## 783 710       PumpkabooLarge Size    Ghost    Grass   335  54     66      70
    ## 784 710       PumpkabooSuper Size    Ghost    Grass   335  59     66      70
    ## 785 711     GourgeistAverage Size    Ghost    Grass   494  65     90     122
    ## 786 711       GourgeistSmall Size    Ghost    Grass   494  55     85     122
    ## 787 711       GourgeistLarge Size    Ghost    Grass   494  75     95     122
    ## 788 711       GourgeistSuper Size    Ghost    Grass   494  85    100     122
    ## 789 712                  Bergmite      Ice            304  55     69      85
    ## 790 713                   Avalugg      Ice            514  95    117     184
    ## 791 714                    Noibat   Flying   Dragon   245  40     30      35
    ## 792 715                   Noivern   Flying   Dragon   535  85     70      80
    ## 793 716                   Xerneas    Fairy            680 126    131      95
    ## 794 717                   Yveltal     Dark   Flying   680 126    131      95
    ## 795 718          Zygarde50% Forme   Dragon   Ground   600 108    100     121
    ## 796 719                   Diancie     Rock    Fairy   600  50    100     150
    ## 797 719       DiancieMega Diancie     Rock    Fairy   700  50    160     110
    ## 798 720       HoopaHoopa Confined  Psychic    Ghost   600  80    110      60
    ## 799 720        HoopaHoopa Unbound  Psychic     Dark   680  80    160      60
    ## 800 721                 Volcanion     Fire    Water   600  80    110     120
    ##     Sp..Atk Sp..Def Speed Generation Legendary
    ## 1        65      65    45          1     False
    ## 2        80      80    60          1     False
    ## 3       100     100    80          1     False
    ## 4       122     120    80          1     False
    ## 5        60      50    65          1     False
    ## 6        80      65    80          1     False
    ## 7       109      85   100          1     False
    ## 8       130      85   100          1     False
    ## 9       159     115   100          1     False
    ## 10       50      64    43          1     False
    ## 11       65      80    58          1     False
    ## 12       85     105    78          1     False
    ## 13      135     115    78          1     False
    ## 14       20      20    45          1     False
    ## 15       25      25    30          1     False
    ## 16       90      80    70          1     False
    ## 17       20      20    50          1     False
    ## 18       25      25    35          1     False
    ## 19       45      80    75          1     False
    ## 20       15      80   145          1     False
    ## 21       35      35    56          1     False
    ## 22       50      50    71          1     False
    ## 23       70      70   101          1     False
    ## 24      135      80   121          1     False
    ## 25       25      35    72          1     False
    ## 26       50      70    97          1     False
    ## 27       31      31    70          1     False
    ## 28       61      61   100          1     False
    ## 29       40      54    55          1     False
    ## 30       65      79    80          1     False
    ## 31       50      50    90          1     False
    ## 32       90      80   110          1     False
    ## 33       20      30    40          1     False
    ## 34       45      55    65          1     False
    ## 35       40      40    41          1     False
    ## 36       55      55    56          1     False
    ## 37       75      85    76          1     False
    ## 38       40      40    50          1     False
    ## 39       55      55    65          1     False
    ## 40       85      75    85          1     False
    ## 41       60      65    35          1     False
    ## 42       95      90    60          1     False
    ## 43       50      65    65          1     False
    ## 44       81     100   100          1     False
    ## 45       45      25    20          1     False
    ## 46       85      50    45          1     False
    ## 47       30      40    55          1     False
    ## 48       65      75    90          1     False
    ## 49       75      65    30          1     False
    ## 50       85      75    40          1     False
    ## 51      110      90    50          1     False
    ## 52       45      55    25          1     False
    ## 53       60      80    30          1     False
    ## 54       40      55    45          1     False
    ## 55       90      75    90          1     False
    ## 56       35      45    95          1     False
    ## 57       50      70   120          1     False
    ## 58       40      40    90          1     False
    ## 59       65      65   115          1     False
    ## 60       65      50    55          1     False
    ## 61       95      80    85          1     False
    ## 62       35      45    70          1     False
    ## 63       60      70    95          1     False
    ## 64       70      50    60          1     False
    ## 65      100      80    95          1     False
    ## 66       40      40    90          1     False
    ## 67       50      50    90          1     False
    ## 68       70      90    70          1     False
    ## 69      105      55    90          1     False
    ## 70      120      70   105          1     False
    ## 71      135      95   120          1     False
    ## 72      175      95   150          1     False
    ## 73       35      35    35          1     False
    ## 74       50      60    45          1     False
    ## 75       65      85    55          1     False
    ## 76       70      30    40          1     False
    ## 77       85      45    55          1     False
    ## 78      100      70    70          1     False
    ## 79       50     100    70          1     False
    ## 80       80     120   100          1     False
    ## 81       30      30    20          1     False
    ## 82       45      45    35          1     False
    ## 83       55      65    45          1     False
    ## 84       65      65    90          1     False
    ## 85       80      80   105          1     False
    ## 86       40      40    15          1     False
    ## 87      100      80    30          1     False
    ## 88      130      80    30          1     False
    ## 89       95      55    45          1     False
    ## 90      120      70    70          1     False
    ## 91       58      62    60          1     False
    ## 92       35      35    75          1     False
    ## 93       60      60   100          1     False
    ## 94       45      70    45          1     False
    ## 95       70      95    70          1     False
    ## 96       40      50    25          1     False
    ## 97       65     100    50          1     False
    ## 98       45      25    40          1     False
    ## 99       85      45    70          1     False
    ## 100     100      35    80          1     False
    ## 101     115      55    95          1     False
    ## 102     130      75   110          1     False
    ## 103     170      95   130          1     False
    ## 104      30      45    70          1     False
    ## 105      43      90    42          1     False
    ## 106      73     115    67          1     False
    ## 107      25      25    50          1     False
    ## 108      50      50    75          1     False
    ## 109      55      55   100          1     False
    ## 110      80      80   140          1     False
    ## 111      60      45    40          1     False
    ## 112     125      65    55          1     False
    ## 113      40      50    35          1     False
    ## 114      50      80    45          1     False
    ## 115      35     110    87          1     False
    ## 116      35     110    76          1     False
    ## 117      60      75    30          1     False
    ## 118      60      45    35          1     False
    ## 119      85      70    60          1     False
    ## 120      30      30    25          1     False
    ## 121      45      45    40          1     False
    ## 122      35     105    50          1     False
    ## 123     100      40    60          1     False
    ## 124      40      80    90          1     False
    ## 125      60     100   100          1     False
    ## 126      70      25    60          1     False
    ## 127      95      45    85          1     False
    ## 128      35      50    63          1     False
    ## 129      65      80    68          1     False
    ## 130      70      55    85          1     False
    ## 131     100      85   115          1     False
    ## 132     100     120    90          1     False
    ## 133      55      80   105          1     False
    ## 134     115      95    95          1     False
    ## 135      95      85   105          1     False
    ## 136     100      85    93          1     False
    ## 137      55      70    85          1     False
    ## 138      65      90   105          1     False
    ## 139      40      70   110          1     False
    ## 140      15      20    80          1     False
    ## 141      60     100    81          1     False
    ## 142      70     130    81          1     False
    ## 143      85      95    60          1     False
    ## 144      48      48    48          1     False
    ## 145      45      65    55          1     False
    ## 146     110      95    65          1     False
    ## 147     110      95   130          1     False
    ## 148      95     110    65          1     False
    ## 149      85      75    40          1     False
    ## 150      90      55    35          1     False
    ## 151     115      70    55          1     False
    ## 152      55      45    55          1     False
    ## 153      65      70    80          1     False
    ## 154      60      75   130          1     False
    ## 155      70      95   150          1     False
    ## 156      65     110    30          1     False
    ## 157      95     125    85          1      True
    ## 158     125      90   100          1      True
    ## 159     125      85    90          1      True
    ## 160      50      50    50          1     False
    ## 161      70      70    70          1     False
    ## 162     100     100    80          1     False
    ## 163     154      90   130          1      True
    ## 164     154     100   130          1      True
    ## 165     194     120   140          1      True
    ## 166     100     100   100          1     False
    ## 167      49      65    45          2     False
    ## 168      63      80    60          2     False
    ## 169      83     100    80          2     False
    ## 170      60      50    65          2     False
    ## 171      80      65    80          2     False
    ## 172     109      85   100          2     False
    ## 173      44      48    43          2     False
    ## 174      59      63    58          2     False
    ## 175      79      83    78          2     False
    ## 176      35      45    20          2     False
    ## 177      45      55    90          2     False
    ## 178      36      56    50          2     False
    ## 179      76      96    70          2     False
    ## 180      40      80    55          2     False
    ## 181      55     110    85          2     False
    ## 182      40      40    30          2     False
    ## 183      60      60    40          2     False
    ## 184      70      80   130          2     False
    ## 185      56      56    67          2     False
    ## 186      76      76    67          2     False
    ## 187      35      35    60          2     False
    ## 188      45      55    15          2     False
    ## 189      40      20    15          2     False
    ## 190      40      65    20          2     False
    ## 191      80     105    40          2     False
    ## 192      70      45    70          2     False
    ## 193      95      70    95          2     False
    ## 194      65      45    35          2     False
    ## 195      80      60    45          2     False
    ## 196     115      90    55          2     False
    ## 197     165     110    45          2     False
    ## 198      90     100    50          2     False
    ## 199      20      50    40          2     False
    ## 200      60      80    50          2     False
    ## 201      30      65    30          2     False
    ## 202      90     100    70          2     False
    ## 203      35      55    50          2     False
    ## 204      45      65    80          2     False
    ## 205      55      95   110          2     False
    ## 206      40      55    85          2     False
    ## 207      30      30    30          2     False
    ## 208     105      85    30          2     False
    ## 209      75      45    95          2     False
    ## 210      25      25    15          2     False
    ## 211      65      65    35          2     False
    ## 212     130      95   110          2     False
    ## 213      60     130    65          2     False
    ## 214      85      42    91          2     False
    ## 215     100     110    30          2     False
    ## 216      85      85    85          2     False
    ## 217      72      48    48          2     False
    ## 218      33      58    33          2     False
    ## 219      90      65    85          2     False
    ## 220      35      35    15          2     False
    ## 221      60      60    40          2     False
    ## 222      65      65    45          2     False
    ## 223      35      65    85          2     False
    ## 224      55      65    30          2     False
    ## 225      55      95    30          2     False
    ## 226      40      40    30          2     False
    ## 227      60      60    45          2     False
    ## 228      55      55    85          2     False
    ## 229      55      80    65          2     False
    ## 230      65     100    75          2     False
    ## 231      10     230     5          2     False
    ## 232      40      95    85          2     False
    ## 233      40     105    75          2     False
    ## 234      35      75   115          2     False
    ## 235      50      50    40          2     False
    ## 236      75      75    55          2     False
    ## 237      70      40    20          2     False
    ## 238      80      80    30          2     False
    ## 239      30      30    50          2     False
    ## 240      60      60    50          2     False
    ## 241      65      85    35          2     False
    ## 242      65      35    65          2     False
    ## 243     105      75    45          2     False
    ## 244      65      45    75          2     False
    ## 245      80     140    70          2     False
    ## 246      40      70    70          2     False
    ## 247      80      50    65          2     False
    ## 248     110      80    95          2     False
    ## 249     140      90   115          2     False
    ## 250      95      95    85          2     False
    ## 251      40      40    40          2     False
    ## 252      60      60    50          2     False
    ## 253     105      95    60          2     False
    ## 254      85      65    85          2     False
    ## 255      20      45    75          2     False
    ## 256      35      35    35          2     False
    ## 257      35     110    70          2     False
    ## 258      85      65    65          2     False
    ## 259      65      55    95          2     False
    ## 260      70      55    83          2     False
    ## 261      40      70   100          2     False
    ## 262      75     135    55          2     False
    ## 263     115     100   115          2      True
    ## 264      90      75   100          2      True
    ## 265      90     115    85          2      True
    ## 266      45      50    41          2     False
    ## 267      65      70    51          2     False
    ## 268      95     100    61          2     False
    ## 269      95     120    71          2     False
    ## 270      90     154   110          2      True
    ## 271     110     154    90          2      True
    ## 272     100     100   100          2     False
    ## 273      65      55    70          3     False
    ## 274      85      65    95          3     False
    ## 275     105      85   120          3     False
    ## 276     145      85   145          3     False
    ## 277      70      50    45          3     False
    ## 278      85      60    55          3     False
    ## 279     110      70    80          3     False
    ## 280     130      80   100          3     False
    ## 281      50      50    40          3     False
    ## 282      60      70    50          3     False
    ## 283      85      90    60          3     False
    ## 284      95     110    70          3     False
    ## 285      30      30    35          3     False
    ## 286      60      60    70          3     False
    ## 287      30      41    60          3     False
    ## 288      50      61   100          3     False
    ## 289      20      30    20          3     False
    ## 290      25      25    15          3     False
    ## 291     100      50    65          3     False
    ## 292      25      25    15          3     False
    ## 293      50      90    65          3     False
    ## 294      40      50    30          3     False
    ## 295      60      70    50          3     False
    ## 296      90     100    70          3     False
    ## 297      30      30    30          3     False
    ## 298      60      40    60          3     False
    ## 299      90      60    80          3     False
    ## 300      30      30    85          3     False
    ## 301      50      50   125          3     False
    ## 302      55      30    85          3     False
    ## 303      85      70    65          3     False
    ## 304      45      35    40          3     False
    ## 305      65      55    50          3     False
    ## 306     125     115    80          3     False
    ## 307     165     135   100          3     False
    ## 308      50      52    65          3     False
    ## 309      80      82    60          3     False
    ## 310      40      60    35          3     False
    ## 311      60      60    70          3     False
    ## 312      35      35    30          3     False
    ## 313      55      55    90          3     False
    ## 314      95      65   100          3     False
    ## 315      30      30    40          3     False
    ## 316      50      50   160          3     False
    ## 317      30      30    40          3     False
    ## 318      51      23    28          3     False
    ## 319      71      43    48          3     False
    ## 320      91      73    68          3     False
    ## 321      20      30    25          3     False
    ## 322      40      60    50          3     False
    ## 323      20      40    20          3     False
    ## 324      45      90    30          3     False
    ## 325      35      35    50          3     False
    ## 326      55      55    70          3     False
    ## 327      65      65    50          3     False
    ## 328      85     115    20          3     False
    ## 329      55      55    50          3     False
    ## 330      55      95    50          3     False
    ## 331      40      40    30          3     False
    ## 332      50      50    40          3     False
    ## 333      60      60    50          3     False
    ## 334      60      80    50          3     False
    ## 335      40      55    60          3     False
    ## 336      60      75    80          3     False
    ## 337      80      85   100          3     False
    ## 338      65      40    65          3     False
    ## 339     105      60   105          3     False
    ## 340     135      80   135          3     False
    ## 341      85      75    95          3     False
    ## 342      75      85    95          3     False
    ## 343      47      75    85          3     False
    ## 344      73      75    85          3     False
    ## 345     100      80    65          3     False
    ## 346      43      53    40          3     False
    ## 347      73      83    55          3     False
    ## 348      65      20    65          3     False
    ## 349      95      40    95          3     False
    ## 350     110      65   105          3     False
    ## 351      70      35    60          3     False
    ## 352      90      45    60          3     False
    ## 353      65      45    35          3     False
    ## 354     105      75    40          3     False
    ## 355     145     105    20          3     False
    ## 356      85      70    20          3     False
    ## 357      70      80    60          3     False
    ## 358      90     110    80          3     False
    ## 359      60      60    60          3     False
    ## 360      45      45    10          3     False
    ## 361      50      50    70          3     False
    ## 362      80      80   100          3     False
    ## 363      85      40    35          3     False
    ## 364     115      60    55          3     False
    ## 365      40      75    50          3     False
    ## 366      70     105    80          3     False
    ## 367     110     105    80          3     False
    ## 368      60      60    90          3     False
    ## 369     100      60    65          3     False
    ## 370      95      85    70          3     False
    ## 371      55      65    70          3     False
    ## 372      46      41    60          3     False
    ## 373      76      71    60          3     False
    ## 374      50      35    35          3     False
    ## 375      90      55    55          3     False
    ## 376      40      70    55          3     False
    ## 377      70     120    75          3     False
    ## 378      61      87    23          3     False
    ## 379      81     107    43          3     False
    ## 380      40      50    75          3     False
    ## 381      70      80    45          3     False
    ## 382      10      55    80          3     False
    ## 383     100     125    81          3     False
    ## 384      70      70    70          3     False
    ## 385      60     120    40          3     False
    ## 386      63      33    45          3     False
    ## 387      83      63    65          3     False
    ## 388      93      83    75          3     False
    ## 389      30      90    25          3     False
    ## 390      60     130    25          3     False
    ## 391      72      87    51          3     False
    ## 392      95      80    65          3     False
    ## 393      75      60    75          3     False
    ## 394     115      60   115          3     False
    ## 395      23      48    23          3     False
    ## 396      50      50    50          3     False
    ## 397      80      80    80          3     False
    ## 398     120      80   100          3     False
    ## 399      55      50    25          3     False
    ## 400      75      70    45          3     False
    ## 401      95      90    65          3     False
    ## 402      74      55    32          3     False
    ## 403      94      75    52          3     False
    ## 404     114      75    52          3     False
    ## 405      45      65    55          3     False
    ## 406      40      65    97          3     False
    ## 407      40      30    50          3     False
    ## 408      60      50    50          3     False
    ## 409     110      80   100          3     False
    ## 410     120      90   120          3     False
    ## 411      35      60    30          3     False
    ## 412      55      80    50          3     False
    ## 413      95      90    70          3     False
    ## 414     105     110   110          3     False
    ## 415      50     100    50          3      True
    ## 416     100     200    50          3      True
    ## 417      75     150    50          3      True
    ## 418     110     130   110          3      True
    ## 419     140     150   110          3      True
    ## 420     130     110   110          3      True
    ## 421     160     120   110          3      True
    ## 422     150     140    90          3      True
    ## 423     180     160    90          3      True
    ## 424     100      90    90          3      True
    ## 425     150      90    90          3      True
    ## 426     150      90    95          3      True
    ## 427     180     100   115          3      True
    ## 428     100     100   100          3      True
    ## 429     150      50   150          3      True
    ## 430     180      20   150          3      True
    ## 431      70     160    90          3      True
    ## 432      95      90   180          3      True
    ## 433      45      55    31          4     False
    ## 434      55      65    36          4     False
    ## 435      75      85    56          4     False
    ## 436      58      44    61          4     False
    ## 437      78      52    81          4     False
    ## 438     104      71   108          4     False
    ## 439      61      56    40          4     False
    ## 440      81      76    50          4     False
    ## 441     111     101    60          4     False
    ## 442      30      30    60          4     False
    ## 443      40      40    80          4     False
    ## 444      50      60   100          4     False
    ## 445      35      40    31          4     False
    ## 446      55      60    71          4     False
    ## 447      25      41    25          4     False
    ## 448      55      51    65          4     False
    ## 449      40      34    45          4     False
    ## 450      60      49    60          4     False
    ## 451      95      79    70          4     False
    ## 452      50      70    55          4     False
    ## 453     125     105    90          4     False
    ## 454      30      30    58          4     False
    ## 455      65      50    58          4     False
    ## 456      42      88    30          4     False
    ## 457      47     138    30          4     False
    ## 458      29      45    36          4     False
    ## 459      79     105    36          4     False
    ## 460      59      85    36          4     False
    ## 461      69      95    36          4     False
    ## 462      94      50    66          4     False
    ## 463      30      42    70          4     False
    ## 464      80     102    40          4     False
    ## 465      45      90    95          4     False
    ## 466      60      30    85          4     False
    ## 467      85      50   115          4     False
    ## 468      62      53    35          4     False
    ## 469      87      78    85          4     False
    ## 470      57      62    34          4     False
    ## 471      92      82    39          4     False
    ## 472      60      66   115          4     False
    ## 473      60      44    70          4     False
    ## 474      90      54    80          4     False
    ## 475      44      56    85          4     False
    ## 476      54      96   105          4     False
    ## 477      54      96   135          4     False
    ## 478     105     105   105          4     False
    ## 479     105      52    71          4     False
    ## 480      42      37    85          4     False
    ## 481      64      59   112          4     False
    ## 482      65      50    45          4     False
    ## 483      41      41    74          4     False
    ## 484      71      61    84          4     False
    ## 485      24      86    23          4     False
    ## 486      79     116    33          4     False
    ## 487      10      45    10          4     False
    ## 488      70      90    60          4     False
    ## 489      15      65    30          4     False
    ## 490      92      42    91          4     False
    ## 491      92     108    35          4     False
    ## 492      40      45    42          4     False
    ## 493      50      55    82          4     False
    ## 494      80      85   102          4     False
    ## 495     120      95    92          4     False
    ## 496      40      85     5          4     False
    ## 497      35      40    60          4     False
    ## 498     115      70    90          4     False
    ## 499     140      70   112          4     False
    ## 500      38      42    32          4     False
    ## 501      68      72    47          4     False
    ## 502      30      55    65          4     False
    ## 503      60      75    95          4     False
    ## 504      61      40    50          4     False
    ## 505      86      65    85          4     False
    ## 506      90      72    46          4     False
    ## 507      49      61    66          4     False
    ## 508      69      86    91          4     False
    ## 509      60     120    50          4     False
    ## 510      62      60    40          4     False
    ## 511      92      85    60          4     False
    ## 512     132     105    30          4     False
    ## 513      45      85   125          4     False
    ## 514     130      90    60          4     False
    ## 515      80      95    50          4     False
    ## 516      55      55    40          4     False
    ## 517     110      50    50          4     False
    ## 518      95      85    95          4     False
    ## 519     125      95    83          4     False
    ## 520     120     115    80          4     False
    ## 521     116      56    95          4     False
    ## 522      60      65    95          4     False
    ## 523     130      95    65          4     False
    ## 524      45      75    95          4     False
    ## 525      70      60    80          4     False
    ## 526     135      75    90          4     False
    ## 527      65     115    80          4     False
    ## 528      65     115   110          4     False
    ## 529      75     150    40          4     False
    ## 530      65     135    45          4     False
    ## 531      80      70   110          4     False
    ## 532      95      77    91          4     False
    ## 533     105     107    86          4     False
    ## 534     105     107    86          4     False
    ## 535     105     107    86          4     False
    ## 536     105     107    86          4     False
    ## 537     105     107    86          4     False
    ## 538      75     130    95          4      True
    ## 539     105     105    80          4      True
    ## 540     125      70   115          4      True
    ## 541     150     100    90          4      True
    ## 542     150     120   100          4      True
    ## 543     130     106    77          4      True
    ## 544      80     110   100          4      True
    ## 545     100     120    90          4      True
    ## 546     120     100    90          4      True
    ## 547      75     130    85          4     False
    ## 548      80      80    80          4     False
    ## 549     100     100   100          4     False
    ## 550     135      90   125          4      True
    ## 551     100     100   100          4      True
    ## 552     120      75   127          4      True
    ## 553     120     120   120          4      True
    ## 554     100     100   100          5      True
    ## 555      45      55    63          5     False
    ## 556      60      75    83          5     False
    ## 557      75      95   113          5     False
    ## 558      45      45    45          5     False
    ## 559      70      55    55          5     False
    ## 560     100      65    65          5     False
    ## 561      63      45    45          5     False
    ## 562      83      60    60          5     False
    ## 563     108      70    70          5     False
    ## 564      35      39    42          5     False
    ## 565      60      69    77          5     False
    ## 566      25      45    55          5     False
    ## 567      35      65    60          5     False
    ## 568      45      90    80          5     False
    ## 569      50      37    66          5     False
    ## 570      88      50   106          5     False
    ## 571      53      48    64          5     False
    ## 572      98      63   101          5     False
    ## 573      53      48    64          5     False
    ## 574      98      63   101          5     False
    ## 575      53      48    64          5     False
    ## 576      98      63   101          5     False
    ## 577      67      55    24          5     False
    ## 578     107      95    29          5     False
    ## 579      36      30    43          5     False
    ## 580      50      42    65          5     False
    ## 581      65      55    93          5     False
    ## 582      50      32    76          5     False
    ## 583      80      63   116          5     False
    ## 584      25      25    15          5     False
    ## 585      50      40    20          5     False
    ## 586      60      80    25          5     False
    ## 587      55      43    72          5     False
    ## 588      77      55   114          5     False
    ## 589      30      45    68          5     False
    ## 590      50      65    88          5     False
    ## 591      60      86    50          5     False
    ## 592      80     126    50          5     False
    ## 593      25      35    35          5     False
    ## 594      40      50    40          5     False
    ## 595      55      65    45          5     False
    ## 596      50      40    64          5     False
    ## 597      65      55    69          5     False
    ## 598      85      75    74          5     False
    ## 599      30      85    45          5     False
    ## 600      30      75    85          5     False
    ## 601      40      60    42          5     False
    ## 602      50      80    42          5     False
    ## 603      70      80    92          5     False
    ## 604      30      39    57          5     False
    ## 605      40      79    47          5     False
    ## 606      55      69   112          5     False
    ## 607      37      50    66          5     False
    ## 608      77      75   116          5     False
    ## 609      70      50    30          5     False
    ## 610     110      75    90          5     False
    ## 611      80      55    98          5     False
    ## 612      35      35    65          5     False
    ## 613      45      45    74          5     False
    ## 614      65      70    92          5     False
    ## 615      15      45    50          5     False
    ## 616      30      55    95          5     False
    ## 617     140     105    55          5     False
    ## 618     106      67    60          5     False
    ## 619      35      35    55          5     False
    ## 620      65      75    45          5     False
    ## 621      35      70    48          5     False
    ## 622      45     115    58          5     False
    ## 623     103      80    97          5     False
    ## 624      55      65    30          5     False
    ## 625      95     105    30          5     False
    ## 626      53      45    22          5     False
    ## 627      83      65    32          5     False
    ## 628      74      45    70          5     False
    ## 629     112      65   110          5     False
    ## 630      40      62    65          5     False
    ## 631      60      82    75          5     False
    ## 632      80      40    65          5     False
    ## 633     120      60   105          5     False
    ## 634      40      40    75          5     False
    ## 635      65      60   115          5     False
    ## 636      55      65    45          5     False
    ## 637      75      85    55          5     False
    ## 638      95     110    65          5     False
    ## 639     105      50    20          5     False
    ## 640     125      60    30          5     False
    ## 641     125      85    30          5     False
    ## 642      44      50    55          5     False
    ## 643      87      63    98          5     False
    ## 644      65      60    44          5     False
    ## 645      80      75    59          5     False
    ## 646     110      95    79          5     False
    ## 647      40      50    75          5     False
    ## 648      60      70    95          5     False
    ## 649      75      60   103          5     False
    ## 650      40      45    60          5     False
    ## 651      60     105    20          5     False
    ## 652      55      55    15          5     False
    ## 653      85      80    30          5     False
    ## 654      65      85    40          5     False
    ## 655      85     105    60          5     False
    ## 656      40      45    65          5     False
    ## 657      57      50    65          5     False
    ## 658      97      60   108          5     False
    ## 659      24      86    10          5     False
    ## 660      54     116    20          5     False
    ## 661      45      60    30          5     False
    ## 662      70      85    50          5     False
    ## 663      70      85    90          5     False
    ## 664      45      40    60          5     False
    ## 665      75      70    40          5     False
    ## 666     105      80    50          5     False
    ## 667      85      55    30          5     False
    ## 668     125      95    40          5     False
    ## 669      65      55    20          5     False
    ## 670      95      60    55          5     False
    ## 671     145      90    80          5     False
    ## 672      30      40    57          5     False
    ## 673      40      50    67          5     False
    ## 674      60      70    97          5     False
    ## 675      60      40    40          5     False
    ## 676      70      80    50          5     False
    ## 677      95     135   105          5     False
    ## 678      40      65    25          5     False
    ## 679     100      60   145          5     False
    ## 680      81      99    32          5     False
    ## 681      55      50    65          5     False
    ## 682      95      60   105          5     False
    ## 683      60      90    48          5     False
    ## 684      35      50    35          5     False
    ## 685      55      80    55          5     False
    ## 686      40      40    60          5     False
    ## 687      60      70    70          5     False
    ## 688      40      95    55          5     False
    ## 689      37      50    60          5     False
    ## 690      57      75    80          5     False
    ## 691      45      65    60          5     False
    ## 692      55      95    80          5     False
    ## 693     105      66    65          5     False
    ## 694      48      48   109          5     False
    ## 695      45      50    38          5     False
    ## 696      65      70    58          5     False
    ## 697     125      90    98          5     False
    ## 698      50      55    60          5     False
    ## 699     135     105   100          5     False
    ## 700      90      72   108          5      True
    ## 701      72      90   108          5      True
    ## 702      90     129   108          5      True
    ## 703     125      80   111          5      True
    ## 704     110      90   121          5      True
    ## 705     125      80   111          5      True
    ## 706     145      80   101          5      True
    ## 707     150     120    90          5      True
    ## 708     120     100    90          5      True
    ## 709     115      80   101          5      True
    ## 710     105      80    91          5      True
    ## 711     130      90    95          5      True
    ## 712     120      90    95          5      True
    ## 713     170     100    95          5      True
    ## 714     129      90   108          5     False
    ## 715     129      90   108          5     False
    ## 716     128     128    90          5     False
    ## 717      77      77   128          5     False
    ## 718     120      95    99          5     False
    ## 719      48      45    38          6     False
    ## 720      56      58    57          6     False
    ## 721      74      75    64          6     False
    ## 722      62      60    60          6     False
    ## 723      90      70    73          6     False
    ## 724     114     100   104          6     False
    ## 725      62      44    71          6     False
    ## 726      83      56    97          6     False
    ## 727     103      71   122          6     False
    ## 728      32      36    57          6     False
    ## 729      50      77    78          6     False
    ## 730      40      38    62          6     False
    ## 731      56      52    84          6     False
    ## 732      74      69   126          6     False
    ## 733      27      25    35          6     False
    ## 734      27      30    29          6     False
    ## 735      90      50    89          6     False
    ## 736      73      54    72          6     False
    ## 737     109      66   106          6     False
    ## 738      61      79    42          6     False
    ## 739      75      98    52          6     False
    ## 740     112     154    75          6     False
    ## 741      62      57    52          6     False
    ## 742      97      81    68          6     False
    ## 743      46      48    43          6     False
    ## 744      69      71    58          6     False
    ## 745      65      90   102          6     False
    ## 746      63      60    68          6     False
    ## 747      83      81   104          6     False
    ## 748      83      81   104          6     False
    ## 749      35      37    28          6     False
    ## 750      45      49    35          6     False
    ## 751     150      50    60          6     False
    ## 752      50     150    60          6     False
    ## 753      63      65    23          6     False
    ## 754      99      89    29          6     False
    ## 755      59      57    49          6     False
    ## 756      85      75    72          6     False
    ## 757      37      46    45          6     False
    ## 758      68      75    73          6     False
    ## 759      39      56    50          6     False
    ## 760      54      86    68          6     False
    ## 761      60      60    30          6     False
    ## 762      97     123    44          6     False
    ## 763      58      63    44          6     False
    ## 764     120      89    59          6     False
    ## 765      61      43    70          6     False
    ## 766     109      94   109          6     False
    ## 767      45      45    48          6     False
    ## 768      69      59    71          6     False
    ## 769      67      63    46          6     False
    ## 770      99      92    58          6     False
    ## 771     110     130    60          6     False
    ## 772      74      63   118          6     False
    ## 773      81      67   101          6     False
    ## 774      50     150    50          6     False
    ## 775      55      75    40          6     False
    ## 776      83     113    60          6     False
    ## 777     110     150    80          6     False
    ## 778      80      87    75          6     False
    ## 779      50      60    38          6     False
    ## 780      65      82    56          6     False
    ## 781      44      55    51          6     False
    ## 782      44      55    56          6     False
    ## 783      44      55    46          6     False
    ## 784      44      55    41          6     False
    ## 785      58      75    84          6     False
    ## 786      58      75    99          6     False
    ## 787      58      75    69          6     False
    ## 788      58      75    54          6     False
    ## 789      32      35    28          6     False
    ## 790      44      46    28          6     False
    ## 791      45      40    55          6     False
    ## 792      97      80   123          6     False
    ## 793     131      98    99          6      True
    ## 794     131      98    99          6      True
    ## 795      81      95    95          6      True
    ## 796     100     150    50          6      True
    ## 797     160     110   110          6      True
    ## 798     150     130    70          6      True
    ## 799     170     130    80          6      True
    ## 800     130      90    70          6      True

``` r
head(pk)
```

    ##   X.                  Name Type.1 Type.2 Total HP Attack Defense Sp..Atk
    ## 1  1             Bulbasaur  Grass Poison   318 45     49      49      65
    ## 2  2               Ivysaur  Grass Poison   405 60     62      63      80
    ## 3  3              Venusaur  Grass Poison   525 80     82      83     100
    ## 4  3 VenusaurMega Venusaur  Grass Poison   625 80    100     123     122
    ## 5  4            Charmander   Fire          309 39     52      43      60
    ## 6  5            Charmeleon   Fire          405 58     64      58      80
    ##   Sp..Def Speed Generation Legendary
    ## 1      65    45          1     False
    ## 2      80    60          1     False
    ## 3     100    80          1     False
    ## 4     120    80          1     False
    ## 5      50    65          1     False
    ## 6      65    80          1     False

## Limpieza de datos

Para poder hacer un correcto analisis de datos, primero vamos a elimiar
todas las columnas de datos que no utilizaremos, en nuestro caso, solo
nos quedaremos con ataque y velocidad.

``` r
pk
```

    ##      X.                      Name   Type.1   Type.2 Total  HP Attack Defense
    ## 1     1                 Bulbasaur    Grass   Poison   318  45     49      49
    ## 2     2                   Ivysaur    Grass   Poison   405  60     62      63
    ## 3     3                  Venusaur    Grass   Poison   525  80     82      83
    ## 4     3     VenusaurMega Venusaur    Grass   Poison   625  80    100     123
    ## 5     4                Charmander     Fire            309  39     52      43
    ## 6     5                Charmeleon     Fire            405  58     64      58
    ## 7     6                 Charizard     Fire   Flying   534  78     84      78
    ## 8     6 CharizardMega Charizard X     Fire   Dragon   634  78    130     111
    ## 9     6 CharizardMega Charizard Y     Fire   Flying   634  78    104      78
    ## 10    7                  Squirtle    Water            314  44     48      65
    ## 11    8                 Wartortle    Water            405  59     63      80
    ## 12    9                 Blastoise    Water            530  79     83     100
    ## 13    9   BlastoiseMega Blastoise    Water            630  79    103     120
    ## 14   10                  Caterpie      Bug            195  45     30      35
    ## 15   11                   Metapod      Bug            205  50     20      55
    ## 16   12                Butterfree      Bug   Flying   395  60     45      50
    ## 17   13                    Weedle      Bug   Poison   195  40     35      30
    ## 18   14                    Kakuna      Bug   Poison   205  45     25      50
    ## 19   15                  Beedrill      Bug   Poison   395  65     90      40
    ## 20   15     BeedrillMega Beedrill      Bug   Poison   495  65    150      40
    ## 21   16                    Pidgey   Normal   Flying   251  40     45      40
    ## 22   17                 Pidgeotto   Normal   Flying   349  63     60      55
    ## 23   18                   Pidgeot   Normal   Flying   479  83     80      75
    ## 24   18       PidgeotMega Pidgeot   Normal   Flying   579  83     80      80
    ## 25   19                   Rattata   Normal            253  30     56      35
    ## 26   20                  Raticate   Normal            413  55     81      60
    ## 27   21                   Spearow   Normal   Flying   262  40     60      30
    ## 28   22                    Fearow   Normal   Flying   442  65     90      65
    ## 29   23                     Ekans   Poison            288  35     60      44
    ## 30   24                     Arbok   Poison            438  60     85      69
    ## 31   25                   Pikachu Electric            320  35     55      40
    ## 32   26                    Raichu Electric            485  60     90      55
    ## 33   27                 Sandshrew   Ground            300  50     75      85
    ## 34   28                 Sandslash   Ground            450  75    100     110
    ## 35   29                Nidoranâ\231\200   Poison            275  55     47      52
    ## 36   30                  Nidorina   Poison            365  70     62      67
    ## 37   31                 Nidoqueen   Poison   Ground   505  90     92      87
    ## 38   32                Nidoranâ\231‚   Poison            273  46     57      40
    ## 39   33                  Nidorino   Poison            365  61     72      57
    ## 40   34                  Nidoking   Poison   Ground   505  81    102      77
    ## 41   35                  Clefairy    Fairy            323  70     45      48
    ## 42   36                  Clefable    Fairy            483  95     70      73
    ## 43   37                    Vulpix     Fire            299  38     41      40
    ## 44   38                 Ninetales     Fire            505  73     76      75
    ## 45   39                Jigglypuff   Normal    Fairy   270 115     45      20
    ## 46   40                Wigglytuff   Normal    Fairy   435 140     70      45
    ## 47   41                     Zubat   Poison   Flying   245  40     45      35
    ## 48   42                    Golbat   Poison   Flying   455  75     80      70
    ## 49   43                    Oddish    Grass   Poison   320  45     50      55
    ## 50   44                     Gloom    Grass   Poison   395  60     65      70
    ## 51   45                 Vileplume    Grass   Poison   490  75     80      85
    ## 52   46                     Paras      Bug    Grass   285  35     70      55
    ## 53   47                  Parasect      Bug    Grass   405  60     95      80
    ## 54   48                   Venonat      Bug   Poison   305  60     55      50
    ## 55   49                  Venomoth      Bug   Poison   450  70     65      60
    ## 56   50                   Diglett   Ground            265  10     55      25
    ## 57   51                   Dugtrio   Ground            405  35     80      50
    ## 58   52                    Meowth   Normal            290  40     45      35
    ## 59   53                   Persian   Normal            440  65     70      60
    ## 60   54                   Psyduck    Water            320  50     52      48
    ## 61   55                   Golduck    Water            500  80     82      78
    ## 62   56                    Mankey Fighting            305  40     80      35
    ## 63   57                  Primeape Fighting            455  65    105      60
    ## 64   58                 Growlithe     Fire            350  55     70      45
    ## 65   59                  Arcanine     Fire            555  90    110      80
    ## 66   60                   Poliwag    Water            300  40     50      40
    ## 67   61                 Poliwhirl    Water            385  65     65      65
    ## 68   62                 Poliwrath    Water Fighting   510  90     95      95
    ## 69   63                      Abra  Psychic            310  25     20      15
    ## 70   64                   Kadabra  Psychic            400  40     35      30
    ## 71   65                  Alakazam  Psychic            500  55     50      45
    ## 72   65     AlakazamMega Alakazam  Psychic            590  55     50      65
    ## 73   66                    Machop Fighting            305  70     80      50
    ## 74   67                   Machoke Fighting            405  80    100      70
    ## 75   68                   Machamp Fighting            505  90    130      80
    ## 76   69                Bellsprout    Grass   Poison   300  50     75      35
    ## 77   70                Weepinbell    Grass   Poison   390  65     90      50
    ## 78   71                Victreebel    Grass   Poison   490  80    105      65
    ## 79   72                 Tentacool    Water   Poison   335  40     40      35
    ## 80   73                Tentacruel    Water   Poison   515  80     70      65
    ## 81   74                   Geodude     Rock   Ground   300  40     80     100
    ## 82   75                  Graveler     Rock   Ground   390  55     95     115
    ## 83   76                     Golem     Rock   Ground   495  80    120     130
    ## 84   77                    Ponyta     Fire            410  50     85      55
    ## 85   78                  Rapidash     Fire            500  65    100      70
    ## 86   79                  Slowpoke    Water  Psychic   315  90     65      65
    ## 87   80                   Slowbro    Water  Psychic   490  95     75     110
    ## 88   80       SlowbroMega Slowbro    Water  Psychic   590  95     75     180
    ## 89   81                 Magnemite Electric    Steel   325  25     35      70
    ## 90   82                  Magneton Electric    Steel   465  50     60      95
    ## 91   83                Farfetch'd   Normal   Flying   352  52     65      55
    ## 92   84                     Doduo   Normal   Flying   310  35     85      45
    ## 93   85                    Dodrio   Normal   Flying   460  60    110      70
    ## 94   86                      Seel    Water            325  65     45      55
    ## 95   87                   Dewgong    Water      Ice   475  90     70      80
    ## 96   88                    Grimer   Poison            325  80     80      50
    ## 97   89                       Muk   Poison            500 105    105      75
    ## 98   90                  Shellder    Water            305  30     65     100
    ## 99   91                  Cloyster    Water      Ice   525  50     95     180
    ## 100  92                    Gastly    Ghost   Poison   310  30     35      30
    ## 101  93                   Haunter    Ghost   Poison   405  45     50      45
    ## 102  94                    Gengar    Ghost   Poison   500  60     65      60
    ## 103  94         GengarMega Gengar    Ghost   Poison   600  60     65      80
    ## 104  95                      Onix     Rock   Ground   385  35     45     160
    ## 105  96                   Drowzee  Psychic            328  60     48      45
    ## 106  97                     Hypno  Psychic            483  85     73      70
    ## 107  98                    Krabby    Water            325  30    105      90
    ## 108  99                   Kingler    Water            475  55    130     115
    ## 109 100                   Voltorb Electric            330  40     30      50
    ## 110 101                 Electrode Electric            480  60     50      70
    ## 111 102                 Exeggcute    Grass  Psychic   325  60     40      80
    ## 112 103                 Exeggutor    Grass  Psychic   520  95     95      85
    ## 113 104                    Cubone   Ground            320  50     50      95
    ## 114 105                   Marowak   Ground            425  60     80     110
    ## 115 106                 Hitmonlee Fighting            455  50    120      53
    ## 116 107                Hitmonchan Fighting            455  50    105      79
    ## 117 108                 Lickitung   Normal            385  90     55      75
    ## 118 109                   Koffing   Poison            340  40     65      95
    ## 119 110                   Weezing   Poison            490  65     90     120
    ## 120 111                   Rhyhorn   Ground     Rock   345  80     85      95
    ## 121 112                    Rhydon   Ground     Rock   485 105    130     120
    ## 122 113                   Chansey   Normal            450 250      5       5
    ## 123 114                   Tangela    Grass            435  65     55     115
    ## 124 115                Kangaskhan   Normal            490 105     95      80
    ## 125 115 KangaskhanMega Kangaskhan   Normal            590 105    125     100
    ## 126 116                    Horsea    Water            295  30     40      70
    ## 127 117                    Seadra    Water            440  55     65      95
    ## 128 118                   Goldeen    Water            320  45     67      60
    ## 129 119                   Seaking    Water            450  80     92      65
    ## 130 120                    Staryu    Water            340  30     45      55
    ## 131 121                   Starmie    Water  Psychic   520  60     75      85
    ## 132 122                  Mr. Mime  Psychic    Fairy   460  40     45      65
    ## 133 123                   Scyther      Bug   Flying   500  70    110      80
    ## 134 124                      Jynx      Ice  Psychic   455  65     50      35
    ## 135 125                Electabuzz Electric            490  65     83      57
    ## 136 126                    Magmar     Fire            495  65     95      57
    ## 137 127                    Pinsir      Bug            500  65    125     100
    ## 138 127         PinsirMega Pinsir      Bug   Flying   600  65    155     120
    ## 139 128                    Tauros   Normal            490  75    100      95
    ## 140 129                  Magikarp    Water            200  20     10      55
    ## 141 130                  Gyarados    Water   Flying   540  95    125      79
    ## 142 130     GyaradosMega Gyarados    Water     Dark   640  95    155     109
    ## 143 131                    Lapras    Water      Ice   535 130     85      80
    ## 144 132                     Ditto   Normal            288  48     48      48
    ## 145 133                     Eevee   Normal            325  55     55      50
    ## 146 134                  Vaporeon    Water            525 130     65      60
    ## 147 135                   Jolteon Electric            525  65     65      60
    ## 148 136                   Flareon     Fire            525  65    130      60
    ## 149 137                   Porygon   Normal            395  65     60      70
    ## 150 138                   Omanyte     Rock    Water   355  35     40     100
    ## 151 139                   Omastar     Rock    Water   495  70     60     125
    ## 152 140                    Kabuto     Rock    Water   355  30     80      90
    ## 153 141                  Kabutops     Rock    Water   495  60    115     105
    ## 154 142                Aerodactyl     Rock   Flying   515  80    105      65
    ## 155 142 AerodactylMega Aerodactyl     Rock   Flying   615  80    135      85
    ## 156 143                   Snorlax   Normal            540 160    110      65
    ## 157 144                  Articuno      Ice   Flying   580  90     85     100
    ## 158 145                    Zapdos Electric   Flying   580  90     90      85
    ## 159 146                   Moltres     Fire   Flying   580  90    100      90
    ## 160 147                   Dratini   Dragon            300  41     64      45
    ## 161 148                 Dragonair   Dragon            420  61     84      65
    ## 162 149                 Dragonite   Dragon   Flying   600  91    134      95
    ## 163 150                    Mewtwo  Psychic            680 106    110      90
    ## 164 150       MewtwoMega Mewtwo X  Psychic Fighting   780 106    190     100
    ## 165 150       MewtwoMega Mewtwo Y  Psychic            780 106    150      70
    ## 166 151                       Mew  Psychic            600 100    100     100
    ## 167 152                 Chikorita    Grass            318  45     49      65
    ## 168 153                   Bayleef    Grass            405  60     62      80
    ## 169 154                  Meganium    Grass            525  80     82     100
    ## 170 155                 Cyndaquil     Fire            309  39     52      43
    ## 171 156                   Quilava     Fire            405  58     64      58
    ## 172 157                Typhlosion     Fire            534  78     84      78
    ## 173 158                  Totodile    Water            314  50     65      64
    ## 174 159                  Croconaw    Water            405  65     80      80
    ## 175 160                Feraligatr    Water            530  85    105     100
    ## 176 161                   Sentret   Normal            215  35     46      34
    ## 177 162                    Furret   Normal            415  85     76      64
    ## 178 163                  Hoothoot   Normal   Flying   262  60     30      30
    ## 179 164                   Noctowl   Normal   Flying   442 100     50      50
    ## 180 165                    Ledyba      Bug   Flying   265  40     20      30
    ## 181 166                    Ledian      Bug   Flying   390  55     35      50
    ## 182 167                  Spinarak      Bug   Poison   250  40     60      40
    ## 183 168                   Ariados      Bug   Poison   390  70     90      70
    ## 184 169                    Crobat   Poison   Flying   535  85     90      80
    ## 185 170                  Chinchou    Water Electric   330  75     38      38
    ## 186 171                   Lanturn    Water Electric   460 125     58      58
    ## 187 172                     Pichu Electric            205  20     40      15
    ## 188 173                    Cleffa    Fairy            218  50     25      28
    ## 189 174                 Igglybuff   Normal    Fairy   210  90     30      15
    ## 190 175                    Togepi    Fairy            245  35     20      65
    ## 191 176                   Togetic    Fairy   Flying   405  55     40      85
    ## 192 177                      Natu  Psychic   Flying   320  40     50      45
    ## 193 178                      Xatu  Psychic   Flying   470  65     75      70
    ## 194 179                    Mareep Electric            280  55     40      40
    ## 195 180                   Flaaffy Electric            365  70     55      55
    ## 196 181                  Ampharos Electric            510  90     75      85
    ## 197 181     AmpharosMega Ampharos Electric   Dragon   610  90     95     105
    ## 198 182                 Bellossom    Grass            490  75     80      95
    ## 199 183                    Marill    Water    Fairy   250  70     20      50
    ## 200 184                 Azumarill    Water    Fairy   420 100     50      80
    ## 201 185                 Sudowoodo     Rock            410  70    100     115
    ## 202 186                  Politoed    Water            500  90     75      75
    ## 203 187                    Hoppip    Grass   Flying   250  35     35      40
    ## 204 188                  Skiploom    Grass   Flying   340  55     45      50
    ## 205 189                  Jumpluff    Grass   Flying   460  75     55      70
    ## 206 190                     Aipom   Normal            360  55     70      55
    ## 207 191                   Sunkern    Grass            180  30     30      30
    ## 208 192                  Sunflora    Grass            425  75     75      55
    ## 209 193                     Yanma      Bug   Flying   390  65     65      45
    ## 210 194                    Wooper    Water   Ground   210  55     45      45
    ## 211 195                  Quagsire    Water   Ground   430  95     85      85
    ## 212 196                    Espeon  Psychic            525  65     65      60
    ## 213 197                   Umbreon     Dark            525  95     65     110
    ## 214 198                   Murkrow     Dark   Flying   405  60     85      42
    ## 215 199                  Slowking    Water  Psychic   490  95     75      80
    ## 216 200                Misdreavus    Ghost            435  60     60      60
    ## 217 201                     Unown  Psychic            336  48     72      48
    ## 218 202                 Wobbuffet  Psychic            405 190     33      58
    ## 219 203                 Girafarig   Normal  Psychic   455  70     80      65
    ## 220 204                    Pineco      Bug            290  50     65      90
    ## 221 205                Forretress      Bug    Steel   465  75     90     140
    ## 222 206                 Dunsparce   Normal            415 100     70      70
    ## 223 207                    Gligar   Ground   Flying   430  65     75     105
    ## 224 208                   Steelix    Steel   Ground   510  75     85     200
    ## 225 208       SteelixMega Steelix    Steel   Ground   610  75    125     230
    ## 226 209                  Snubbull    Fairy            300  60     80      50
    ## 227 210                  Granbull    Fairy            450  90    120      75
    ## 228 211                  Qwilfish    Water   Poison   430  65     95      75
    ## 229 212                    Scizor      Bug    Steel   500  70    130     100
    ## 230 212         ScizorMega Scizor      Bug    Steel   600  70    150     140
    ## 231 213                   Shuckle      Bug     Rock   505  20     10     230
    ## 232 214                 Heracross      Bug Fighting   500  80    125      75
    ## 233 214   HeracrossMega Heracross      Bug Fighting   600  80    185     115
    ## 234 215                   Sneasel     Dark      Ice   430  55     95      55
    ## 235 216                 Teddiursa   Normal            330  60     80      50
    ## 236 217                  Ursaring   Normal            500  90    130      75
    ## 237 218                    Slugma     Fire            250  40     40      40
    ## 238 219                  Magcargo     Fire     Rock   410  50     50     120
    ## 239 220                    Swinub      Ice   Ground   250  50     50      40
    ## 240 221                 Piloswine      Ice   Ground   450 100    100      80
    ## 241 222                   Corsola    Water     Rock   380  55     55      85
    ## 242 223                  Remoraid    Water            300  35     65      35
    ## 243 224                 Octillery    Water            480  75    105      75
    ## 244 225                  Delibird      Ice   Flying   330  45     55      45
    ## 245 226                   Mantine    Water   Flying   465  65     40      70
    ## 246 227                  Skarmory    Steel   Flying   465  65     80     140
    ## 247 228                  Houndour     Dark     Fire   330  45     60      30
    ## 248 229                  Houndoom     Dark     Fire   500  75     90      50
    ## 249 229     HoundoomMega Houndoom     Dark     Fire   600  75     90      90
    ## 250 230                   Kingdra    Water   Dragon   540  75     95      95
    ## 251 231                    Phanpy   Ground            330  90     60      60
    ## 252 232                   Donphan   Ground            500  90    120     120
    ## 253 233                  Porygon2   Normal            515  85     80      90
    ## 254 234                  Stantler   Normal            465  73     95      62
    ## 255 235                  Smeargle   Normal            250  55     20      35
    ## 256 236                   Tyrogue Fighting            210  35     35      35
    ## 257 237                 Hitmontop Fighting            455  50     95      95
    ## 258 238                  Smoochum      Ice  Psychic   305  45     30      15
    ## 259 239                    Elekid Electric            360  45     63      37
    ## 260 240                     Magby     Fire            365  45     75      37
    ## 261 241                   Miltank   Normal            490  95     80     105
    ## 262 242                   Blissey   Normal            540 255     10      10
    ## 263 243                    Raikou Electric            580  90     85      75
    ## 264 244                     Entei     Fire            580 115    115      85
    ## 265 245                   Suicune    Water            580 100     75     115
    ## 266 246                  Larvitar     Rock   Ground   300  50     64      50
    ## 267 247                   Pupitar     Rock   Ground   410  70     84      70
    ## 268 248                 Tyranitar     Rock     Dark   600 100    134     110
    ## 269 248   TyranitarMega Tyranitar     Rock     Dark   700 100    164     150
    ## 270 249                     Lugia  Psychic   Flying   680 106     90     130
    ## 271 250                     Ho-oh     Fire   Flying   680 106    130      90
    ## 272 251                    Celebi  Psychic    Grass   600 100    100     100
    ## 273 252                   Treecko    Grass            310  40     45      35
    ## 274 253                   Grovyle    Grass            405  50     65      45
    ## 275 254                  Sceptile    Grass            530  70     85      65
    ## 276 254     SceptileMega Sceptile    Grass   Dragon   630  70    110      75
    ## 277 255                   Torchic     Fire            310  45     60      40
    ## 278 256                 Combusken     Fire Fighting   405  60     85      60
    ## 279 257                  Blaziken     Fire Fighting   530  80    120      70
    ## 280 257     BlazikenMega Blaziken     Fire Fighting   630  80    160      80
    ## 281 258                    Mudkip    Water            310  50     70      50
    ## 282 259                 Marshtomp    Water   Ground   405  70     85      70
    ## 283 260                  Swampert    Water   Ground   535 100    110      90
    ## 284 260     SwampertMega Swampert    Water   Ground   635 100    150     110
    ## 285 261                 Poochyena     Dark            220  35     55      35
    ## 286 262                 Mightyena     Dark            420  70     90      70
    ## 287 263                 Zigzagoon   Normal            240  38     30      41
    ## 288 264                   Linoone   Normal            420  78     70      61
    ## 289 265                   Wurmple      Bug            195  45     45      35
    ## 290 266                   Silcoon      Bug            205  50     35      55
    ## 291 267                 Beautifly      Bug   Flying   395  60     70      50
    ## 292 268                   Cascoon      Bug            205  50     35      55
    ## 293 269                    Dustox      Bug   Poison   385  60     50      70
    ## 294 270                     Lotad    Water    Grass   220  40     30      30
    ## 295 271                    Lombre    Water    Grass   340  60     50      50
    ## 296 272                  Ludicolo    Water    Grass   480  80     70      70
    ## 297 273                    Seedot    Grass            220  40     40      50
    ## 298 274                   Nuzleaf    Grass     Dark   340  70     70      40
    ## 299 275                   Shiftry    Grass     Dark   480  90    100      60
    ## 300 276                   Taillow   Normal   Flying   270  40     55      30
    ## 301 277                   Swellow   Normal   Flying   430  60     85      60
    ## 302 278                   Wingull    Water   Flying   270  40     30      30
    ## 303 279                  Pelipper    Water   Flying   430  60     50     100
    ## 304 280                     Ralts  Psychic    Fairy   198  28     25      25
    ## 305 281                    Kirlia  Psychic    Fairy   278  38     35      35
    ## 306 282                 Gardevoir  Psychic    Fairy   518  68     65      65
    ## 307 282   GardevoirMega Gardevoir  Psychic    Fairy   618  68     85      65
    ## 308 283                   Surskit      Bug    Water   269  40     30      32
    ## 309 284                Masquerain      Bug   Flying   414  70     60      62
    ## 310 285                 Shroomish    Grass            295  60     40      60
    ## 311 286                   Breloom    Grass Fighting   460  60    130      80
    ## 312 287                   Slakoth   Normal            280  60     60      60
    ## 313 288                  Vigoroth   Normal            440  80     80      80
    ## 314 289                   Slaking   Normal            670 150    160     100
    ## 315 290                   Nincada      Bug   Ground   266  31     45      90
    ## 316 291                   Ninjask      Bug   Flying   456  61     90      45
    ## 317 292                  Shedinja      Bug    Ghost   236   1     90      45
    ## 318 293                   Whismur   Normal            240  64     51      23
    ## 319 294                   Loudred   Normal            360  84     71      43
    ## 320 295                   Exploud   Normal            490 104     91      63
    ## 321 296                  Makuhita Fighting            237  72     60      30
    ## 322 297                  Hariyama Fighting            474 144    120      60
    ## 323 298                   Azurill   Normal    Fairy   190  50     20      40
    ## 324 299                  Nosepass     Rock            375  30     45     135
    ## 325 300                    Skitty   Normal            260  50     45      45
    ## 326 301                  Delcatty   Normal            380  70     65      65
    ## 327 302                   Sableye     Dark    Ghost   380  50     75      75
    ## 328 302       SableyeMega Sableye     Dark    Ghost   480  50     85     125
    ## 329 303                    Mawile    Steel    Fairy   380  50     85      85
    ## 330 303         MawileMega Mawile    Steel    Fairy   480  50    105     125
    ## 331 304                      Aron    Steel     Rock   330  50     70     100
    ## 332 305                    Lairon    Steel     Rock   430  60     90     140
    ## 333 306                    Aggron    Steel     Rock   530  70    110     180
    ## 334 306         AggronMega Aggron    Steel            630  70    140     230
    ## 335 307                  Meditite Fighting  Psychic   280  30     40      55
    ## 336 308                  Medicham Fighting  Psychic   410  60     60      75
    ## 337 308     MedichamMega Medicham Fighting  Psychic   510  60    100      85
    ## 338 309                 Electrike Electric            295  40     45      40
    ## 339 310                 Manectric Electric            475  70     75      60
    ## 340 310   ManectricMega Manectric Electric            575  70     75      80
    ## 341 311                    Plusle Electric            405  60     50      40
    ## 342 312                     Minun Electric            405  60     40      50
    ## 343 313                   Volbeat      Bug            400  65     73      55
    ## 344 314                  Illumise      Bug            400  65     47      55
    ## 345 315                   Roselia    Grass   Poison   400  50     60      45
    ## 346 316                    Gulpin   Poison            302  70     43      53
    ## 347 317                    Swalot   Poison            467 100     73      83
    ## 348 318                  Carvanha    Water     Dark   305  45     90      20
    ## 349 319                  Sharpedo    Water     Dark   460  70    120      40
    ## 350 319     SharpedoMega Sharpedo    Water     Dark   560  70    140      70
    ## 351 320                   Wailmer    Water            400 130     70      35
    ## 352 321                   Wailord    Water            500 170     90      45
    ## 353 322                     Numel     Fire   Ground   305  60     60      40
    ## 354 323                  Camerupt     Fire   Ground   460  70    100      70
    ## 355 323     CameruptMega Camerupt     Fire   Ground   560  70    120     100
    ## 356 324                   Torkoal     Fire            470  70     85     140
    ## 357 325                    Spoink  Psychic            330  60     25      35
    ## 358 326                   Grumpig  Psychic            470  80     45      65
    ## 359 327                    Spinda   Normal            360  60     60      60
    ## 360 328                  Trapinch   Ground            290  45    100      45
    ## 361 329                   Vibrava   Ground   Dragon   340  50     70      50
    ## 362 330                    Flygon   Ground   Dragon   520  80    100      80
    ## 363 331                    Cacnea    Grass            335  50     85      40
    ## 364 332                  Cacturne    Grass     Dark   475  70    115      60
    ## 365 333                    Swablu   Normal   Flying   310  45     40      60
    ## 366 334                   Altaria   Dragon   Flying   490  75     70      90
    ## 367 334       AltariaMega Altaria   Dragon    Fairy   590  75    110     110
    ## 368 335                  Zangoose   Normal            458  73    115      60
    ## 369 336                   Seviper   Poison            458  73    100      60
    ## 370 337                  Lunatone     Rock  Psychic   440  70     55      65
    ## 371 338                   Solrock     Rock  Psychic   440  70     95      85
    ## 372 339                  Barboach    Water   Ground   288  50     48      43
    ## 373 340                  Whiscash    Water   Ground   468 110     78      73
    ## 374 341                  Corphish    Water            308  43     80      65
    ## 375 342                 Crawdaunt    Water     Dark   468  63    120      85
    ## 376 343                    Baltoy   Ground  Psychic   300  40     40      55
    ## 377 344                   Claydol   Ground  Psychic   500  60     70     105
    ## 378 345                    Lileep     Rock    Grass   355  66     41      77
    ## 379 346                   Cradily     Rock    Grass   495  86     81      97
    ## 380 347                   Anorith     Rock      Bug   355  45     95      50
    ## 381 348                   Armaldo     Rock      Bug   495  75    125     100
    ## 382 349                    Feebas    Water            200  20     15      20
    ## 383 350                   Milotic    Water            540  95     60      79
    ## 384 351                  Castform   Normal            420  70     70      70
    ## 385 352                   Kecleon   Normal            440  60     90      70
    ## 386 353                   Shuppet    Ghost            295  44     75      35
    ## 387 354                   Banette    Ghost            455  64    115      65
    ## 388 354       BanetteMega Banette    Ghost            555  64    165      75
    ## 389 355                   Duskull    Ghost            295  20     40      90
    ## 390 356                  Dusclops    Ghost            455  40     70     130
    ## 391 357                   Tropius    Grass   Flying   460  99     68      83
    ## 392 358                  Chimecho  Psychic            425  65     50      70
    ## 393 359                     Absol     Dark            465  65    130      60
    ## 394 359           AbsolMega Absol     Dark            565  65    150      60
    ## 395 360                    Wynaut  Psychic            260  95     23      48
    ## 396 361                   Snorunt      Ice            300  50     50      50
    ## 397 362                    Glalie      Ice            480  80     80      80
    ## 398 362         GlalieMega Glalie      Ice            580  80    120      80
    ## 399 363                    Spheal      Ice    Water   290  70     40      50
    ## 400 364                    Sealeo      Ice    Water   410  90     60      70
    ## 401 365                   Walrein      Ice    Water   530 110     80      90
    ## 402 366                  Clamperl    Water            345  35     64      85
    ## 403 367                   Huntail    Water            485  55    104     105
    ## 404 368                  Gorebyss    Water            485  55     84     105
    ## 405 369                 Relicanth    Water     Rock   485 100     90     130
    ## 406 370                   Luvdisc    Water            330  43     30      55
    ## 407 371                     Bagon   Dragon            300  45     75      60
    ## 408 372                   Shelgon   Dragon            420  65     95     100
    ## 409 373                 Salamence   Dragon   Flying   600  95    135      80
    ## 410 373   SalamenceMega Salamence   Dragon   Flying   700  95    145     130
    ## 411 374                    Beldum    Steel  Psychic   300  40     55      80
    ## 412 375                    Metang    Steel  Psychic   420  60     75     100
    ## 413 376                 Metagross    Steel  Psychic   600  80    135     130
    ## 414 376   MetagrossMega Metagross    Steel  Psychic   700  80    145     150
    ## 415 377                  Regirock     Rock            580  80    100     200
    ## 416 378                    Regice      Ice            580  80     50     100
    ## 417 379                 Registeel    Steel            580  80     75     150
    ## 418 380                    Latias   Dragon  Psychic   600  80     80      90
    ## 419 380         LatiasMega Latias   Dragon  Psychic   700  80    100     120
    ## 420 381                    Latios   Dragon  Psychic   600  80     90      80
    ## 421 381         LatiosMega Latios   Dragon  Psychic   700  80    130     100
    ## 422 382                    Kyogre    Water            670 100    100      90
    ## 423 382       KyogrePrimal Kyogre    Water            770 100    150      90
    ## 424 383                   Groudon   Ground            670 100    150     140
    ## 425 383     GroudonPrimal Groudon   Ground     Fire   770 100    180     160
    ## 426 384                  Rayquaza   Dragon   Flying   680 105    150      90
    ## 427 384     RayquazaMega Rayquaza   Dragon   Flying   780 105    180     100
    ## 428 385                   Jirachi    Steel  Psychic   600 100    100     100
    ## 429 386        DeoxysNormal Forme  Psychic            600  50    150      50
    ## 430 386        DeoxysAttack Forme  Psychic            600  50    180      20
    ## 431 386       DeoxysDefense Forme  Psychic            600  50     70     160
    ## 432 386         DeoxysSpeed Forme  Psychic            600  50     95      90
    ## 433 387                   Turtwig    Grass            318  55     68      64
    ## 434 388                    Grotle    Grass            405  75     89      85
    ## 435 389                  Torterra    Grass   Ground   525  95    109     105
    ## 436 390                  Chimchar     Fire            309  44     58      44
    ## 437 391                  Monferno     Fire Fighting   405  64     78      52
    ## 438 392                 Infernape     Fire Fighting   534  76    104      71
    ## 439 393                    Piplup    Water            314  53     51      53
    ## 440 394                  Prinplup    Water            405  64     66      68
    ## 441 395                  Empoleon    Water    Steel   530  84     86      88
    ## 442 396                    Starly   Normal   Flying   245  40     55      30
    ## 443 397                  Staravia   Normal   Flying   340  55     75      50
    ## 444 398                 Staraptor   Normal   Flying   485  85    120      70
    ## 445 399                    Bidoof   Normal            250  59     45      40
    ## 446 400                   Bibarel   Normal    Water   410  79     85      60
    ## 447 401                 Kricketot      Bug            194  37     25      41
    ## 448 402                Kricketune      Bug            384  77     85      51
    ## 449 403                     Shinx Electric            263  45     65      34
    ## 450 404                     Luxio Electric            363  60     85      49
    ## 451 405                    Luxray Electric            523  80    120      79
    ## 452 406                     Budew    Grass   Poison   280  40     30      35
    ## 453 407                  Roserade    Grass   Poison   515  60     70      65
    ## 454 408                  Cranidos     Rock            350  67    125      40
    ## 455 409                 Rampardos     Rock            495  97    165      60
    ## 456 410                  Shieldon     Rock    Steel   350  30     42     118
    ## 457 411                 Bastiodon     Rock    Steel   495  60     52     168
    ## 458 412                     Burmy      Bug            224  40     29      45
    ## 459 413       WormadamPlant Cloak      Bug    Grass   424  60     59      85
    ## 460 413       WormadamSandy Cloak      Bug   Ground   424  60     79     105
    ## 461 413       WormadamTrash Cloak      Bug    Steel   424  60     69      95
    ## 462 414                    Mothim      Bug   Flying   424  70     94      50
    ## 463 415                    Combee      Bug   Flying   244  30     30      42
    ## 464 416                 Vespiquen      Bug   Flying   474  70     80     102
    ## 465 417                 Pachirisu Electric            405  60     45      70
    ## 466 418                    Buizel    Water            330  55     65      35
    ## 467 419                  Floatzel    Water            495  85    105      55
    ## 468 420                   Cherubi    Grass            275  45     35      45
    ## 469 421                   Cherrim    Grass            450  70     60      70
    ## 470 422                   Shellos    Water            325  76     48      48
    ## 471 423                 Gastrodon    Water   Ground   475 111     83      68
    ## 472 424                   Ambipom   Normal            482  75    100      66
    ## 473 425                  Drifloon    Ghost   Flying   348  90     50      34
    ## 474 426                  Drifblim    Ghost   Flying   498 150     80      44
    ## 475 427                   Buneary   Normal            350  55     66      44
    ## 476 428                   Lopunny   Normal            480  65     76      84
    ## 477 428       LopunnyMega Lopunny   Normal Fighting   580  65    136      94
    ## 478 429                 Mismagius    Ghost            495  60     60      60
    ## 479 430                 Honchkrow     Dark   Flying   505 100    125      52
    ## 480 431                   Glameow   Normal            310  49     55      42
    ## 481 432                   Purugly   Normal            452  71     82      64
    ## 482 433                 Chingling  Psychic            285  45     30      50
    ## 483 434                    Stunky   Poison     Dark   329  63     63      47
    ## 484 435                  Skuntank   Poison     Dark   479 103     93      67
    ## 485 436                   Bronzor    Steel  Psychic   300  57     24      86
    ## 486 437                  Bronzong    Steel  Psychic   500  67     89     116
    ## 487 438                    Bonsly     Rock            290  50     80      95
    ## 488 439                  Mime Jr.  Psychic    Fairy   310  20     25      45
    ## 489 440                   Happiny   Normal            220 100      5       5
    ## 490 441                    Chatot   Normal   Flying   411  76     65      45
    ## 491 442                 Spiritomb    Ghost     Dark   485  50     92     108
    ## 492 443                     Gible   Dragon   Ground   300  58     70      45
    ## 493 444                    Gabite   Dragon   Ground   410  68     90      65
    ## 494 445                  Garchomp   Dragon   Ground   600 108    130      95
    ## 495 445     GarchompMega Garchomp   Dragon   Ground   700 108    170     115
    ## 496 446                  Munchlax   Normal            390 135     85      40
    ## 497 447                     Riolu Fighting            285  40     70      40
    ## 498 448                   Lucario Fighting    Steel   525  70    110      70
    ## 499 448       LucarioMega Lucario Fighting    Steel   625  70    145      88
    ## 500 449                Hippopotas   Ground            330  68     72      78
    ## 501 450                 Hippowdon   Ground            525 108    112     118
    ## 502 451                   Skorupi   Poison      Bug   330  40     50      90
    ## 503 452                   Drapion   Poison     Dark   500  70     90     110
    ## 504 453                  Croagunk   Poison Fighting   300  48     61      40
    ## 505 454                 Toxicroak   Poison Fighting   490  83    106      65
    ## 506 455                 Carnivine    Grass            454  74    100      72
    ## 507 456                   Finneon    Water            330  49     49      56
    ## 508 457                  Lumineon    Water            460  69     69      76
    ## 509 458                   Mantyke    Water   Flying   345  45     20      50
    ## 510 459                    Snover    Grass      Ice   334  60     62      50
    ## 511 460                 Abomasnow    Grass      Ice   494  90     92      75
    ## 512 460   AbomasnowMega Abomasnow    Grass      Ice   594  90    132     105
    ## 513 461                   Weavile     Dark      Ice   510  70    120      65
    ## 514 462                 Magnezone Electric    Steel   535  70     70     115
    ## 515 463                Lickilicky   Normal            515 110     85      95
    ## 516 464                 Rhyperior   Ground     Rock   535 115    140     130
    ## 517 465                 Tangrowth    Grass            535 100    100     125
    ## 518 466                Electivire Electric            540  75    123      67
    ## 519 467                 Magmortar     Fire            540  75     95      67
    ## 520 468                  Togekiss    Fairy   Flying   545  85     50      95
    ## 521 469                   Yanmega      Bug   Flying   515  86     76      86
    ## 522 470                   Leafeon    Grass            525  65    110     130
    ## 523 471                   Glaceon      Ice            525  65     60     110
    ## 524 472                   Gliscor   Ground   Flying   510  75     95     125
    ## 525 473                 Mamoswine      Ice   Ground   530 110    130      80
    ## 526 474                 Porygon-Z   Normal            535  85     80      70
    ## 527 475                   Gallade  Psychic Fighting   518  68    125      65
    ## 528 475       GalladeMega Gallade  Psychic Fighting   618  68    165      95
    ## 529 476                 Probopass     Rock    Steel   525  60     55     145
    ## 530 477                  Dusknoir    Ghost            525  45    100     135
    ## 531 478                  Froslass      Ice    Ghost   480  70     80      70
    ## 532 479                     Rotom Electric    Ghost   440  50     50      77
    ## 533 479           RotomHeat Rotom Electric     Fire   520  50     65     107
    ## 534 479           RotomWash Rotom Electric    Water   520  50     65     107
    ## 535 479          RotomFrost Rotom Electric      Ice   520  50     65     107
    ## 536 479            RotomFan Rotom Electric   Flying   520  50     65     107
    ## 537 479            RotomMow Rotom Electric    Grass   520  50     65     107
    ## 538 480                      Uxie  Psychic            580  75     75     130
    ## 539 481                   Mesprit  Psychic            580  80    105     105
    ## 540 482                     Azelf  Psychic            580  75    125      70
    ## 541 483                    Dialga    Steel   Dragon   680 100    120     120
    ## 542 484                    Palkia    Water   Dragon   680  90    120     100
    ## 543 485                   Heatran     Fire    Steel   600  91     90     106
    ## 544 486                 Regigigas   Normal            670 110    160     110
    ## 545 487     GiratinaAltered Forme    Ghost   Dragon   680 150    100     120
    ## 546 487      GiratinaOrigin Forme    Ghost   Dragon   680 150    120     100
    ## 547 488                 Cresselia  Psychic            600 120     70     120
    ## 548 489                    Phione    Water            480  80     80      80
    ## 549 490                   Manaphy    Water            600 100    100     100
    ## 550 491                   Darkrai     Dark            600  70     90      90
    ## 551 492         ShayminLand Forme    Grass            600 100    100     100
    ## 552 492          ShayminSky Forme    Grass   Flying   600 100    103      75
    ## 553 493                    Arceus   Normal            720 120    120     120
    ## 554 494                   Victini  Psychic     Fire   600 100    100     100
    ## 555 495                     Snivy    Grass            308  45     45      55
    ## 556 496                   Servine    Grass            413  60     60      75
    ## 557 497                 Serperior    Grass            528  75     75      95
    ## 558 498                     Tepig     Fire            308  65     63      45
    ## 559 499                   Pignite     Fire Fighting   418  90     93      55
    ## 560 500                    Emboar     Fire Fighting   528 110    123      65
    ## 561 501                  Oshawott    Water            308  55     55      45
    ## 562 502                    Dewott    Water            413  75     75      60
    ## 563 503                  Samurott    Water            528  95    100      85
    ## 564 504                    Patrat   Normal            255  45     55      39
    ## 565 505                   Watchog   Normal            420  60     85      69
    ## 566 506                  Lillipup   Normal            275  45     60      45
    ## 567 507                   Herdier   Normal            370  65     80      65
    ## 568 508                 Stoutland   Normal            500  85    110      90
    ## 569 509                  Purrloin     Dark            281  41     50      37
    ## 570 510                   Liepard     Dark            446  64     88      50
    ## 571 511                   Pansage    Grass            316  50     53      48
    ## 572 512                  Simisage    Grass            498  75     98      63
    ## 573 513                   Pansear     Fire            316  50     53      48
    ## 574 514                  Simisear     Fire            498  75     98      63
    ## 575 515                   Panpour    Water            316  50     53      48
    ## 576 516                  Simipour    Water            498  75     98      63
    ## 577 517                     Munna  Psychic            292  76     25      45
    ## 578 518                  Musharna  Psychic            487 116     55      85
    ## 579 519                    Pidove   Normal   Flying   264  50     55      50
    ## 580 520                 Tranquill   Normal   Flying   358  62     77      62
    ## 581 521                  Unfezant   Normal   Flying   488  80    115      80
    ## 582 522                   Blitzle Electric            295  45     60      32
    ## 583 523                 Zebstrika Electric            497  75    100      63
    ## 584 524                Roggenrola     Rock            280  55     75      85
    ## 585 525                   Boldore     Rock            390  70    105     105
    ## 586 526                  Gigalith     Rock            515  85    135     130
    ## 587 527                    Woobat  Psychic   Flying   313  55     45      43
    ## 588 528                   Swoobat  Psychic   Flying   425  67     57      55
    ## 589 529                   Drilbur   Ground            328  60     85      40
    ## 590 530                 Excadrill   Ground    Steel   508 110    135      60
    ## 591 531                    Audino   Normal            445 103     60      86
    ## 592 531         AudinoMega Audino   Normal    Fairy   545 103     60     126
    ## 593 532                   Timburr Fighting            305  75     80      55
    ## 594 533                   Gurdurr Fighting            405  85    105      85
    ## 595 534                Conkeldurr Fighting            505 105    140      95
    ## 596 535                   Tympole    Water            294  50     50      40
    ## 597 536                 Palpitoad    Water   Ground   384  75     65      55
    ## 598 537                Seismitoad    Water   Ground   509 105     95      75
    ## 599 538                     Throh Fighting            465 120    100      85
    ## 600 539                      Sawk Fighting            465  75    125      75
    ## 601 540                  Sewaddle      Bug    Grass   310  45     53      70
    ## 602 541                  Swadloon      Bug    Grass   380  55     63      90
    ## 603 542                  Leavanny      Bug    Grass   500  75    103      80
    ## 604 543                  Venipede      Bug   Poison   260  30     45      59
    ## 605 544                Whirlipede      Bug   Poison   360  40     55      99
    ## 606 545                 Scolipede      Bug   Poison   485  60    100      89
    ## 607 546                  Cottonee    Grass    Fairy   280  40     27      60
    ## 608 547                Whimsicott    Grass    Fairy   480  60     67      85
    ## 609 548                   Petilil    Grass            280  45     35      50
    ## 610 549                 Lilligant    Grass            480  70     60      75
    ## 611 550                  Basculin    Water            460  70     92      65
    ## 612 551                   Sandile   Ground     Dark   292  50     72      35
    ## 613 552                  Krokorok   Ground     Dark   351  60     82      45
    ## 614 553                Krookodile   Ground     Dark   519  95    117      80
    ## 615 554                  Darumaka     Fire            315  70     90      45
    ## 616 555   DarmanitanStandard Mode     Fire            480 105    140      55
    ## 617 555        DarmanitanZen Mode     Fire  Psychic   540 105     30     105
    ## 618 556                  Maractus    Grass            461  75     86      67
    ## 619 557                   Dwebble      Bug     Rock   325  50     65      85
    ## 620 558                   Crustle      Bug     Rock   475  70     95     125
    ## 621 559                   Scraggy     Dark Fighting   348  50     75      70
    ## 622 560                   Scrafty     Dark Fighting   488  65     90     115
    ## 623 561                  Sigilyph  Psychic   Flying   490  72     58      80
    ## 624 562                    Yamask    Ghost            303  38     30      85
    ## 625 563                Cofagrigus    Ghost            483  58     50     145
    ## 626 564                  Tirtouga    Water     Rock   355  54     78     103
    ## 627 565                Carracosta    Water     Rock   495  74    108     133
    ## 628 566                    Archen     Rock   Flying   401  55    112      45
    ## 629 567                  Archeops     Rock   Flying   567  75    140      65
    ## 630 568                  Trubbish   Poison            329  50     50      62
    ## 631 569                  Garbodor   Poison            474  80     95      82
    ## 632 570                     Zorua     Dark            330  40     65      40
    ## 633 571                   Zoroark     Dark            510  60    105      60
    ## 634 572                  Minccino   Normal            300  55     50      40
    ## 635 573                  Cinccino   Normal            470  75     95      60
    ## 636 574                   Gothita  Psychic            290  45     30      50
    ## 637 575                 Gothorita  Psychic            390  60     45      70
    ## 638 576                Gothitelle  Psychic            490  70     55      95
    ## 639 577                   Solosis  Psychic            290  45     30      40
    ## 640 578                   Duosion  Psychic            370  65     40      50
    ## 641 579                 Reuniclus  Psychic            490 110     65      75
    ## 642 580                  Ducklett    Water   Flying   305  62     44      50
    ## 643 581                    Swanna    Water   Flying   473  75     87      63
    ## 644 582                 Vanillite      Ice            305  36     50      50
    ## 645 583                 Vanillish      Ice            395  51     65      65
    ## 646 584                 Vanilluxe      Ice            535  71     95      85
    ## 647 585                  Deerling   Normal    Grass   335  60     60      50
    ## 648 586                  Sawsbuck   Normal    Grass   475  80    100      70
    ## 649 587                    Emolga Electric   Flying   428  55     75      60
    ## 650 588                Karrablast      Bug            315  50     75      45
    ## 651 589                Escavalier      Bug    Steel   495  70    135     105
    ## 652 590                   Foongus    Grass   Poison   294  69     55      45
    ## 653 591                 Amoonguss    Grass   Poison   464 114     85      70
    ## 654 592                  Frillish    Water    Ghost   335  55     40      50
    ## 655 593                 Jellicent    Water    Ghost   480 100     60      70
    ## 656 594                 Alomomola    Water            470 165     75      80
    ## 657 595                    Joltik      Bug Electric   319  50     47      50
    ## 658 596                Galvantula      Bug Electric   472  70     77      60
    ## 659 597                 Ferroseed    Grass    Steel   305  44     50      91
    ## 660 598                Ferrothorn    Grass    Steel   489  74     94     131
    ## 661 599                     Klink    Steel            300  40     55      70
    ## 662 600                     Klang    Steel            440  60     80      95
    ## 663 601                 Klinklang    Steel            520  60    100     115
    ## 664 602                    Tynamo Electric            275  35     55      40
    ## 665 603                 Eelektrik Electric            405  65     85      70
    ## 666 604                Eelektross Electric            515  85    115      80
    ## 667 605                    Elgyem  Psychic            335  55     55      55
    ## 668 606                  Beheeyem  Psychic            485  75     75      75
    ## 669 607                   Litwick    Ghost     Fire   275  50     30      55
    ## 670 608                   Lampent    Ghost     Fire   370  60     40      60
    ## 671 609                Chandelure    Ghost     Fire   520  60     55      90
    ## 672 610                      Axew   Dragon            320  46     87      60
    ## 673 611                   Fraxure   Dragon            410  66    117      70
    ## 674 612                   Haxorus   Dragon            540  76    147      90
    ## 675 613                   Cubchoo      Ice            305  55     70      40
    ## 676 614                   Beartic      Ice            485  95    110      80
    ## 677 615                 Cryogonal      Ice            485  70     50      30
    ## 678 616                   Shelmet      Bug            305  50     40      85
    ## 679 617                  Accelgor      Bug            495  80     70      40
    ## 680 618                  Stunfisk   Ground Electric   471 109     66      84
    ## 681 619                   Mienfoo Fighting            350  45     85      50
    ## 682 620                  Mienshao Fighting            510  65    125      60
    ## 683 621                 Druddigon   Dragon            485  77    120      90
    ## 684 622                    Golett   Ground    Ghost   303  59     74      50
    ## 685 623                    Golurk   Ground    Ghost   483  89    124      80
    ## 686 624                  Pawniard     Dark    Steel   340  45     85      70
    ## 687 625                   Bisharp     Dark    Steel   490  65    125     100
    ## 688 626                Bouffalant   Normal            490  95    110      95
    ## 689 627                   Rufflet   Normal   Flying   350  70     83      50
    ## 690 628                  Braviary   Normal   Flying   510 100    123      75
    ## 691 629                   Vullaby     Dark   Flying   370  70     55      75
    ## 692 630                 Mandibuzz     Dark   Flying   510 110     65     105
    ## 693 631                   Heatmor     Fire            484  85     97      66
    ## 694 632                    Durant      Bug    Steel   484  58    109     112
    ## 695 633                     Deino     Dark   Dragon   300  52     65      50
    ## 696 634                  Zweilous     Dark   Dragon   420  72     85      70
    ## 697 635                 Hydreigon     Dark   Dragon   600  92    105      90
    ## 698 636                  Larvesta      Bug     Fire   360  55     85      55
    ## 699 637                 Volcarona      Bug     Fire   550  85     60      65
    ## 700 638                  Cobalion    Steel Fighting   580  91     90     129
    ## 701 639                 Terrakion     Rock Fighting   580  91    129      90
    ## 702 640                  Virizion    Grass Fighting   580  91     90      72
    ## 703 641   TornadusIncarnate Forme   Flying            580  79    115      70
    ## 704 641     TornadusTherian Forme   Flying            580  79    100      80
    ## 705 642  ThundurusIncarnate Forme Electric   Flying   580  79    115      70
    ## 706 642    ThundurusTherian Forme Electric   Flying   580  79    105      70
    ## 707 643                  Reshiram   Dragon     Fire   680 100    120     100
    ## 708 644                    Zekrom   Dragon Electric   680 100    150     120
    ## 709 645   LandorusIncarnate Forme   Ground   Flying   600  89    125      90
    ## 710 645     LandorusTherian Forme   Ground   Flying   600  89    145      90
    ## 711 646                    Kyurem   Dragon      Ice   660 125    130      90
    ## 712 646        KyuremBlack Kyurem   Dragon      Ice   700 125    170     100
    ## 713 646        KyuremWhite Kyurem   Dragon      Ice   700 125    120      90
    ## 714 647      KeldeoOrdinary Forme    Water Fighting   580  91     72      90
    ## 715 647      KeldeoResolute Forme    Water Fighting   580  91     72      90
    ## 716 648        MeloettaAria Forme   Normal  Psychic   600 100     77      77
    ## 717 648   MeloettaPirouette Forme   Normal Fighting   600 100    128      90
    ## 718 649                  Genesect      Bug    Steel   600  71    120      95
    ## 719 650                   Chespin    Grass            313  56     61      65
    ## 720 651                 Quilladin    Grass            405  61     78      95
    ## 721 652                Chesnaught    Grass Fighting   530  88    107     122
    ## 722 653                  Fennekin     Fire            307  40     45      40
    ## 723 654                   Braixen     Fire            409  59     59      58
    ## 724 655                   Delphox     Fire  Psychic   534  75     69      72
    ## 725 656                   Froakie    Water            314  41     56      40
    ## 726 657                 Frogadier    Water            405  54     63      52
    ## 727 658                  Greninja    Water     Dark   530  72     95      67
    ## 728 659                  Bunnelby   Normal            237  38     36      38
    ## 729 660                 Diggersby   Normal   Ground   423  85     56      77
    ## 730 661                Fletchling   Normal   Flying   278  45     50      43
    ## 731 662               Fletchinder     Fire   Flying   382  62     73      55
    ## 732 663                Talonflame     Fire   Flying   499  78     81      71
    ## 733 664                Scatterbug      Bug            200  38     35      40
    ## 734 665                    Spewpa      Bug            213  45     22      60
    ## 735 666                  Vivillon      Bug   Flying   411  80     52      50
    ## 736 667                    Litleo     Fire   Normal   369  62     50      58
    ## 737 668                    Pyroar     Fire   Normal   507  86     68      72
    ## 738 669                 FlabÃ©bÃ©    Fairy            303  44     38      39
    ## 739 670                   Floette    Fairy            371  54     45      47
    ## 740 671                   Florges    Fairy            552  78     65      68
    ## 741 672                    Skiddo    Grass            350  66     65      48
    ## 742 673                    Gogoat    Grass            531 123    100      62
    ## 743 674                   Pancham Fighting            348  67     82      62
    ## 744 675                   Pangoro Fighting     Dark   495  95    124      78
    ## 745 676                   Furfrou   Normal            472  75     80      60
    ## 746 677                    Espurr  Psychic            355  62     48      54
    ## 747 678              MeowsticMale  Psychic            466  74     48      76
    ## 748 678            MeowsticFemale  Psychic            466  74     48      76
    ## 749 679                   Honedge    Steel    Ghost   325  45     80     100
    ## 750 680                  Doublade    Steel    Ghost   448  59    110     150
    ## 751 681      AegislashBlade Forme    Steel    Ghost   520  60    150      50
    ## 752 681     AegislashShield Forme    Steel    Ghost   520  60     50     150
    ## 753 682                  Spritzee    Fairy            341  78     52      60
    ## 754 683                Aromatisse    Fairy            462 101     72      72
    ## 755 684                   Swirlix    Fairy            341  62     48      66
    ## 756 685                  Slurpuff    Fairy            480  82     80      86
    ## 757 686                     Inkay     Dark  Psychic   288  53     54      53
    ## 758 687                   Malamar     Dark  Psychic   482  86     92      88
    ## 759 688                   Binacle     Rock    Water   306  42     52      67
    ## 760 689                Barbaracle     Rock    Water   500  72    105     115
    ## 761 690                    Skrelp   Poison    Water   320  50     60      60
    ## 762 691                  Dragalge   Poison   Dragon   494  65     75      90
    ## 763 692                 Clauncher    Water            330  50     53      62
    ## 764 693                 Clawitzer    Water            500  71     73      88
    ## 765 694                Helioptile Electric   Normal   289  44     38      33
    ## 766 695                 Heliolisk Electric   Normal   481  62     55      52
    ## 767 696                    Tyrunt     Rock   Dragon   362  58     89      77
    ## 768 697                 Tyrantrum     Rock   Dragon   521  82    121     119
    ## 769 698                    Amaura     Rock      Ice   362  77     59      50
    ## 770 699                   Aurorus     Rock      Ice   521 123     77      72
    ## 771 700                   Sylveon    Fairy            525  95     65      65
    ## 772 701                  Hawlucha Fighting   Flying   500  78     92      75
    ## 773 702                   Dedenne Electric    Fairy   431  67     58      57
    ## 774 703                   Carbink     Rock    Fairy   500  50     50     150
    ## 775 704                     Goomy   Dragon            300  45     50      35
    ## 776 705                   Sliggoo   Dragon            452  68     75      53
    ## 777 706                    Goodra   Dragon            600  90    100      70
    ## 778 707                    Klefki    Steel    Fairy   470  57     80      91
    ## 779 708                  Phantump    Ghost    Grass   309  43     70      48
    ## 780 709                 Trevenant    Ghost    Grass   474  85    110      76
    ## 781 710     PumpkabooAverage Size    Ghost    Grass   335  49     66      70
    ## 782 710       PumpkabooSmall Size    Ghost    Grass   335  44     66      70
    ## 783 710       PumpkabooLarge Size    Ghost    Grass   335  54     66      70
    ## 784 710       PumpkabooSuper Size    Ghost    Grass   335  59     66      70
    ## 785 711     GourgeistAverage Size    Ghost    Grass   494  65     90     122
    ## 786 711       GourgeistSmall Size    Ghost    Grass   494  55     85     122
    ## 787 711       GourgeistLarge Size    Ghost    Grass   494  75     95     122
    ## 788 711       GourgeistSuper Size    Ghost    Grass   494  85    100     122
    ## 789 712                  Bergmite      Ice            304  55     69      85
    ## 790 713                   Avalugg      Ice            514  95    117     184
    ## 791 714                    Noibat   Flying   Dragon   245  40     30      35
    ## 792 715                   Noivern   Flying   Dragon   535  85     70      80
    ## 793 716                   Xerneas    Fairy            680 126    131      95
    ## 794 717                   Yveltal     Dark   Flying   680 126    131      95
    ## 795 718          Zygarde50% Forme   Dragon   Ground   600 108    100     121
    ## 796 719                   Diancie     Rock    Fairy   600  50    100     150
    ## 797 719       DiancieMega Diancie     Rock    Fairy   700  50    160     110
    ## 798 720       HoopaHoopa Confined  Psychic    Ghost   600  80    110      60
    ## 799 720        HoopaHoopa Unbound  Psychic     Dark   680  80    160      60
    ## 800 721                 Volcanion     Fire    Water   600  80    110     120
    ##     Sp..Atk Sp..Def Speed Generation Legendary
    ## 1        65      65    45          1     False
    ## 2        80      80    60          1     False
    ## 3       100     100    80          1     False
    ## 4       122     120    80          1     False
    ## 5        60      50    65          1     False
    ## 6        80      65    80          1     False
    ## 7       109      85   100          1     False
    ## 8       130      85   100          1     False
    ## 9       159     115   100          1     False
    ## 10       50      64    43          1     False
    ## 11       65      80    58          1     False
    ## 12       85     105    78          1     False
    ## 13      135     115    78          1     False
    ## 14       20      20    45          1     False
    ## 15       25      25    30          1     False
    ## 16       90      80    70          1     False
    ## 17       20      20    50          1     False
    ## 18       25      25    35          1     False
    ## 19       45      80    75          1     False
    ## 20       15      80   145          1     False
    ## 21       35      35    56          1     False
    ## 22       50      50    71          1     False
    ## 23       70      70   101          1     False
    ## 24      135      80   121          1     False
    ## 25       25      35    72          1     False
    ## 26       50      70    97          1     False
    ## 27       31      31    70          1     False
    ## 28       61      61   100          1     False
    ## 29       40      54    55          1     False
    ## 30       65      79    80          1     False
    ## 31       50      50    90          1     False
    ## 32       90      80   110          1     False
    ## 33       20      30    40          1     False
    ## 34       45      55    65          1     False
    ## 35       40      40    41          1     False
    ## 36       55      55    56          1     False
    ## 37       75      85    76          1     False
    ## 38       40      40    50          1     False
    ## 39       55      55    65          1     False
    ## 40       85      75    85          1     False
    ## 41       60      65    35          1     False
    ## 42       95      90    60          1     False
    ## 43       50      65    65          1     False
    ## 44       81     100   100          1     False
    ## 45       45      25    20          1     False
    ## 46       85      50    45          1     False
    ## 47       30      40    55          1     False
    ## 48       65      75    90          1     False
    ## 49       75      65    30          1     False
    ## 50       85      75    40          1     False
    ## 51      110      90    50          1     False
    ## 52       45      55    25          1     False
    ## 53       60      80    30          1     False
    ## 54       40      55    45          1     False
    ## 55       90      75    90          1     False
    ## 56       35      45    95          1     False
    ## 57       50      70   120          1     False
    ## 58       40      40    90          1     False
    ## 59       65      65   115          1     False
    ## 60       65      50    55          1     False
    ## 61       95      80    85          1     False
    ## 62       35      45    70          1     False
    ## 63       60      70    95          1     False
    ## 64       70      50    60          1     False
    ## 65      100      80    95          1     False
    ## 66       40      40    90          1     False
    ## 67       50      50    90          1     False
    ## 68       70      90    70          1     False
    ## 69      105      55    90          1     False
    ## 70      120      70   105          1     False
    ## 71      135      95   120          1     False
    ## 72      175      95   150          1     False
    ## 73       35      35    35          1     False
    ## 74       50      60    45          1     False
    ## 75       65      85    55          1     False
    ## 76       70      30    40          1     False
    ## 77       85      45    55          1     False
    ## 78      100      70    70          1     False
    ## 79       50     100    70          1     False
    ## 80       80     120   100          1     False
    ## 81       30      30    20          1     False
    ## 82       45      45    35          1     False
    ## 83       55      65    45          1     False
    ## 84       65      65    90          1     False
    ## 85       80      80   105          1     False
    ## 86       40      40    15          1     False
    ## 87      100      80    30          1     False
    ## 88      130      80    30          1     False
    ## 89       95      55    45          1     False
    ## 90      120      70    70          1     False
    ## 91       58      62    60          1     False
    ## 92       35      35    75          1     False
    ## 93       60      60   100          1     False
    ## 94       45      70    45          1     False
    ## 95       70      95    70          1     False
    ## 96       40      50    25          1     False
    ## 97       65     100    50          1     False
    ## 98       45      25    40          1     False
    ## 99       85      45    70          1     False
    ## 100     100      35    80          1     False
    ## 101     115      55    95          1     False
    ## 102     130      75   110          1     False
    ## 103     170      95   130          1     False
    ## 104      30      45    70          1     False
    ## 105      43      90    42          1     False
    ## 106      73     115    67          1     False
    ## 107      25      25    50          1     False
    ## 108      50      50    75          1     False
    ## 109      55      55   100          1     False
    ## 110      80      80   140          1     False
    ## 111      60      45    40          1     False
    ## 112     125      65    55          1     False
    ## 113      40      50    35          1     False
    ## 114      50      80    45          1     False
    ## 115      35     110    87          1     False
    ## 116      35     110    76          1     False
    ## 117      60      75    30          1     False
    ## 118      60      45    35          1     False
    ## 119      85      70    60          1     False
    ## 120      30      30    25          1     False
    ## 121      45      45    40          1     False
    ## 122      35     105    50          1     False
    ## 123     100      40    60          1     False
    ## 124      40      80    90          1     False
    ## 125      60     100   100          1     False
    ## 126      70      25    60          1     False
    ## 127      95      45    85          1     False
    ## 128      35      50    63          1     False
    ## 129      65      80    68          1     False
    ## 130      70      55    85          1     False
    ## 131     100      85   115          1     False
    ## 132     100     120    90          1     False
    ## 133      55      80   105          1     False
    ## 134     115      95    95          1     False
    ## 135      95      85   105          1     False
    ## 136     100      85    93          1     False
    ## 137      55      70    85          1     False
    ## 138      65      90   105          1     False
    ## 139      40      70   110          1     False
    ## 140      15      20    80          1     False
    ## 141      60     100    81          1     False
    ## 142      70     130    81          1     False
    ## 143      85      95    60          1     False
    ## 144      48      48    48          1     False
    ## 145      45      65    55          1     False
    ## 146     110      95    65          1     False
    ## 147     110      95   130          1     False
    ## 148      95     110    65          1     False
    ## 149      85      75    40          1     False
    ## 150      90      55    35          1     False
    ## 151     115      70    55          1     False
    ## 152      55      45    55          1     False
    ## 153      65      70    80          1     False
    ## 154      60      75   130          1     False
    ## 155      70      95   150          1     False
    ## 156      65     110    30          1     False
    ## 157      95     125    85          1      True
    ## 158     125      90   100          1      True
    ## 159     125      85    90          1      True
    ## 160      50      50    50          1     False
    ## 161      70      70    70          1     False
    ## 162     100     100    80          1     False
    ## 163     154      90   130          1      True
    ## 164     154     100   130          1      True
    ## 165     194     120   140          1      True
    ## 166     100     100   100          1     False
    ## 167      49      65    45          2     False
    ## 168      63      80    60          2     False
    ## 169      83     100    80          2     False
    ## 170      60      50    65          2     False
    ## 171      80      65    80          2     False
    ## 172     109      85   100          2     False
    ## 173      44      48    43          2     False
    ## 174      59      63    58          2     False
    ## 175      79      83    78          2     False
    ## 176      35      45    20          2     False
    ## 177      45      55    90          2     False
    ## 178      36      56    50          2     False
    ## 179      76      96    70          2     False
    ## 180      40      80    55          2     False
    ## 181      55     110    85          2     False
    ## 182      40      40    30          2     False
    ## 183      60      60    40          2     False
    ## 184      70      80   130          2     False
    ## 185      56      56    67          2     False
    ## 186      76      76    67          2     False
    ## 187      35      35    60          2     False
    ## 188      45      55    15          2     False
    ## 189      40      20    15          2     False
    ## 190      40      65    20          2     False
    ## 191      80     105    40          2     False
    ## 192      70      45    70          2     False
    ## 193      95      70    95          2     False
    ## 194      65      45    35          2     False
    ## 195      80      60    45          2     False
    ## 196     115      90    55          2     False
    ## 197     165     110    45          2     False
    ## 198      90     100    50          2     False
    ## 199      20      50    40          2     False
    ## 200      60      80    50          2     False
    ## 201      30      65    30          2     False
    ## 202      90     100    70          2     False
    ## 203      35      55    50          2     False
    ## 204      45      65    80          2     False
    ## 205      55      95   110          2     False
    ## 206      40      55    85          2     False
    ## 207      30      30    30          2     False
    ## 208     105      85    30          2     False
    ## 209      75      45    95          2     False
    ## 210      25      25    15          2     False
    ## 211      65      65    35          2     False
    ## 212     130      95   110          2     False
    ## 213      60     130    65          2     False
    ## 214      85      42    91          2     False
    ## 215     100     110    30          2     False
    ## 216      85      85    85          2     False
    ## 217      72      48    48          2     False
    ## 218      33      58    33          2     False
    ## 219      90      65    85          2     False
    ## 220      35      35    15          2     False
    ## 221      60      60    40          2     False
    ## 222      65      65    45          2     False
    ## 223      35      65    85          2     False
    ## 224      55      65    30          2     False
    ## 225      55      95    30          2     False
    ## 226      40      40    30          2     False
    ## 227      60      60    45          2     False
    ## 228      55      55    85          2     False
    ## 229      55      80    65          2     False
    ## 230      65     100    75          2     False
    ## 231      10     230     5          2     False
    ## 232      40      95    85          2     False
    ## 233      40     105    75          2     False
    ## 234      35      75   115          2     False
    ## 235      50      50    40          2     False
    ## 236      75      75    55          2     False
    ## 237      70      40    20          2     False
    ## 238      80      80    30          2     False
    ## 239      30      30    50          2     False
    ## 240      60      60    50          2     False
    ## 241      65      85    35          2     False
    ## 242      65      35    65          2     False
    ## 243     105      75    45          2     False
    ## 244      65      45    75          2     False
    ## 245      80     140    70          2     False
    ## 246      40      70    70          2     False
    ## 247      80      50    65          2     False
    ## 248     110      80    95          2     False
    ## 249     140      90   115          2     False
    ## 250      95      95    85          2     False
    ## 251      40      40    40          2     False
    ## 252      60      60    50          2     False
    ## 253     105      95    60          2     False
    ## 254      85      65    85          2     False
    ## 255      20      45    75          2     False
    ## 256      35      35    35          2     False
    ## 257      35     110    70          2     False
    ## 258      85      65    65          2     False
    ## 259      65      55    95          2     False
    ## 260      70      55    83          2     False
    ## 261      40      70   100          2     False
    ## 262      75     135    55          2     False
    ## 263     115     100   115          2      True
    ## 264      90      75   100          2      True
    ## 265      90     115    85          2      True
    ## 266      45      50    41          2     False
    ## 267      65      70    51          2     False
    ## 268      95     100    61          2     False
    ## 269      95     120    71          2     False
    ## 270      90     154   110          2      True
    ## 271     110     154    90          2      True
    ## 272     100     100   100          2     False
    ## 273      65      55    70          3     False
    ## 274      85      65    95          3     False
    ## 275     105      85   120          3     False
    ## 276     145      85   145          3     False
    ## 277      70      50    45          3     False
    ## 278      85      60    55          3     False
    ## 279     110      70    80          3     False
    ## 280     130      80   100          3     False
    ## 281      50      50    40          3     False
    ## 282      60      70    50          3     False
    ## 283      85      90    60          3     False
    ## 284      95     110    70          3     False
    ## 285      30      30    35          3     False
    ## 286      60      60    70          3     False
    ## 287      30      41    60          3     False
    ## 288      50      61   100          3     False
    ## 289      20      30    20          3     False
    ## 290      25      25    15          3     False
    ## 291     100      50    65          3     False
    ## 292      25      25    15          3     False
    ## 293      50      90    65          3     False
    ## 294      40      50    30          3     False
    ## 295      60      70    50          3     False
    ## 296      90     100    70          3     False
    ## 297      30      30    30          3     False
    ## 298      60      40    60          3     False
    ## 299      90      60    80          3     False
    ## 300      30      30    85          3     False
    ## 301      50      50   125          3     False
    ## 302      55      30    85          3     False
    ## 303      85      70    65          3     False
    ## 304      45      35    40          3     False
    ## 305      65      55    50          3     False
    ## 306     125     115    80          3     False
    ## 307     165     135   100          3     False
    ## 308      50      52    65          3     False
    ## 309      80      82    60          3     False
    ## 310      40      60    35          3     False
    ## 311      60      60    70          3     False
    ## 312      35      35    30          3     False
    ## 313      55      55    90          3     False
    ## 314      95      65   100          3     False
    ## 315      30      30    40          3     False
    ## 316      50      50   160          3     False
    ## 317      30      30    40          3     False
    ## 318      51      23    28          3     False
    ## 319      71      43    48          3     False
    ## 320      91      73    68          3     False
    ## 321      20      30    25          3     False
    ## 322      40      60    50          3     False
    ## 323      20      40    20          3     False
    ## 324      45      90    30          3     False
    ## 325      35      35    50          3     False
    ## 326      55      55    70          3     False
    ## 327      65      65    50          3     False
    ## 328      85     115    20          3     False
    ## 329      55      55    50          3     False
    ## 330      55      95    50          3     False
    ## 331      40      40    30          3     False
    ## 332      50      50    40          3     False
    ## 333      60      60    50          3     False
    ## 334      60      80    50          3     False
    ## 335      40      55    60          3     False
    ## 336      60      75    80          3     False
    ## 337      80      85   100          3     False
    ## 338      65      40    65          3     False
    ## 339     105      60   105          3     False
    ## 340     135      80   135          3     False
    ## 341      85      75    95          3     False
    ## 342      75      85    95          3     False
    ## 343      47      75    85          3     False
    ## 344      73      75    85          3     False
    ## 345     100      80    65          3     False
    ## 346      43      53    40          3     False
    ## 347      73      83    55          3     False
    ## 348      65      20    65          3     False
    ## 349      95      40    95          3     False
    ## 350     110      65   105          3     False
    ## 351      70      35    60          3     False
    ## 352      90      45    60          3     False
    ## 353      65      45    35          3     False
    ## 354     105      75    40          3     False
    ## 355     145     105    20          3     False
    ## 356      85      70    20          3     False
    ## 357      70      80    60          3     False
    ## 358      90     110    80          3     False
    ## 359      60      60    60          3     False
    ## 360      45      45    10          3     False
    ## 361      50      50    70          3     False
    ## 362      80      80   100          3     False
    ## 363      85      40    35          3     False
    ## 364     115      60    55          3     False
    ## 365      40      75    50          3     False
    ## 366      70     105    80          3     False
    ## 367     110     105    80          3     False
    ## 368      60      60    90          3     False
    ## 369     100      60    65          3     False
    ## 370      95      85    70          3     False
    ## 371      55      65    70          3     False
    ## 372      46      41    60          3     False
    ## 373      76      71    60          3     False
    ## 374      50      35    35          3     False
    ## 375      90      55    55          3     False
    ## 376      40      70    55          3     False
    ## 377      70     120    75          3     False
    ## 378      61      87    23          3     False
    ## 379      81     107    43          3     False
    ## 380      40      50    75          3     False
    ## 381      70      80    45          3     False
    ## 382      10      55    80          3     False
    ## 383     100     125    81          3     False
    ## 384      70      70    70          3     False
    ## 385      60     120    40          3     False
    ## 386      63      33    45          3     False
    ## 387      83      63    65          3     False
    ## 388      93      83    75          3     False
    ## 389      30      90    25          3     False
    ## 390      60     130    25          3     False
    ## 391      72      87    51          3     False
    ## 392      95      80    65          3     False
    ## 393      75      60    75          3     False
    ## 394     115      60   115          3     False
    ## 395      23      48    23          3     False
    ## 396      50      50    50          3     False
    ## 397      80      80    80          3     False
    ## 398     120      80   100          3     False
    ## 399      55      50    25          3     False
    ## 400      75      70    45          3     False
    ## 401      95      90    65          3     False
    ## 402      74      55    32          3     False
    ## 403      94      75    52          3     False
    ## 404     114      75    52          3     False
    ## 405      45      65    55          3     False
    ## 406      40      65    97          3     False
    ## 407      40      30    50          3     False
    ## 408      60      50    50          3     False
    ## 409     110      80   100          3     False
    ## 410     120      90   120          3     False
    ## 411      35      60    30          3     False
    ## 412      55      80    50          3     False
    ## 413      95      90    70          3     False
    ## 414     105     110   110          3     False
    ## 415      50     100    50          3      True
    ## 416     100     200    50          3      True
    ## 417      75     150    50          3      True
    ## 418     110     130   110          3      True
    ## 419     140     150   110          3      True
    ## 420     130     110   110          3      True
    ## 421     160     120   110          3      True
    ## 422     150     140    90          3      True
    ## 423     180     160    90          3      True
    ## 424     100      90    90          3      True
    ## 425     150      90    90          3      True
    ## 426     150      90    95          3      True
    ## 427     180     100   115          3      True
    ## 428     100     100   100          3      True
    ## 429     150      50   150          3      True
    ## 430     180      20   150          3      True
    ## 431      70     160    90          3      True
    ## 432      95      90   180          3      True
    ## 433      45      55    31          4     False
    ## 434      55      65    36          4     False
    ## 435      75      85    56          4     False
    ## 436      58      44    61          4     False
    ## 437      78      52    81          4     False
    ## 438     104      71   108          4     False
    ## 439      61      56    40          4     False
    ## 440      81      76    50          4     False
    ## 441     111     101    60          4     False
    ## 442      30      30    60          4     False
    ## 443      40      40    80          4     False
    ## 444      50      60   100          4     False
    ## 445      35      40    31          4     False
    ## 446      55      60    71          4     False
    ## 447      25      41    25          4     False
    ## 448      55      51    65          4     False
    ## 449      40      34    45          4     False
    ## 450      60      49    60          4     False
    ## 451      95      79    70          4     False
    ## 452      50      70    55          4     False
    ## 453     125     105    90          4     False
    ## 454      30      30    58          4     False
    ## 455      65      50    58          4     False
    ## 456      42      88    30          4     False
    ## 457      47     138    30          4     False
    ## 458      29      45    36          4     False
    ## 459      79     105    36          4     False
    ## 460      59      85    36          4     False
    ## 461      69      95    36          4     False
    ## 462      94      50    66          4     False
    ## 463      30      42    70          4     False
    ## 464      80     102    40          4     False
    ## 465      45      90    95          4     False
    ## 466      60      30    85          4     False
    ## 467      85      50   115          4     False
    ## 468      62      53    35          4     False
    ## 469      87      78    85          4     False
    ## 470      57      62    34          4     False
    ## 471      92      82    39          4     False
    ## 472      60      66   115          4     False
    ## 473      60      44    70          4     False
    ## 474      90      54    80          4     False
    ## 475      44      56    85          4     False
    ## 476      54      96   105          4     False
    ## 477      54      96   135          4     False
    ## 478     105     105   105          4     False
    ## 479     105      52    71          4     False
    ## 480      42      37    85          4     False
    ## 481      64      59   112          4     False
    ## 482      65      50    45          4     False
    ## 483      41      41    74          4     False
    ## 484      71      61    84          4     False
    ## 485      24      86    23          4     False
    ## 486      79     116    33          4     False
    ## 487      10      45    10          4     False
    ## 488      70      90    60          4     False
    ## 489      15      65    30          4     False
    ## 490      92      42    91          4     False
    ## 491      92     108    35          4     False
    ## 492      40      45    42          4     False
    ## 493      50      55    82          4     False
    ## 494      80      85   102          4     False
    ## 495     120      95    92          4     False
    ## 496      40      85     5          4     False
    ## 497      35      40    60          4     False
    ## 498     115      70    90          4     False
    ## 499     140      70   112          4     False
    ## 500      38      42    32          4     False
    ## 501      68      72    47          4     False
    ## 502      30      55    65          4     False
    ## 503      60      75    95          4     False
    ## 504      61      40    50          4     False
    ## 505      86      65    85          4     False
    ## 506      90      72    46          4     False
    ## 507      49      61    66          4     False
    ## 508      69      86    91          4     False
    ## 509      60     120    50          4     False
    ## 510      62      60    40          4     False
    ## 511      92      85    60          4     False
    ## 512     132     105    30          4     False
    ## 513      45      85   125          4     False
    ## 514     130      90    60          4     False
    ## 515      80      95    50          4     False
    ## 516      55      55    40          4     False
    ## 517     110      50    50          4     False
    ## 518      95      85    95          4     False
    ## 519     125      95    83          4     False
    ## 520     120     115    80          4     False
    ## 521     116      56    95          4     False
    ## 522      60      65    95          4     False
    ## 523     130      95    65          4     False
    ## 524      45      75    95          4     False
    ## 525      70      60    80          4     False
    ## 526     135      75    90          4     False
    ## 527      65     115    80          4     False
    ## 528      65     115   110          4     False
    ## 529      75     150    40          4     False
    ## 530      65     135    45          4     False
    ## 531      80      70   110          4     False
    ## 532      95      77    91          4     False
    ## 533     105     107    86          4     False
    ## 534     105     107    86          4     False
    ## 535     105     107    86          4     False
    ## 536     105     107    86          4     False
    ## 537     105     107    86          4     False
    ## 538      75     130    95          4      True
    ## 539     105     105    80          4      True
    ## 540     125      70   115          4      True
    ## 541     150     100    90          4      True
    ## 542     150     120   100          4      True
    ## 543     130     106    77          4      True
    ## 544      80     110   100          4      True
    ## 545     100     120    90          4      True
    ## 546     120     100    90          4      True
    ## 547      75     130    85          4     False
    ## 548      80      80    80          4     False
    ## 549     100     100   100          4     False
    ## 550     135      90   125          4      True
    ## 551     100     100   100          4      True
    ## 552     120      75   127          4      True
    ## 553     120     120   120          4      True
    ## 554     100     100   100          5      True
    ## 555      45      55    63          5     False
    ## 556      60      75    83          5     False
    ## 557      75      95   113          5     False
    ## 558      45      45    45          5     False
    ## 559      70      55    55          5     False
    ## 560     100      65    65          5     False
    ## 561      63      45    45          5     False
    ## 562      83      60    60          5     False
    ## 563     108      70    70          5     False
    ## 564      35      39    42          5     False
    ## 565      60      69    77          5     False
    ## 566      25      45    55          5     False
    ## 567      35      65    60          5     False
    ## 568      45      90    80          5     False
    ## 569      50      37    66          5     False
    ## 570      88      50   106          5     False
    ## 571      53      48    64          5     False
    ## 572      98      63   101          5     False
    ## 573      53      48    64          5     False
    ## 574      98      63   101          5     False
    ## 575      53      48    64          5     False
    ## 576      98      63   101          5     False
    ## 577      67      55    24          5     False
    ## 578     107      95    29          5     False
    ## 579      36      30    43          5     False
    ## 580      50      42    65          5     False
    ## 581      65      55    93          5     False
    ## 582      50      32    76          5     False
    ## 583      80      63   116          5     False
    ## 584      25      25    15          5     False
    ## 585      50      40    20          5     False
    ## 586      60      80    25          5     False
    ## 587      55      43    72          5     False
    ## 588      77      55   114          5     False
    ## 589      30      45    68          5     False
    ## 590      50      65    88          5     False
    ## 591      60      86    50          5     False
    ## 592      80     126    50          5     False
    ## 593      25      35    35          5     False
    ## 594      40      50    40          5     False
    ## 595      55      65    45          5     False
    ## 596      50      40    64          5     False
    ## 597      65      55    69          5     False
    ## 598      85      75    74          5     False
    ## 599      30      85    45          5     False
    ## 600      30      75    85          5     False
    ## 601      40      60    42          5     False
    ## 602      50      80    42          5     False
    ## 603      70      80    92          5     False
    ## 604      30      39    57          5     False
    ## 605      40      79    47          5     False
    ## 606      55      69   112          5     False
    ## 607      37      50    66          5     False
    ## 608      77      75   116          5     False
    ## 609      70      50    30          5     False
    ## 610     110      75    90          5     False
    ## 611      80      55    98          5     False
    ## 612      35      35    65          5     False
    ## 613      45      45    74          5     False
    ## 614      65      70    92          5     False
    ## 615      15      45    50          5     False
    ## 616      30      55    95          5     False
    ## 617     140     105    55          5     False
    ## 618     106      67    60          5     False
    ## 619      35      35    55          5     False
    ## 620      65      75    45          5     False
    ## 621      35      70    48          5     False
    ## 622      45     115    58          5     False
    ## 623     103      80    97          5     False
    ## 624      55      65    30          5     False
    ## 625      95     105    30          5     False
    ## 626      53      45    22          5     False
    ## 627      83      65    32          5     False
    ## 628      74      45    70          5     False
    ## 629     112      65   110          5     False
    ## 630      40      62    65          5     False
    ## 631      60      82    75          5     False
    ## 632      80      40    65          5     False
    ## 633     120      60   105          5     False
    ## 634      40      40    75          5     False
    ## 635      65      60   115          5     False
    ## 636      55      65    45          5     False
    ## 637      75      85    55          5     False
    ## 638      95     110    65          5     False
    ## 639     105      50    20          5     False
    ## 640     125      60    30          5     False
    ## 641     125      85    30          5     False
    ## 642      44      50    55          5     False
    ## 643      87      63    98          5     False
    ## 644      65      60    44          5     False
    ## 645      80      75    59          5     False
    ## 646     110      95    79          5     False
    ## 647      40      50    75          5     False
    ## 648      60      70    95          5     False
    ## 649      75      60   103          5     False
    ## 650      40      45    60          5     False
    ## 651      60     105    20          5     False
    ## 652      55      55    15          5     False
    ## 653      85      80    30          5     False
    ## 654      65      85    40          5     False
    ## 655      85     105    60          5     False
    ## 656      40      45    65          5     False
    ## 657      57      50    65          5     False
    ## 658      97      60   108          5     False
    ## 659      24      86    10          5     False
    ## 660      54     116    20          5     False
    ## 661      45      60    30          5     False
    ## 662      70      85    50          5     False
    ## 663      70      85    90          5     False
    ## 664      45      40    60          5     False
    ## 665      75      70    40          5     False
    ## 666     105      80    50          5     False
    ## 667      85      55    30          5     False
    ## 668     125      95    40          5     False
    ## 669      65      55    20          5     False
    ## 670      95      60    55          5     False
    ## 671     145      90    80          5     False
    ## 672      30      40    57          5     False
    ## 673      40      50    67          5     False
    ## 674      60      70    97          5     False
    ## 675      60      40    40          5     False
    ## 676      70      80    50          5     False
    ## 677      95     135   105          5     False
    ## 678      40      65    25          5     False
    ## 679     100      60   145          5     False
    ## 680      81      99    32          5     False
    ## 681      55      50    65          5     False
    ## 682      95      60   105          5     False
    ## 683      60      90    48          5     False
    ## 684      35      50    35          5     False
    ## 685      55      80    55          5     False
    ## 686      40      40    60          5     False
    ## 687      60      70    70          5     False
    ## 688      40      95    55          5     False
    ## 689      37      50    60          5     False
    ## 690      57      75    80          5     False
    ## 691      45      65    60          5     False
    ## 692      55      95    80          5     False
    ## 693     105      66    65          5     False
    ## 694      48      48   109          5     False
    ## 695      45      50    38          5     False
    ## 696      65      70    58          5     False
    ## 697     125      90    98          5     False
    ## 698      50      55    60          5     False
    ## 699     135     105   100          5     False
    ## 700      90      72   108          5      True
    ## 701      72      90   108          5      True
    ## 702      90     129   108          5      True
    ## 703     125      80   111          5      True
    ## 704     110      90   121          5      True
    ## 705     125      80   111          5      True
    ## 706     145      80   101          5      True
    ## 707     150     120    90          5      True
    ## 708     120     100    90          5      True
    ## 709     115      80   101          5      True
    ## 710     105      80    91          5      True
    ## 711     130      90    95          5      True
    ## 712     120      90    95          5      True
    ## 713     170     100    95          5      True
    ## 714     129      90   108          5     False
    ## 715     129      90   108          5     False
    ## 716     128     128    90          5     False
    ## 717      77      77   128          5     False
    ## 718     120      95    99          5     False
    ## 719      48      45    38          6     False
    ## 720      56      58    57          6     False
    ## 721      74      75    64          6     False
    ## 722      62      60    60          6     False
    ## 723      90      70    73          6     False
    ## 724     114     100   104          6     False
    ## 725      62      44    71          6     False
    ## 726      83      56    97          6     False
    ## 727     103      71   122          6     False
    ## 728      32      36    57          6     False
    ## 729      50      77    78          6     False
    ## 730      40      38    62          6     False
    ## 731      56      52    84          6     False
    ## 732      74      69   126          6     False
    ## 733      27      25    35          6     False
    ## 734      27      30    29          6     False
    ## 735      90      50    89          6     False
    ## 736      73      54    72          6     False
    ## 737     109      66   106          6     False
    ## 738      61      79    42          6     False
    ## 739      75      98    52          6     False
    ## 740     112     154    75          6     False
    ## 741      62      57    52          6     False
    ## 742      97      81    68          6     False
    ## 743      46      48    43          6     False
    ## 744      69      71    58          6     False
    ## 745      65      90   102          6     False
    ## 746      63      60    68          6     False
    ## 747      83      81   104          6     False
    ## 748      83      81   104          6     False
    ## 749      35      37    28          6     False
    ## 750      45      49    35          6     False
    ## 751     150      50    60          6     False
    ## 752      50     150    60          6     False
    ## 753      63      65    23          6     False
    ## 754      99      89    29          6     False
    ## 755      59      57    49          6     False
    ## 756      85      75    72          6     False
    ## 757      37      46    45          6     False
    ## 758      68      75    73          6     False
    ## 759      39      56    50          6     False
    ## 760      54      86    68          6     False
    ## 761      60      60    30          6     False
    ## 762      97     123    44          6     False
    ## 763      58      63    44          6     False
    ## 764     120      89    59          6     False
    ## 765      61      43    70          6     False
    ## 766     109      94   109          6     False
    ## 767      45      45    48          6     False
    ## 768      69      59    71          6     False
    ## 769      67      63    46          6     False
    ## 770      99      92    58          6     False
    ## 771     110     130    60          6     False
    ## 772      74      63   118          6     False
    ## 773      81      67   101          6     False
    ## 774      50     150    50          6     False
    ## 775      55      75    40          6     False
    ## 776      83     113    60          6     False
    ## 777     110     150    80          6     False
    ## 778      80      87    75          6     False
    ## 779      50      60    38          6     False
    ## 780      65      82    56          6     False
    ## 781      44      55    51          6     False
    ## 782      44      55    56          6     False
    ## 783      44      55    46          6     False
    ## 784      44      55    41          6     False
    ## 785      58      75    84          6     False
    ## 786      58      75    99          6     False
    ## 787      58      75    69          6     False
    ## 788      58      75    54          6     False
    ## 789      32      35    28          6     False
    ## 790      44      46    28          6     False
    ## 791      45      40    55          6     False
    ## 792      97      80   123          6     False
    ## 793     131      98    99          6      True
    ## 794     131      98    99          6      True
    ## 795      81      95    95          6      True
    ## 796     100     150    50          6      True
    ## 797     160     110   110          6      True
    ## 798     150     130    70          6      True
    ## 799     170     130    80          6      True
    ## 800     130      90    70          6      True

``` r
pk <-  pk[, !(colnames(pk)%in% c("Name","Type.1","Type.2", "Total" , "HP" , "Defense","Generation","Legendary","Sp..Atk","Sp..Def" ))]
pk
```

    ##      X. Attack Speed
    ## 1     1     49    45
    ## 2     2     62    60
    ## 3     3     82    80
    ## 4     3    100    80
    ## 5     4     52    65
    ## 6     5     64    80
    ## 7     6     84   100
    ## 8     6    130   100
    ## 9     6    104   100
    ## 10    7     48    43
    ## 11    8     63    58
    ## 12    9     83    78
    ## 13    9    103    78
    ## 14   10     30    45
    ## 15   11     20    30
    ## 16   12     45    70
    ## 17   13     35    50
    ## 18   14     25    35
    ## 19   15     90    75
    ## 20   15    150   145
    ## 21   16     45    56
    ## 22   17     60    71
    ## 23   18     80   101
    ## 24   18     80   121
    ## 25   19     56    72
    ## 26   20     81    97
    ## 27   21     60    70
    ## 28   22     90   100
    ## 29   23     60    55
    ## 30   24     85    80
    ## 31   25     55    90
    ## 32   26     90   110
    ## 33   27     75    40
    ## 34   28    100    65
    ## 35   29     47    41
    ## 36   30     62    56
    ## 37   31     92    76
    ## 38   32     57    50
    ## 39   33     72    65
    ## 40   34    102    85
    ## 41   35     45    35
    ## 42   36     70    60
    ## 43   37     41    65
    ## 44   38     76   100
    ## 45   39     45    20
    ## 46   40     70    45
    ## 47   41     45    55
    ## 48   42     80    90
    ## 49   43     50    30
    ## 50   44     65    40
    ## 51   45     80    50
    ## 52   46     70    25
    ## 53   47     95    30
    ## 54   48     55    45
    ## 55   49     65    90
    ## 56   50     55    95
    ## 57   51     80   120
    ## 58   52     45    90
    ## 59   53     70   115
    ## 60   54     52    55
    ## 61   55     82    85
    ## 62   56     80    70
    ## 63   57    105    95
    ## 64   58     70    60
    ## 65   59    110    95
    ## 66   60     50    90
    ## 67   61     65    90
    ## 68   62     95    70
    ## 69   63     20    90
    ## 70   64     35   105
    ## 71   65     50   120
    ## 72   65     50   150
    ## 73   66     80    35
    ## 74   67    100    45
    ## 75   68    130    55
    ## 76   69     75    40
    ## 77   70     90    55
    ## 78   71    105    70
    ## 79   72     40    70
    ## 80   73     70   100
    ## 81   74     80    20
    ## 82   75     95    35
    ## 83   76    120    45
    ## 84   77     85    90
    ## 85   78    100   105
    ## 86   79     65    15
    ## 87   80     75    30
    ## 88   80     75    30
    ## 89   81     35    45
    ## 90   82     60    70
    ## 91   83     65    60
    ## 92   84     85    75
    ## 93   85    110   100
    ## 94   86     45    45
    ## 95   87     70    70
    ## 96   88     80    25
    ## 97   89    105    50
    ## 98   90     65    40
    ## 99   91     95    70
    ## 100  92     35    80
    ## 101  93     50    95
    ## 102  94     65   110
    ## 103  94     65   130
    ## 104  95     45    70
    ## 105  96     48    42
    ## 106  97     73    67
    ## 107  98    105    50
    ## 108  99    130    75
    ## 109 100     30   100
    ## 110 101     50   140
    ## 111 102     40    40
    ## 112 103     95    55
    ## 113 104     50    35
    ## 114 105     80    45
    ## 115 106    120    87
    ## 116 107    105    76
    ## 117 108     55    30
    ## 118 109     65    35
    ## 119 110     90    60
    ## 120 111     85    25
    ## 121 112    130    40
    ## 122 113      5    50
    ## 123 114     55    60
    ## 124 115     95    90
    ## 125 115    125   100
    ## 126 116     40    60
    ## 127 117     65    85
    ## 128 118     67    63
    ## 129 119     92    68
    ## 130 120     45    85
    ## 131 121     75   115
    ## 132 122     45    90
    ## 133 123    110   105
    ## 134 124     50    95
    ## 135 125     83   105
    ## 136 126     95    93
    ## 137 127    125    85
    ## 138 127    155   105
    ## 139 128    100   110
    ## 140 129     10    80
    ## 141 130    125    81
    ## 142 130    155    81
    ## 143 131     85    60
    ## 144 132     48    48
    ## 145 133     55    55
    ## 146 134     65    65
    ## 147 135     65   130
    ## 148 136    130    65
    ## 149 137     60    40
    ## 150 138     40    35
    ## 151 139     60    55
    ## 152 140     80    55
    ## 153 141    115    80
    ## 154 142    105   130
    ## 155 142    135   150
    ## 156 143    110    30
    ## 157 144     85    85
    ## 158 145     90   100
    ## 159 146    100    90
    ## 160 147     64    50
    ## 161 148     84    70
    ## 162 149    134    80
    ## 163 150    110   130
    ## 164 150    190   130
    ## 165 150    150   140
    ## 166 151    100   100
    ## 167 152     49    45
    ## 168 153     62    60
    ## 169 154     82    80
    ## 170 155     52    65
    ## 171 156     64    80
    ## 172 157     84   100
    ## 173 158     65    43
    ## 174 159     80    58
    ## 175 160    105    78
    ## 176 161     46    20
    ## 177 162     76    90
    ## 178 163     30    50
    ## 179 164     50    70
    ## 180 165     20    55
    ## 181 166     35    85
    ## 182 167     60    30
    ## 183 168     90    40
    ## 184 169     90   130
    ## 185 170     38    67
    ## 186 171     58    67
    ## 187 172     40    60
    ## 188 173     25    15
    ## 189 174     30    15
    ## 190 175     20    20
    ## 191 176     40    40
    ## 192 177     50    70
    ## 193 178     75    95
    ## 194 179     40    35
    ## 195 180     55    45
    ## 196 181     75    55
    ## 197 181     95    45
    ## 198 182     80    50
    ## 199 183     20    40
    ## 200 184     50    50
    ## 201 185    100    30
    ## 202 186     75    70
    ## 203 187     35    50
    ## 204 188     45    80
    ## 205 189     55   110
    ## 206 190     70    85
    ## 207 191     30    30
    ## 208 192     75    30
    ## 209 193     65    95
    ## 210 194     45    15
    ## 211 195     85    35
    ## 212 196     65   110
    ## 213 197     65    65
    ## 214 198     85    91
    ## 215 199     75    30
    ## 216 200     60    85
    ## 217 201     72    48
    ## 218 202     33    33
    ## 219 203     80    85
    ## 220 204     65    15
    ## 221 205     90    40
    ## 222 206     70    45
    ## 223 207     75    85
    ## 224 208     85    30
    ## 225 208    125    30
    ## 226 209     80    30
    ## 227 210    120    45
    ## 228 211     95    85
    ## 229 212    130    65
    ## 230 212    150    75
    ## 231 213     10     5
    ## 232 214    125    85
    ## 233 214    185    75
    ## 234 215     95   115
    ## 235 216     80    40
    ## 236 217    130    55
    ## 237 218     40    20
    ## 238 219     50    30
    ## 239 220     50    50
    ## 240 221    100    50
    ## 241 222     55    35
    ## 242 223     65    65
    ## 243 224    105    45
    ## 244 225     55    75
    ## 245 226     40    70
    ## 246 227     80    70
    ## 247 228     60    65
    ## 248 229     90    95
    ## 249 229     90   115
    ## 250 230     95    85
    ## 251 231     60    40
    ## 252 232    120    50
    ## 253 233     80    60
    ## 254 234     95    85
    ## 255 235     20    75
    ## 256 236     35    35
    ## 257 237     95    70
    ## 258 238     30    65
    ## 259 239     63    95
    ## 260 240     75    83
    ## 261 241     80   100
    ## 262 242     10    55
    ## 263 243     85   115
    ## 264 244    115   100
    ## 265 245     75    85
    ## 266 246     64    41
    ## 267 247     84    51
    ## 268 248    134    61
    ## 269 248    164    71
    ## 270 249     90   110
    ## 271 250    130    90
    ## 272 251    100   100
    ## 273 252     45    70
    ## 274 253     65    95
    ## 275 254     85   120
    ## 276 254    110   145
    ## 277 255     60    45
    ## 278 256     85    55
    ## 279 257    120    80
    ## 280 257    160   100
    ## 281 258     70    40
    ## 282 259     85    50
    ## 283 260    110    60
    ## 284 260    150    70
    ## 285 261     55    35
    ## 286 262     90    70
    ## 287 263     30    60
    ## 288 264     70   100
    ## 289 265     45    20
    ## 290 266     35    15
    ## 291 267     70    65
    ## 292 268     35    15
    ## 293 269     50    65
    ## 294 270     30    30
    ## 295 271     50    50
    ## 296 272     70    70
    ## 297 273     40    30
    ## 298 274     70    60
    ## 299 275    100    80
    ## 300 276     55    85
    ## 301 277     85   125
    ## 302 278     30    85
    ## 303 279     50    65
    ## 304 280     25    40
    ## 305 281     35    50
    ## 306 282     65    80
    ## 307 282     85   100
    ## 308 283     30    65
    ## 309 284     60    60
    ## 310 285     40    35
    ## 311 286    130    70
    ## 312 287     60    30
    ## 313 288     80    90
    ## 314 289    160   100
    ## 315 290     45    40
    ## 316 291     90   160
    ## 317 292     90    40
    ## 318 293     51    28
    ## 319 294     71    48
    ## 320 295     91    68
    ## 321 296     60    25
    ## 322 297    120    50
    ## 323 298     20    20
    ## 324 299     45    30
    ## 325 300     45    50
    ## 326 301     65    70
    ## 327 302     75    50
    ## 328 302     85    20
    ## 329 303     85    50
    ## 330 303    105    50
    ## 331 304     70    30
    ## 332 305     90    40
    ## 333 306    110    50
    ## 334 306    140    50
    ## 335 307     40    60
    ## 336 308     60    80
    ## 337 308    100   100
    ## 338 309     45    65
    ## 339 310     75   105
    ## 340 310     75   135
    ## 341 311     50    95
    ## 342 312     40    95
    ## 343 313     73    85
    ## 344 314     47    85
    ## 345 315     60    65
    ## 346 316     43    40
    ## 347 317     73    55
    ## 348 318     90    65
    ## 349 319    120    95
    ## 350 319    140   105
    ## 351 320     70    60
    ## 352 321     90    60
    ## 353 322     60    35
    ## 354 323    100    40
    ## 355 323    120    20
    ## 356 324     85    20
    ## 357 325     25    60
    ## 358 326     45    80
    ## 359 327     60    60
    ## 360 328    100    10
    ## 361 329     70    70
    ## 362 330    100   100
    ## 363 331     85    35
    ## 364 332    115    55
    ## 365 333     40    50
    ## 366 334     70    80
    ## 367 334    110    80
    ## 368 335    115    90
    ## 369 336    100    65
    ## 370 337     55    70
    ## 371 338     95    70
    ## 372 339     48    60
    ## 373 340     78    60
    ## 374 341     80    35
    ## 375 342    120    55
    ## 376 343     40    55
    ## 377 344     70    75
    ## 378 345     41    23
    ## 379 346     81    43
    ## 380 347     95    75
    ## 381 348    125    45
    ## 382 349     15    80
    ## 383 350     60    81
    ## 384 351     70    70
    ## 385 352     90    40
    ## 386 353     75    45
    ## 387 354    115    65
    ## 388 354    165    75
    ## 389 355     40    25
    ## 390 356     70    25
    ## 391 357     68    51
    ## 392 358     50    65
    ## 393 359    130    75
    ## 394 359    150   115
    ## 395 360     23    23
    ## 396 361     50    50
    ## 397 362     80    80
    ## 398 362    120   100
    ## 399 363     40    25
    ## 400 364     60    45
    ## 401 365     80    65
    ## 402 366     64    32
    ## 403 367    104    52
    ## 404 368     84    52
    ## 405 369     90    55
    ## 406 370     30    97
    ## 407 371     75    50
    ## 408 372     95    50
    ## 409 373    135   100
    ## 410 373    145   120
    ## 411 374     55    30
    ## 412 375     75    50
    ## 413 376    135    70
    ## 414 376    145   110
    ## 415 377    100    50
    ## 416 378     50    50
    ## 417 379     75    50
    ## 418 380     80   110
    ## 419 380    100   110
    ## 420 381     90   110
    ## 421 381    130   110
    ## 422 382    100    90
    ## 423 382    150    90
    ## 424 383    150    90
    ## 425 383    180    90
    ## 426 384    150    95
    ## 427 384    180   115
    ## 428 385    100   100
    ## 429 386    150   150
    ## 430 386    180   150
    ## 431 386     70    90
    ## 432 386     95   180
    ## 433 387     68    31
    ## 434 388     89    36
    ## 435 389    109    56
    ## 436 390     58    61
    ## 437 391     78    81
    ## 438 392    104   108
    ## 439 393     51    40
    ## 440 394     66    50
    ## 441 395     86    60
    ## 442 396     55    60
    ## 443 397     75    80
    ## 444 398    120   100
    ## 445 399     45    31
    ## 446 400     85    71
    ## 447 401     25    25
    ## 448 402     85    65
    ## 449 403     65    45
    ## 450 404     85    60
    ## 451 405    120    70
    ## 452 406     30    55
    ## 453 407     70    90
    ## 454 408    125    58
    ## 455 409    165    58
    ## 456 410     42    30
    ## 457 411     52    30
    ## 458 412     29    36
    ## 459 413     59    36
    ## 460 413     79    36
    ## 461 413     69    36
    ## 462 414     94    66
    ## 463 415     30    70
    ## 464 416     80    40
    ## 465 417     45    95
    ## 466 418     65    85
    ## 467 419    105   115
    ## 468 420     35    35
    ## 469 421     60    85
    ## 470 422     48    34
    ## 471 423     83    39
    ## 472 424    100   115
    ## 473 425     50    70
    ## 474 426     80    80
    ## 475 427     66    85
    ## 476 428     76   105
    ## 477 428    136   135
    ## 478 429     60   105
    ## 479 430    125    71
    ## 480 431     55    85
    ## 481 432     82   112
    ## 482 433     30    45
    ## 483 434     63    74
    ## 484 435     93    84
    ## 485 436     24    23
    ## 486 437     89    33
    ## 487 438     80    10
    ## 488 439     25    60
    ## 489 440      5    30
    ## 490 441     65    91
    ## 491 442     92    35
    ## 492 443     70    42
    ## 493 444     90    82
    ## 494 445    130   102
    ## 495 445    170    92
    ## 496 446     85     5
    ## 497 447     70    60
    ## 498 448    110    90
    ## 499 448    145   112
    ## 500 449     72    32
    ## 501 450    112    47
    ## 502 451     50    65
    ## 503 452     90    95
    ## 504 453     61    50
    ## 505 454    106    85
    ## 506 455    100    46
    ## 507 456     49    66
    ## 508 457     69    91
    ## 509 458     20    50
    ## 510 459     62    40
    ## 511 460     92    60
    ## 512 460    132    30
    ## 513 461    120   125
    ## 514 462     70    60
    ## 515 463     85    50
    ## 516 464    140    40
    ## 517 465    100    50
    ## 518 466    123    95
    ## 519 467     95    83
    ## 520 468     50    80
    ## 521 469     76    95
    ## 522 470    110    95
    ## 523 471     60    65
    ## 524 472     95    95
    ## 525 473    130    80
    ## 526 474     80    90
    ## 527 475    125    80
    ## 528 475    165   110
    ## 529 476     55    40
    ## 530 477    100    45
    ## 531 478     80   110
    ## 532 479     50    91
    ## 533 479     65    86
    ## 534 479     65    86
    ## 535 479     65    86
    ## 536 479     65    86
    ## 537 479     65    86
    ## 538 480     75    95
    ## 539 481    105    80
    ## 540 482    125   115
    ## 541 483    120    90
    ## 542 484    120   100
    ## 543 485     90    77
    ## 544 486    160   100
    ## 545 487    100    90
    ## 546 487    120    90
    ## 547 488     70    85
    ## 548 489     80    80
    ## 549 490    100   100
    ## 550 491     90   125
    ## 551 492    100   100
    ## 552 492    103   127
    ## 553 493    120   120
    ## 554 494    100   100
    ## 555 495     45    63
    ## 556 496     60    83
    ## 557 497     75   113
    ## 558 498     63    45
    ## 559 499     93    55
    ## 560 500    123    65
    ## 561 501     55    45
    ## 562 502     75    60
    ## 563 503    100    70
    ## 564 504     55    42
    ## 565 505     85    77
    ## 566 506     60    55
    ## 567 507     80    60
    ## 568 508    110    80
    ## 569 509     50    66
    ## 570 510     88   106
    ## 571 511     53    64
    ## 572 512     98   101
    ## 573 513     53    64
    ## 574 514     98   101
    ## 575 515     53    64
    ## 576 516     98   101
    ## 577 517     25    24
    ## 578 518     55    29
    ## 579 519     55    43
    ## 580 520     77    65
    ## 581 521    115    93
    ## 582 522     60    76
    ## 583 523    100   116
    ## 584 524     75    15
    ## 585 525    105    20
    ## 586 526    135    25
    ## 587 527     45    72
    ## 588 528     57   114
    ## 589 529     85    68
    ## 590 530    135    88
    ## 591 531     60    50
    ## 592 531     60    50
    ## 593 532     80    35
    ## 594 533    105    40
    ## 595 534    140    45
    ## 596 535     50    64
    ## 597 536     65    69
    ## 598 537     95    74
    ## 599 538    100    45
    ## 600 539    125    85
    ## 601 540     53    42
    ## 602 541     63    42
    ## 603 542    103    92
    ## 604 543     45    57
    ## 605 544     55    47
    ## 606 545    100   112
    ## 607 546     27    66
    ## 608 547     67   116
    ## 609 548     35    30
    ## 610 549     60    90
    ## 611 550     92    98
    ## 612 551     72    65
    ## 613 552     82    74
    ## 614 553    117    92
    ## 615 554     90    50
    ## 616 555    140    95
    ## 617 555     30    55
    ## 618 556     86    60
    ## 619 557     65    55
    ## 620 558     95    45
    ## 621 559     75    48
    ## 622 560     90    58
    ## 623 561     58    97
    ## 624 562     30    30
    ## 625 563     50    30
    ## 626 564     78    22
    ## 627 565    108    32
    ## 628 566    112    70
    ## 629 567    140   110
    ## 630 568     50    65
    ## 631 569     95    75
    ## 632 570     65    65
    ## 633 571    105   105
    ## 634 572     50    75
    ## 635 573     95   115
    ## 636 574     30    45
    ## 637 575     45    55
    ## 638 576     55    65
    ## 639 577     30    20
    ## 640 578     40    30
    ## 641 579     65    30
    ## 642 580     44    55
    ## 643 581     87    98
    ## 644 582     50    44
    ## 645 583     65    59
    ## 646 584     95    79
    ## 647 585     60    75
    ## 648 586    100    95
    ## 649 587     75   103
    ## 650 588     75    60
    ## 651 589    135    20
    ## 652 590     55    15
    ## 653 591     85    30
    ## 654 592     40    40
    ## 655 593     60    60
    ## 656 594     75    65
    ## 657 595     47    65
    ## 658 596     77   108
    ## 659 597     50    10
    ## 660 598     94    20
    ## 661 599     55    30
    ## 662 600     80    50
    ## 663 601    100    90
    ## 664 602     55    60
    ## 665 603     85    40
    ## 666 604    115    50
    ## 667 605     55    30
    ## 668 606     75    40
    ## 669 607     30    20
    ## 670 608     40    55
    ## 671 609     55    80
    ## 672 610     87    57
    ## 673 611    117    67
    ## 674 612    147    97
    ## 675 613     70    40
    ## 676 614    110    50
    ## 677 615     50   105
    ## 678 616     40    25
    ## 679 617     70   145
    ## 680 618     66    32
    ## 681 619     85    65
    ## 682 620    125   105
    ## 683 621    120    48
    ## 684 622     74    35
    ## 685 623    124    55
    ## 686 624     85    60
    ## 687 625    125    70
    ## 688 626    110    55
    ## 689 627     83    60
    ## 690 628    123    80
    ## 691 629     55    60
    ## 692 630     65    80
    ## 693 631     97    65
    ## 694 632    109   109
    ## 695 633     65    38
    ## 696 634     85    58
    ## 697 635    105    98
    ## 698 636     85    60
    ## 699 637     60   100
    ## 700 638     90   108
    ## 701 639    129   108
    ## 702 640     90   108
    ## 703 641    115   111
    ## 704 641    100   121
    ## 705 642    115   111
    ## 706 642    105   101
    ## 707 643    120    90
    ## 708 644    150    90
    ## 709 645    125   101
    ## 710 645    145    91
    ## 711 646    130    95
    ## 712 646    170    95
    ## 713 646    120    95
    ## 714 647     72   108
    ## 715 647     72   108
    ## 716 648     77    90
    ## 717 648    128   128
    ## 718 649    120    99
    ## 719 650     61    38
    ## 720 651     78    57
    ## 721 652    107    64
    ## 722 653     45    60
    ## 723 654     59    73
    ## 724 655     69   104
    ## 725 656     56    71
    ## 726 657     63    97
    ## 727 658     95   122
    ## 728 659     36    57
    ## 729 660     56    78
    ## 730 661     50    62
    ## 731 662     73    84
    ## 732 663     81   126
    ## 733 664     35    35
    ## 734 665     22    29
    ## 735 666     52    89
    ## 736 667     50    72
    ## 737 668     68   106
    ## 738 669     38    42
    ## 739 670     45    52
    ## 740 671     65    75
    ## 741 672     65    52
    ## 742 673    100    68
    ## 743 674     82    43
    ## 744 675    124    58
    ## 745 676     80   102
    ## 746 677     48    68
    ## 747 678     48   104
    ## 748 678     48   104
    ## 749 679     80    28
    ## 750 680    110    35
    ## 751 681    150    60
    ## 752 681     50    60
    ## 753 682     52    23
    ## 754 683     72    29
    ## 755 684     48    49
    ## 756 685     80    72
    ## 757 686     54    45
    ## 758 687     92    73
    ## 759 688     52    50
    ## 760 689    105    68
    ## 761 690     60    30
    ## 762 691     75    44
    ## 763 692     53    44
    ## 764 693     73    59
    ## 765 694     38    70
    ## 766 695     55   109
    ## 767 696     89    48
    ## 768 697    121    71
    ## 769 698     59    46
    ## 770 699     77    58
    ## 771 700     65    60
    ## 772 701     92   118
    ## 773 702     58   101
    ## 774 703     50    50
    ## 775 704     50    40
    ## 776 705     75    60
    ## 777 706    100    80
    ## 778 707     80    75
    ## 779 708     70    38
    ## 780 709    110    56
    ## 781 710     66    51
    ## 782 710     66    56
    ## 783 710     66    46
    ## 784 710     66    41
    ## 785 711     90    84
    ## 786 711     85    99
    ## 787 711     95    69
    ## 788 711    100    54
    ## 789 712     69    28
    ## 790 713    117    28
    ## 791 714     30    55
    ## 792 715     70   123
    ## 793 716    131    99
    ## 794 717    131    99
    ## 795 718    100    95
    ## 796 719    100    50
    ## 797 719    160   110
    ## 798 720    110    70
    ## 799 720    160    80
    ## 800 721    110    70

## Primer boxplot

``` r
attach(pk)
att = boxplot(Attack, horizontal = TRUE)
```

![](tarea3_ayudantia_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
stats_att = boxplot.stats(Attack)
att
```

    ## $stats
    ##      [,1]
    ## [1,]    5
    ## [2,]   55
    ## [3,]   75
    ## [4,]  100
    ## [5,]  165
    ## attr(,"class")
    ##         1 
    ## "integer" 
    ## 
    ## $n
    ## [1] 800
    ## 
    ## $conf
    ##          [,1]
    ## [1,] 72.48624
    ## [2,] 77.51376
    ## 
    ## $out
    ## [1] 190 185 180 180 180 170 170
    ## 
    ## $group
    ## [1] 1 1 1 1 1 1 1
    ## 
    ## $names
    ## [1] "1"

``` r
stats_att
```

    ## $stats
    ## [1]   5  55  75 100 165
    ## 
    ## $n
    ## [1] 800
    ## 
    ## $conf
    ## [1] 72.48624 77.51376
    ## 
    ## $out
    ## [1] 190 185 180 180 180 170 170

Como se puede apresiar, ahora contamos con 800 datos, de los cuales 7
son “atipicos”, por lo tanto deben ser eliminados para poder hacer un
analisis mas acertado. ahora procedemos a eliminar dichos datos.

``` r
pk1 <- Attack[Attack < 170]
length(Attack) - length(pk1)
```

    ## [1] 7

``` r
boxplot(pk1, horizontal = TRUE)
```

![](tarea3_ayudantia_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

Ahora haremos lo mismo con los datos de velocidad

``` r
def = boxplot(Speed, horizontal = TRUE)
```

![](tarea3_ayudantia_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
stats_def = boxplot.stats(Speed)
def
```

    ## $stats
    ##      [,1]
    ## [1,]    5
    ## [2,]   45
    ## [3,]   65
    ## [4,]   90
    ## [5,]  150
    ## attr(,"class")
    ##         1 
    ## "integer" 
    ## 
    ## $n
    ## [1] 800
    ## 
    ## $conf
    ##          [,1]
    ## [1,] 62.48624
    ## [2,] 67.51376
    ## 
    ## $out
    ## [1] 160 180
    ## 
    ## $group
    ## [1] 1 1
    ## 
    ## $names
    ## [1] "1"

``` r
stats_def
```

    ## $stats
    ## [1]   5  45  65  90 150
    ## 
    ## $n
    ## [1] 800
    ## 
    ## $conf
    ## [1] 62.48624 67.51376
    ## 
    ## $out
    ## [1] 160 180

En este caso, son dos solamente los datos alejados, por ende los
eliminaremos.

``` r
pk2 <- Speed[Speed < 160]
length(Speed) - length(pk2)
```

    ## [1] 2

``` r
boxplot(pk2, horizontal = TRUE)
```

![](tarea3_ayudantia_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->
