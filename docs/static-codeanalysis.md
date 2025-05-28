# Statisk kode analyse

### ESLint
 ESLint er et statisk kodeanalyseværktøj der kan bruges til at analysere kode. 
 
 Her både læser og gennemgår ESLint koden,  for at finde fejl før koden bliver eksekveret.

#### Hvorfor bruge ESLint
- Fordi den sikrer, at hele teamet følger de samme kodestandarder og konventioner ved at alle medlemmer har ensartet kode.

- Den finder syntaksfejl, bugs og dårlige kodestile, før koden køres eller deployes.

- Den gør koden lettere at læse og vedligeholde fremadrettet.

- Den kan integreres i CI/CD pipelines, så kode automatisk tjekkes ved hver commit.


#### Eksempel
```python
rules: {
    'comma-dangle': ['error', 'always-multiline'],
    'eqeqeq': ['error', 'always'],
    'indent': ['error', 2],
    'no-eval': ['error'],
    'no-trailing-spaces': ['error'],
    'no-unused-vars': ['error'],
    'no-var': ['error'],
    'prefer-const': ['error'],
    'quotes': ['error', 'single'],
    'semi': ['error', 'always'],
  },
```

---------------------------------

### Refaktoring
Refaktoring er processen, hvor man ændrer koden internt for at forbedre dens struktur, uden at ændre dens eksterne opførsel. 

#### Hvorfor bruge refaktoring
- Gør det lettere for andre og dig selv at forstå koden.

- Gør koden mindre kompleks og nemmere at teste.

- Gør det lettere at tilføje nye funktioner senere.

- Fjerner "hurtige løsninger" og dårlige mønstre.

#### Eksempel

Kode før brug af refaktoring
```python
const sortBy = ref('none');

const sortedTemplates = computed(() => {
  let arr = [...templates.value];
  if (sortBy.value === 'newest') {
    arr.sort((a, b) => parseDate(b.date) - parseDate(a.date));
  } else if (sortBy.value === 'oldest') {
    arr.sort((a, b) => parseDate(a.date) - parseDate(b.date));
  } else if (sortBy.value === 'mostUsed') {
    arr.sort((a, b) => b.uses - a.uses);
  }
  return arr;
});

```
^^ Hver sorteringsregel kræver et nyt if eller else if-statement.

^^ Hvis man vil tilføje en ny sorteringsmetode, skal man tilføje endnu en else if-blok.

^^ Koden bliver hurtigt lang og svær at læse, hvis der kommer flere sorteringsmuligheder.

----------------------------------------
#### Eksempel

Kode efter brug af refaktoring
```python
const sortBy = ref('none');

const sortFunctions = {
  newest: (a, b) => parseDate(b.date) - parseDate(a.date),
  oldest: (a, b) => parseDate(a.date) - parseDate(b.date),
  mostUsed: (a, b) => b.uses - a.uses,
  none: () => 0, // Ingen sortering
};

const sortedTemplates = computed(() => {
  const arr = [...templates.value];
  const sortFn = sortFunctions[sortBy.value] || sortFunctions.none;
  return arr.sort(sortFn);
});
 
```
^^ Alle sorteringsfunktioner er samlet ét sted.

^^ Det er nemt at se, hvilke sorteringer der findes, og hvordan de fungerer.

^^ Hvis man vil tilføje en ny sortering, skal man kun tilføje en ny funktion til sortFunctions-objektet.

^^ Man behøver ikke ændre selve sorteringskoden eller tilføje flere if-statements.

^^ Man kalder kun arr.sort(...) én gang, uanset hvilken sortering der vælges.


------------------------------------
#### Principper
- Lav små, sikre ændringer, og test ofte.

- Koden skal virke på samme måde før og efter refaktoring.

- Brug tests til at sikre, at du ikke har ødelagt noget.

####Eksempler på kode principper at følge:
- DRY (dont repeat yourself)
^^Undgå at have den samme kode flere steder

- KISS (keep it simple, stupid)
^^Hold det enkelt og overskueligt så det er nemt at vedligeholde

- SRP (single responsibility principle)
^^Èn klasse eller funktion til ét ansvar

- YAGNI (you aren't gonna need it)
^^Hold fokus på det mest nødvendige


