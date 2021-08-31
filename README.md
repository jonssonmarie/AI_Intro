#  Arbetsflöde för AI-projekt - husförsäljning

## Samla in data, format, spara data
Data kan komma från en källa som har det man söker efter tex Booli.se som har data på husförsäljningar för professionella användare.  Antingen samlar man in data kontinuerligt, i arkiverad form, eller som strömmande data. Boolis data är på ca 1 GB och den är redan formaterad och kräver inte så mycket kapacitet. Eller så får man samla in data manuellt. 
Data kan man spara i en databas/server, molnet eller hantera strömmande. 
Det format man väljer beror på vad källan erbjuder och vad man kan konvertera till.
Boolis svarsformat är JSON, kodat som UTF-8. Men man kan på andra ställen använda tex csv, då csv har versionshantering, alternativt Excel.

## Visualisera data
Visualisera resultatet från modellen kan man göra med olika plottar, diagram, grafer. Det beror på vad som är bäst för ändamålet. 

## Bearbeta data till rätt format
Förbereda data handlar ofta om att konvertera olika datavärden till samma skala, men man måste kolla så att inte skalan har betydsle. Även partiskhet behöver analyseras då det påverkar modellen. Bla behöver NaN och punkter som sticker ut ska sorteras bort.

Exempel på variabler: 
##### Responsvariabel  
Pris
##### Förklarande/residual variabler  
Boarea  
Tomtarea  
Byggår  
Hav  
Rum  
Sålt (sålt/osålt)  
Hus (villa, radhus/kedjehus)  
Samhällsservice – bank, post, affär, bibliotek, sjukvård, skola, dagis, buss/tåg är ytterligare variabler att ta med, dock ej är med i studien^1.

I studiens första regression togs inga variabler bort då de alla kan tänkas ha en inverkan på slutpriset för ett hus. 
För att undersöka om några variabler korrelerar med varandra kan man göra en scatterplott. En scatterplott kan visa om det finns ett linjärt samband mellan variablerna. I studien^1 hittades ett linjärt samband mellan boarea och rum. Då ersattes variabeln Rum med variabeln Borum^1. 

Efter studie av residualplottar får man besluta sig för om man behöver logaritmera responsvariabeln för att få residualvariablerna mer jämna.
Bor man på en mindre ö kanske inte Hav/sjövariabeln ska vara med. I ett område med god samhällsservice ska kanske inte den variabeln vara med. Man får titta på vad som är vettigt på det område man tar körningen på och hur man kan identifiera dessa. 

Stepwise regression kan användas som nästa steg för att selektera bort variabler i modellen.
Sen får man välja vilken nivå på normalfördelningen man vill ha. I studien valde man bort 5% nivån och då försvann alla utom tre variabler. 

Om normalfördelningsplotten visar att punkterna ligger runt linjen i figuren så är det dags för nästa steg. Studera residualplottarna igen för de enskilda variablerna för att se om några punkter sticker ut och som ska tas bort.

När man kör en multipel linjär regression så vill man inte att två eller flera variabler ska korrelera med varandra då deras skattningar kan bli osäkra. För att analysera hur flera variabler korrelerar med varandra kan man använda scatterplot. Man får då en överblick över hur de olika variablerna står i relation till varandra. Korrelerar variablerna med varandra får man ersätta dem med en ny variabel, bestående av en kombination av de två. 

Nästa steg är själva träningen av modellen. Då utnyttjar man endast träningsdata och algoritmen får skapa en modell som förutspår rätt svar. Huvudaktiviteten under träningen är att göra inställningar, vilket kallas för ”hyperparameterization” på engelska.
Använder man strömmande data så kan man göra på två olika sätt. 
1. Fintrimmar befintliga modeller med ny data. 
2. Bygger nya modeller och tränar med ny data.

Studien^1 länk: https://kurser.math.su.se/pluginfile.php/20130/mod_folder/content/0/Kandidat/2015/2015_19_report.pdf?forcedownload=1


## Hur fungerar linjär regression
Linjär regression är en maskininlärningsalgoritm som baseras på bevakad inlärning. Den sätter ett predikterat målvärde baserad på oberoende variabler och den används främst för att hitta beroenden mellan variablerna och prognosen. Linjär regression finner alltså ut det linjära förhållandet mellan x (indata) och y (utdata).

https://www.geeksforgeeks.org/ml-linear-regression/#:~:text=Linear%20Regression%20is%20a%20machine%20learning%20algorithm%20based%20on%20supervised%20learning.&text=Linear%20regression%20performs%20the%20task,)%20and%20y(output)


## Driftsättning av modell
Det finns många olika lösningar för att driftsätta och underhålla AI modeller.
Om man behöver något enkelt och billigt så finns tex Flask, är du företagare med tillräckliga resurser (kunskap och folk)  så kan AWS, Azure eller GCP passa bättre. Har företaget/du större krav så kanske Oracle, IBM eller Goggle Cloud passar. Om du vill ha en end-to-end lösning kan AutoML passa. Det finns hur många som helst på marknaden. 
Den kritiska faktorn för att lyckas få ut sin AI modell på marknaden och i produktion är förmågan att samarbeta och iterera som team.

https://stackoverflow.blog/2020/10/12/how-to-put-machine-learning-models-into-production/
https://towardsdatascience.com/10-ways-to-deploy-and-serve-ai-models-to-make-predictions-336527ef00b2

## Teknologier under maskininlärningsprocessen
Maskininlärning bygger på att undersöka och jämföra stora datamängder för att hitta mönster.  
Bevakad inlärning - algoritmen får data behandlad av människor.  
Oövervakad inlärning - algoritmen får obehandlad data och kan hitta mönster själv.  
Förstärkt inlärning - algoritmen får en uppsättning regler och begränsningar och lär sig själv hur man bäst uppnår målen.

https://techworld.idg.se/2.2524/1.699032/ai-sa-funkar/sida/5/sa-funkar-maskininlarning--steg-for-steg
https://hitechglitz.com/sweden/skillnaden-mellan-ai-och-maskininlarning-forklaras/
