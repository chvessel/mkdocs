# Git workflow

### Branch strategi
I DBI projektet brugte vi en "developer branch" strategi, hvor hvert gruppemedlem arbejdede på samme developer branch som til sidst blev merget med main/master.
#### Branch struktur
```
Main/master 
├── Developer branch
└── Feature branch
```

Selvom at vi begge arbejdede på den samme developer branch var vi obs på at undgå konflikter så vidt muligt. Dette gjorde vi ved ikke at arbejde på de samme views samtidig.

----------------------------------

### Commits

Et commit betyder at du gemmer en version af projektet med en besked, der forklarer, hvad du har ændret. Hellere små men regelmæssige commits end få større commits.

#### Hvorfor 
- Man mister ikke sine ændringer, hvis noget går galt.

- Mindre commits gør det nemt at se, hvornår en fejl opstår.

- Andre kan nemt se, hvad man har lavet, og hvorfor.

- Hvis noget går galt, kan man nemt gå tilbage til en tidligere version.

---------------------------------------

### Dårlige eksempler på commits
```
 "tilføjet ændringer"
 "fikset fejl"
 "opdateret ændringer"
 "asdf"
 "rettet login fejl"
```
^^siger intet om hvad der er ændret

^^hjælper ikke andre personer med at forstå hvad der er lavet.


### Gode eksempler på commits
```
 "Ret fejl hvor login fejlede med korrekt adgangskode"
 "Tilføj søgefunktion til brugerliste"
 "Opdatér README med installationsvejledning"
 "Fjern ubrugte import fra TemplatePage.vue"

```
^^Det beskriver tydeligt hvad der er ændret

^^Giver andre en klar forståelse for ændringerne i "projektet"


