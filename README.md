# AI_IoT_Kunskapskontroll_1
Redovisning av de tre delarna av kunskapskontroll 1 för kursen AI och IoT. 

# Del 1

# 1. Antag att du ska implementera en AI-baserad chatbot för kundsupport. Beskriv arbetsprocessen utifrån design thinking-modellens olika faser och förklara syftet med varje fas.

Stegen Empathize, Define, Ideate, Prototype och Test är ganska tydliga "instruktioner" för en till synes linjär arbetsprocess som egentligen handlar om iteration. 

##  1. Empathize
Här handlar det om att ta till sig grunden för problemet/projektet, skapa en helhetsbild så att man vet vad det handlar om. Vara i verksamheten, tala med personerna i kundsupporten och följa några ärenden igenom processen. Här får man se saker med "nya ögon" för att upptäcka insikter som användarna själva inte alltid är medvetna om.

För ett chatbot-projekt kan det handla om att studera interaktionen med kundsupporten, och se hur tydligt kunderna själva formulerar sina problem.Till det kan man göra intervjuer med både kunder och supportpersonal samt försöka gå på djupet och förstå deras frustrationer eller önskemål bättre.

##  2. Define
Ta fram ett tydligt ramverk för projektet, med en grundlig beskrivning av vad målet är med projektet, *vem* som är målgruppen för prjektet, vilka *behov* som finns och vilka *insikter* som har framkommit i Empathize-fasen. Ett utmärkt sätt kan vara att göra "stream of consciousness"-anteckningar så att man fritt kan få fram allt som man upplevde i fas 1 - med bilder, citat, etc. Genom att skapa en "Point-of-View" får man klarhet och fokus med en meningsfull och handlingskraftig problemformulering.

##  3. Ideate
Nu är det dags att skapa en serie åtgärdsförslag där man jobbar brett och använder fantasi för att hitta även svar som kanske inte omedelbart kan vara självklara. Kreativiteten är viktigare än genomförbarhet - idéerna ska flöda fritt!

I det aktuella projeketet kan det vara bra med  brainstorming/mindmapping för att hitta förslag på chatbotens personlighet, funktioner och användargränssnitt. 

När man fått ihop ett rejält grundmaterial är det dags att sovra och plocka med sig ett par-tre olika alternativ vidare till nästa fas. 

##  4. Prototype
Nu är det dags att ta fram lite enkla och billiga ”artefakter” (som det står i materialet) för att besvara frågor som tar projektet närmare en slutgiltig lösning. Här handlar det om att tänka, kommunicera och våga misslyckas. Prototyperna kan vara vad som helst som användarna kan interagera med – en storyboard, en whiteboard med olika ”vägar” att följa eller till och med ett rollspel där man får låtsas vara chatbot.
    
De olika prototyperna ska ha tydliga mål – vad är det man testar? Handlar det om tonlägen? Logiska menyval? O.s.v.

Eftersom hela processen är iterativ, främst steg 4 och 5, bör prototyperna inte vara för omfattande och man ska inte ”gifta sig” med dem utan våga släppa taget. 

##  5. Test
“Testing is an opportunity to learn about your solution and your user.”

I testfasen samlar man in feedback och lär sig mer om både lösningen och användarna. Kanske ska man formulera om sin POV (problembeskrivning) om det behövs?

För chatboten kan användarna få interagera med prototypen i en realistisk situation utan några instruktioner så att man kan se hur de använder chatboten (rätt eller fel) och i allmänhet vara "a fly on the wall" och bara lyssna.

##  Iteration
Processen ser till en början ut att vara ganska rättfram med en linjär progression, men är i praktiken tvärtom mycket iterativ. Hela processen kan behöva gås igenom från början till slut och man kan iterera fram och tillbaka mellan olika faser i de olika stegen.
 

    
# 2. Beskriv skillnaden mellan ett teknikdrivet och ett användarcentrerat utvecklingssätt.

Skillnaden handlar i grunden om angreppssättet - ska man utveckla utifrån användarens upplevelse och behov eller ska man fokusera på teknikens kapacitet och funktion? 

I ett användarcentrerat utvecklingssätt formulerar man problemet mer fokuserat, baserat på insikter, och arbetar iterativt så att man lär sig och testar fram och tillbaka tills man når sitt mål.

Teknikdriven utveckling är tvärtom bred eller utgår från tekniska krav med ett fokus på att färdigställa en slutprodukt. 

I princip skulle man kunna säga om att det handlar om att antingen leverera på ett upplevt behov eller på en teknisk konstruktionsritning. 
# 3. Ge exempel på hur IoT-data kan användas inom Business Intelligence för att stödja affärsbeslut. Beskriv vilken typ av data som samlas in och hur den kan analyseras.
Ett exempel skulle kunna vara som jag nämnde på föreläsningen. Genom att samla in data om hur laddstolpar används kan man få en grund för ett investeringsbeslut om fler laddstolpar. Ett annat exempel kan vara det som jag gör i min Del 3 - att basera ett beslut om installation av ett hushållsbatteri på flera års data om elförbrukning, elproduktion och solinstrålning för att dels se hur det hade kunnat se ut historiskt (simulering) och dels skapa en modell som kan ta olika parametrar och leverera sannolikheter för vinst/förlust på en sådan investering. 
# 4. Hur skiljer sig IoT-data från traditionell affärsdata och vilka konsekvenser får detta för BI-arbete?

