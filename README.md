# 🛡️ NPoDS 2026 Kursprojekt: Mordor Corp

Ni har blivit anlitade som **säkerhetskonsulter** för att utföra ett penetrationstest (pentest) av företaget det fiktiva företaget **Mordor Corp**.

Företaget står inför en kommande auditering den **6.4.2026** och behöver snabbt identifiera potentiella svagheter i sina system.

Er uppgift är att:

- **Analysera** företagets nätverk, servrar och källkod
- **Identifiera** brister, sårbarheter och felkonfigurationer
- **Dokumentera** och **rapportera** det ni hittar
- **Föreslå** och **implementera** säkerhetsåtgärder

Sammanfattat är målet att visa era offensiva och defensiva säkerhetskunskaper, samt er förståelse av källkod och hur nätverk och dess protokoll fungerar.

## 📧 E-post meddelande från Mordor Corp

```
Ämne: Info till säkerhetskonsulten

Hej,

Tack för att ni tar er an detta med kort varsel. Jag är mitt uppe i förberedelserna inför auditeringen, som äger rum redan den 6.4.2026, och kommer därför att vara svår att nå framöver, så här är den information jag har för tillfället:

Vår interna plattform är ryggraden i verksamheten. Vi är särskilt stolta över vår funktion för användarsökning, som vi anser vara “top-of-the-line”. Samtidigt misstänker jag att det kan finnas gamla databastabeller någonstans djupt ner i systemen.

Systemet utvecklades för några år sedan och, om jag ska vara helt ärlig, har vi inte haft tid att se över säkerhetsuppdateringar sedan dess.

Ett akut problem: Jag har förlorat åtkomsten till mitt admin-konto (lösenordslappen är puts väck!). Men nå HSS eller liknande kanske finns kvar?

Om ni lyckas ta er in, prioritera att identifiera kritiska sårbarheter som vi måste åtgärda innan revisorerna anländer.

Lycka till, vi räknar med er!

Mvh,
Sauron
VD, Mordor Corp
```

## ⚙️Tekniska förutsättningar

Innan du börjar behöver du ha följande installerat på din dator:

- **Git** (för att klona och versionshantera uppdateringar av kursprojektet)
- **Docker** (för att köra labbmiljöerna)

Bra-att-veta Docker kommandon:

```bash
# Starta containrarna i bakgrunden
docker compose up -d

# Stanna alla containrar
docker compose down

# Uppdatera containrarna om Docker Hub images blir uppdaterade
docker compose pull

# Kör detta kommando i din terminal för att komma åt någon körande container instans
docker exec -it containers_namn /bin/bash

# Kom åt attacker containern (Kali Linux) som körs, och starta ett bash shell
docker exec -it attacker /bin/bash
```

## ✍️Rapportering

För att nå full poäng krävs en tekniskt detaljerad rapport som följer dessa steg:

### 1. Rekognoscering (Reconnaissance)

**Syfte**: Samla information utan att aktivt attackera systemen

- **Identifiera** offentlig information (OSINT) som kan vara till nytta
  - Detta steg ska utföras helt passivt
  - Undvik aggressiva skanningar eller enumerering i detta skede
- **Analysera**:
  - Hemsidor
  - Metadata
  - Konfigurationsfiler
  - Korrespondens eller läckta uppgifter

### 2. Kartläggning (Enumeration & Mapping)

**Syfte**: Identifiera attackytor

- Använd både manuella och automatiserade verktyg för att:
  - Identifiera öppna tjänster
  - Hitta dolda kataloger och endpoints
  - Upptäcka subdomäner
  - Identifiera mjukvaruversioner
  - Söka efter kända sårbarheter (CVE)
- Skapa en lista på möjliga attackvektorer in i systemet.

### 3. Fotfäste (Initial Access)

**Syfte**: Försök ta er in i systemet baserat på er kartläggning

- Noggrant dokumentera:
  - Vilka sårbarheter som testades
  - Vilka exploits som användes
  - Vilka metoder som fungerade
  - Vilka försök som misslyckades
- Denna dokumentation är en viktig del av rapporten!

### 4. Rättighetseskalering (Privilege Escalation)

**Syfte**: Eskalera era rättigheter

- När ni har fått åtkomst till systemet:
  - Försök **eskalera** era rättigheter
  - **Identifiera** svagheter

**Mål**: Lokalisera och läs `root` flaggan: `/root/root.txt`. Denna flagga bevisar total systemkontroll.

### 5. Åtgärda säkerhetsproblem (Remediation)

**Syfte**: Rapportera inte bara problemen, försök att åtgärda dom
Exmpel åtgärder:

- Uppdatera sårbara versioner
- Korrigera konfigurationsfel
- Förbättra autentisering

⚠️ Viktigt:

- Plattformen och dess tjänster ska **fortsätta fungera**
- Att endast stänga ner systemet räknas **inte som en godkänd lösning**.
- En temporär **maintenance-sida** är dock acceptabel under tiden ni patchar systemet.

## 🚀 Kom igång

⚠️ Vi kör allting i så kallat _headless mode_. Alltså vi har inget användargränsssnitt/GUI bara terminalfönster och CLI

