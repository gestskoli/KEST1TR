# Skriftur í Linux (bash scripting)

## Skrifað á skjá
Til að skrifa á skjá er skipunin ```echo``` notuð.
```bash
echo Texti
echo "Texti með bilum"
```
Ef skrifa á út útkomu úr skipun þar annaðhvort að setja ` utan um skipunina eða $().
```bash
echo "Í dag er `date`"
echo "Í dag er $(date)"
```
## Breytur
Breytunöfn mega byrja á bókstaf eða undirstriki (_)
### Gildi sett í breytur
```bash 
tala=123
texti=ABC
```
Nota má skipunina ```read``` til að lesa inn frá notanda.
```bash
echo -n "Hvað heitir þú? "
read nafn
echo "Þú heitir $nafn"
```

### Lesið úr breytu
Þegar lesið er úr breytum þarf að setja ```$``` fyrir framan breytuna
```bash
echo $tala
echo "Þrír fyrstu stafirnir í stafrófinu eru $texti"
```
## Samanburðar- og rökvirkjar fyrir ```test```
Þegar bera þarf saman hluti í bash er notað ```test```.
```bash
a=10
b=20
test $a -eq $b
```
```bash
test -f ~/skra.txt
# athugar hvort skráin skra.txt er til í heimasvæðinu
```

Í staðinn fyrir að skrifa ```test``` má nota ```[  ]```.
```bash
a=10
b=20
[ $a -eq $b ]
```
```bash
[ -f ~/skra.txt ]
# athugar hvort skráin skra.txt er til í heimasvæðinu
```

### Samanburðarvirkjar
| Python | bash |
| --- | --- |
| == | -eq |
| != | -ne |
| < | -lt |
| <= | -le |
| > | -gt |
| >= | -ge |

### Rökvirkjar
| Python | bash |
| --- | --- |
| and | -a |
| or | -o |
| not | ! |

## Skriftuskrár
Fyrsta lína í öllum skrám sem innihalda bash skriftu þarf að vera ```#!/bin/bash```. Það segir stýrikerfinu að nota bash til að túlka skriftuna. Venja er að hafa endinguna ```.sh``` á skrám sem innihalda skriftur. Skráin verður líka að vera keyranleg (e. executable) og er það gert með ```chmod``` skipuninni:
```bash
chomod +x nafnið-á-skránni
```
## Skilyrðissetningar
### if-elif-else-fi
```bash
if [ skilyrði ]
then
    gera það sem á að gerast ef skilyrðið er satt
elif [ annað skilyrði ]
then 
    gera það sem á að gerast ef annað skilyrðið er satt
else
    gera það sem á að gerast ef skilyrðin eru ósönn
fi

# Annar ritháttur
if [ skilyrði ]; then
    gera það sem á að gerast ef skilyrðið er satt
elif [ annað skilyrði ]; then 
    gera það sem á að gerast ef annað skilyrðið er satt
else
    gera það sem á að gerast ef skilyrðin eru ósönn
fi
```
Dæmi:
```bash
#!/bin/bash
echo -n "Hver er aldur þinn: "
read aldur
if [ $aldur -ge 17 ]
then
  echo "Þú mátt keyra bíl"
else
  echo "Þú mátt ekki keyra bíl"
fi
```
### case-esac
```bash
#!/bin/bash
echo -n "Sláðu inn 1, 2 eða 3: "
read val
case $val in
1)
  echo "þú valdir 1"
  ;;
2)
  echo "þú valdir 2"
  ;;
3)
  echo "þú valdir 3"
  ;;
*)
  echo "þú valdir eitthvað annað"
esac
```
## Lykkjur
### for
```bash
#!/bin/bash
afangar="FORR1FG KEST1TR VEFÞ1VG"
for afangi in $afangar
do
  echo "Ég er í $afangi"
done

# Eða
#!/bin/bash
afangar="FORR1FG KEST1TR VEFÞ1VG"
for afangi in $afangar; do
  echo "Ég er í $afangi"
done
```
### while
```bash
#!/bin/bash
i=0
while [ $i -lt 10 ]; do
  echo $i
  i=$(( $i + 1 ))
done
```
## Innbyggðar breytur
### ```$?``` niðurstaða síðustu skipunar
```bash
[ 1 -ne 1 ]
# $? inniheldur 1 (villa)
[ 1 -eq 1 ]
# $? inniheldur 0 (ekki villa)
```
### ```$1```, $2, $3 o.s.frv. eru færibreytur sem hægt er að taka inn þegar skrifta er keyrð.
```bash
#!/bin/bash
echo $1
```
þegar svo er kallað á skriftuna ```./skrifta.sh abc``` skrifar hún út abc.
### ```$EUID``` segir til um hvort notandi er root
Ef breytan inniheldur 0 er notandi með root réttindi annars ekki.