Skillnaderna är flera. Bland annat handlar det om volymer - där IoT-data inte sällan kan vara flera storleksordningar större än affärsdata. Det handlar också om att IoT-data är en strid ström av data medan affärsdata ofta mer handlar om batcher, vilka dessutom sannolikt är betydligt bättre strukturerade än den helt ostrukturerade strömmen av IoT-data.

Även konsekvenserna för BI-arbete är flera. Det krävs stora lagringsytor för IoT-data och en stor insats att tvätta/bearbeta dessa för att få några insikter. ETL-arbetet som man ofta lägger stor vikt vid i BI går kanske inte att göra när det handlar om ögonblicksbilder med ett lättflyktigt värde. Realtidsanalyser kräver också en annan arbetsordning än schemalagda SQL-jobb och uppdatering av dashboards kvartalsvis.

En poäng kan också vara att man behöver värdera "brus", hantera outliers och sensorfel. För underhållssyften kan det kanske behövas en prediktiv modell som i realtid kan styra om åtgärder när dataflödet förändras som en signal på att något händer. 

Som BI Analyst med Power BI i högsta hugg kommer det också att handla om att glömma allt om historiska trender och i stället bygga dashboards som mer reagerar när något faller utanför de ramar man har angivit. Man får helt enkelt kanalisera sin inre data engineer än sitta lugnt i båten som BI Analyst. 


# 5. Hur kan AI möjliggöra nya affärsmodeller snarare än enbart effektivisering?

Det här är som du nämnde på någon föreläsning ett mycket brett område. Och som dessutom saknar gränser om man har lite fantasi. 

Om jag först ska nämna ett exempel på en effektivisering så kan det vara att skapa en RAG-modell som sköter företagets support i första linjen och där bara problem som inte kan lösas med "standardsvar" går vidare till en tekniker. Det är ingen ny affärsmodell, men en utmärkt besparing för ett företag som har många supportärenden. 

Ett exempel på en ny affärsmodell (eller ... "ny" är kanske att ta i, men inte fullt ut realiserad än iaf) kan vara som vi diskuterade på föreläsningen. Man kopplar helt sonika ihop sina devices och matar in deras IoT-data i en AI-modell som agerar "överrock" för inköp i dagligvaruhandeln. Kylskåpet meddelar min AI-modell om vad jag saknar eller vad som håller på att gå ut, AI-modellen fyller på inköpslistan i min scanner på ICA - i rätt ordning för den affär jag är i och skickar notiser till min mobil när det är dags att laga mat, med färdiga förslag utifrån vad jag har hemma. Den kan också hålla reda på var jag är och skicka en notis när jag kör förbi affären om jag behöver fylla på med något "akut".


# 6. Hur tror du en kommun hade kunnat utnyttja datan som samlats in (se länk nedan) och hur påverkar det invånarna tror du? https://www.linkedin.com/posts/hoganas-kommun_smartcity-digitalisering-trafiksaeukerhet-activity-7415390506920419328-JVnZ
Med realtidsdata om trafikflöden, hastigheter och rörelsemönster kan Höganäs kommun transformera verksamheten på flera plan. Man nämner själva en stärkt trafiksäkerhet, bättre framkomlighet och en i allmänhet tryggare, smidigare och mer hållbar stad. 

Den kontinuerliga strömmen av data gör att Höganäs kan justera trafikljusens cykler baserat på faktiska belastningstoppar för att minska köbildning – till skillnad mot de statiska intervall som normalt används för trafikljus. 

Man kan också fatta beslut om strategiska investeringar där nya cykelvägar eller övergångsställen placeras där folk faktiskt rör sig, snarare än var man gissar att de rör sig.

En viktig poäng är också att man kan bedriva en proaktiv säkerhetsverksamhet genom att identifiera platser där hastighetsöverträdelser är vanliga och det ofta sker incidenter (olyckor eller ”nästan olyckor”. Dessa kan man få fram om man har IoT-data som påvisar plötsliga inbromsningar eller ovanliga rörelsemönster. 

Fokuset på hållbarhet kan handla om att koppla trafikdata till luftkvalitet och buller – där kommunen vid hög belastning och dålig luftkvalitet helt kan styra om trafiken.

En ”side note” i sammanhanget är att den beskrivna design thinking du nämnt är mycket lämplig här. Med ett användarcentrerat arbetssätt kan man säkerställa att man löser invånarnas faktiska problem och inte bara har en helikopterverksamhet där man roar sig med tekniska möjligheter utan verkliga positiva effekter för invånarna. 

Man kan tänka sig en arbetsgång där man först försöker förstå invånarnas frustrationer i trafiken (empathize), definiera specifika utmaningar (define), hitta på massor av intressanta/roliga idéer (ideate/prototype) och sedan använder IoT-data för att simulera olika lösningar innan man de facto börjar gräva upp gator eller installera teknikstolpar (test).
