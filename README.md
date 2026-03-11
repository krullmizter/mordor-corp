# 🛡️ Projekt Mordor Corp – NPoDS 2026

Ni har blivit anlitade som säkerhetskonsulter för att utföra ett pentest av Mordor Corp. Företaget står inför en stor auditering och behöver identifiera svagheter i sina system.

Ert mål är att analysera deras nätverk, servrar och källkod, dokumentera bristerna och sedan på bästa möjliga sätt åtgärda eller åtminsote rapportera problemen.

Subject: Info till konsulten
Hej,

Tack för att ni tar er an detta med kort varsel. Jag är mitt uppe i förberedelserna inför auditeringen och kommer att vara svår att nå framöver, så här är den information jag har för tillfället:

är ryggraden i vår verksamhet. Särskilt nöjda är vi med vår funktion för användarsök, som vi anser vara "top-of-the-line". Jag misstänker dock att det kan finnas gamla databastabeller kvarlämnade djupt i systemet.

Systemet byggdes för några år sedan, och ärligt talat har vi inte haft tid att se över säkerhetsuppdateringar sedan dess.

Ett akut problem: Jag har förlorat åtkomsten till mitt admin-konto (lösenordslappen är puts väck!). Men nå HSS eller liknande kanske finns kvar?

Om ni lyckas ta er in, prioritera att identifiera kritiska brister som vi måste åtgärda innan de externa revisorerna anländer.

Lycka till, vi räknar med er.

Mvh. Annatar | CEO, Mordor Corp

## Tekniska Förutsättningar

Innan du börjar behöver du ha följande installerat på din maskin:

- Git (för att klona repot och versionshantera dina egna fixar).
- Docker & Docker Compose (för att köra labbmiljön).

## Rapportering

För att nå full poäng krävs en tekniskt detaljerad rapport som följer dessa steg:

1. Rekognoscering
   1. Hitta offentlig information som kan vara till nytta.
      1. Detta steg ska utföras helt passivt.
   2. Analysera korrespondens, webbsidor och metadata.
   3. Inga aggressiva skanningar eller enumerering i detta skede.

2. Kartläggning
   1. Använd både manuella och automatiserade verktyg.
   2. Identifiera öppna tjänster, subdomäner och dolda kataloger.
   3. Lista mjukvaruversioner och leta efter kända sårbarheter (CVEs).
   4. Skapa en lista på möjliga attackvektorer in i systemet.

3. Fotfäste
   1. Försök ta er in i systemet baserat på er kartläggning.
   2. Dokumentera varje steg: Vilka exploits testades? Vilka fungerade?
   3. Notera även misslyckade försök.

4. Rättighetseskalering
   1. När ni väl är inne som en vanlig användare:
   2. Försök eskalera era rättigheter till root.
   3. Mål: Hitta och läs innehållet i /root/root.txt. Detta är beviset på total systemkontroll.

5. Fixa säkerhetsproblem
   1. Rapportera inte bara felen, försök fixa dom!
   2. Uppdatera sårbara bibliotek eller images.
   3. Platformen och dess tjänster ska fortsätta fungera.
      1. Att bara stänga av allt är inte en godkänd lösning, men en tillfällig "Maintenance"-sida är acceptabel under tiden ni patchar.

## Kom Igång

1. Starta miljöerna:
   Navigera till mappen där du klonade GitHub repon (mordor-corp) och kör:
   `docker-compose up -d --build`
2. Öppna din _attacker_ container:
   För att få tillgång till verktygen i din Kali-instans (headless), kör:
   `docker exec -it attacker /bin/bash`
3. Nå tjänsterna:
   1. **Från din egna dator:** Sök på `http://localhost` i webbläsaren.
   2. **Inifrån containrarna:** Använd det interna domännamnet `mordor-corp.fi`

## Felsökning & Uppdateringar

Om miljön börjar bete sig märkligt eller om du vill nollställa databasen:

```bash
docker-compose down -v
docker-compose up -d
```

_Varning: -v tar bort alla volymer, vilket innebär att ändringar i databasen rensas._

Om det kommer uppdateringar till projektet kör då:

```bash
git pull
docker-compose pull
docker-compose up -d
```

_Uppdateringar meddelas via Itslearning och Discord_

## Regler, Sekretess & Plagiat

- Containrarna körs i _bridge-mode_ med utökade rättigheter för nätverksanalys.
- Attackera **endast** de IP-adresser och containrar som tillhör Docker nätverket!
- Ange **källor** för de metoder ni använder, t.ex. om ni hittat någon tutorial på nätet eller exploit på GitHub, hänvisa med länk i rapporten (regelrätt källförteckning behövs inte)
- Det är **förbjudet** att avslöja fynd och metoder för era kurskamrater, eller för yngre studenter som inte ännu gått kursen.
- Det är **förbjudet** att att be om lösningar av kurskompisarna! Om ni kört fast, fråga läraren om tips (helst på lektionstid, nästsista lektionen ägnas åt arbete på projektet).

## Bedömmning & Inlämning

- **Deadline**: Söndag 5.4 kl.23:59
- Lämna in enskilt eller som grupp (max 2 pers) i PDF- eller Markdown-format via Itslearning.
  - Om du jobbar i grupp så anmäl dig och ditt par på Itslearning (Hacking Teams)
- Försenad inlömning bedöms, men med ett poängavdrag på -10% per påbörjad försenad vecka.

Max poäng: 60p
Tröskeln för godkänt kursvitord: 20p på kursprojektet

Rapportens kvalitet (Struktur, tydlighet, metodik): 30p
Root pwned (Hittat root.txt): 10p
Hittat alla andra CTF flaggor: 10p
Remediering: 10p