1.  Klona GitHub repon för kursen (https://github.com/krullmizter/mordor-corp) till er dator
2.  Navigera lokalt till projekt mappen (mordor-corp)
3.  Kör `docker compose up -d`
  - Kommandot går igenom detta repos `docker-compose.yml` fil
  - Detta i sin tur laddar ner Docker alla images, och kör igång containrarna i bakgrunden på din maskin
  - Då allt är klart så ska du få en liknande output i ditt terminal fönster:
```
[+] up 26/26
 ✔ Image krullmizter/mordor-corp:website-v1  Pulled                                                                                   2.0ss
 ✔ Image krullmizter/mordor-corp:db-v1       Pulled                                                                                   2.0ss
 ✔ Image krullmizter/mordor-corp:attacker-v1 Pulled                                                                                   14.8s
 ✔ Network public                            Created                                                                                  0.0s
 ✔ Network internal                          Created                                                                                  0.0s
 ✔ Container db                              Created                                                                                  7.8s
 ✔ Container website                         Created                                                                                  7.8s
 ✔ Container attacker                        Created                                                                                  7.8s
```

4. Få tillgång till din Kali container: `docker exec -it attacker /bin/bash`

Då öppnas en instans av Docker attacker containern.
Inuti den kan du köra Linux och vissa Kali kommandon.
Några fiffga kommandon 😉:
- nmap
- sqlmap
- dirb
- netcat
- curl
- find

4. Få tillgång till Mordor Corp hemsidan

Efter att Docker och containrarna körs, så kan du nå kursprojketets hemsida:
   
**Från din egen dator**

- Du kan alltid nå hemsidan via: `http://localhost` i din webbläsare
- Du kan editer host filen på din dator så att du kan använda domännamnet `mordor-corp.fi` i din webbläsare (valfritt men rekommenderat)

⚠️ Hosts-filen skriver över DNS – `mordor-corp.fi` kommer alltid att peka på din localhost så länge denna rad finns kvar.

Om du vill använda ett mer realistiskt domännamn i din webbläsare behöver du lägga till en lokal DNS ändring på din värddator

**Windows**
1. Öppna följande fil som administratör: `C:\Windows\System32\drivers\etc\hosts`
2. Lägg till:

```
127.0.0.1 mordor-corp.fi
127.0.0.1 www.mordor-corp.fi
```

**macOS / Linux**
1. Öppna följande fil: `/etc/hosts`
2. Lägg till:
```
127.0.0.1 mordor-corp.fi
127.0.0.1 www.mordor-corp.fi
```

**Från Docker**: `mordor-corp.fi`
- I alla dina containrar så kan du hänvisa till hemsidan med följande: `http://mordor-corp.fi`, `http://www.mordor-corp.fi`, `website`
- Exmpelvis: `nmap mordor-corp.fi` kör `nmap`

## 💥Felsökning

Om Docker miljöerna börjar bete sig märkligt eller om du vill nollställa något:

```bash
docker-compose  down  -v
docker compose up -d
```

⚠️Varning: `-v` raderar alla Docker volymer, vilket innebär att databasen återställs.

## 🔄Uppdateringar

Om det kommer uppdateringar till kurs projektet, antingen till **GitHub** eller **Docker Hub**, kör då i projekt mappen:

```bash
git pull
docker compose pull
```

ℹ️ Uppdateringar meddelas både via **Itslearning** och **Discord**

## 📜 Regler, sekretess och plagiat

- Containrarna körs i **bridge-mode** med utökade rättigheter för nätverksanalys.
- Attackera **endast** IP-adresser och containrar inom Docker-nätverket.
- Ange **källor** för metoder eller exploits ni använder (t.ex. tutorials eller GitHub-projekt).
- Det är **förbjudet att dela lösningar eller metoder** med andra studenter.
- Det är **förbjudet att be kurskamrater om lösningar**

**Om ni kör fast**: Fråga läraren, via Discord, Itslearning eller e-post, om hjälp

## 📊 Bedömning och inlämning

**Deadline**:

- Söndag 5.4 kl. 23:59
- Försenad inlämning bedöms, men med ett poängavdrag på **-10%** per påbörjad försenad vecka.

**Kursprojektet kan göras**:

- Individuellt
- I grupp (max 2 personer)
  - Anmäl dig och ditt par på Itslearning (_Kursprojekt mappen -> Hacking Teams_)

**Rapporten** lämnas in på **Itslearning** (_Kursprojekt mappen -> Kursprojekt: Mordor Corp_) som en PDF eller Markdown fil

## 🧮 Poängsättning

Max poäng: **60p**

- Tröskeln för godkänt kursvitsord kräver minst **20p** på kursprojektet!
- För att nå full poäng krävs en **tekniskt detaljerad rapport** som dokumenterar hela arbetsprocessen.
- Rapporten bör följa en strukturerad metodik liknande en verklig penetrationstestprocess.

| Typ                                                                | Poäng |
| ------------------------------------------------------------------ | ----- |
| Rapportens kvalitet och innehåll (struktur, metodik och tydlighet) | 30    |
| Total Systemkontroll / Root pwnd flagga (`root.txt`)               | 10    |
| Hittat alla andra CTF flaggor (6st)                                | 10    |
| Säkerhetsåtgärder (remediation)                                    | 10    |
