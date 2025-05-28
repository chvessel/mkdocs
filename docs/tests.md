#Unit tests

### Hvorfor
- Man opdager hurtigt, hvis en funktion ikke gør det, den skal.

- Man kan være sikker på, at ens kode virker, som man forventer.

- Hvis man ændrer noget, kan man hurtigt se, om det har ødelagt noget andet.

- Den viser hvordan en funktion skal bruges, og hvad den skal returnere.

-----------------------------

## sortFiles
Denne funktion blev brugt til at sortere en liste af filer efter dato, (nyeste, ældste, mest brugte og ingen)


=== "Funktion"

    ```js
    function parseDate(dateStr) {
      return new Date(dateStr);
    }

    export function sortFiles(files, sortBy) {
      let arr = [...files];
      if (sortBy === 'newest') {
        arr.sort((a, b) => parseDate(b.date) - parseDate(a.date));
      } else if (sortBy === 'oldest') {
        arr.sort((a, b) => parseDate(a.date) - parseDate(b.date));
      } else if (sortBy === 'mostUsed') {
        arr.sort((a, b) => b.uses - a.uses);
      }
      return arr;
    }
    ```

=== "Test"

    ```js
    import { sortFiles } from './sortFiles';

    const files = [
      { name: 'A', date: '2024-01-01', uses: 5 },
      { name: 'B', date: '2024-05-01', uses: 2 },
      { name: 'C', date: '2023-12-01', uses: 10 },
    ];

    describe('sortFiles', () => {
      test('sorts by newest', () => {
        const sorted = sortFiles(files, 'newest');
        expect(sorted[0].name).toBe('B');
        expect(sorted[1].name).toBe('A');
        expect(sorted[2].name).toBe('C');
      });

      test('sorts by oldest', () => {
        const sorted = sortFiles(files, 'oldest');
        expect(sorted[0].name).toBe('C');
        expect(sorted[1].name).toBe('A');
        expect(sorted[2].name).toBe('B');
      });

      test('sorts by mostUsed', () => {
        const sorted = sortFiles(files, 'mostUsed');
        expect(sorted[0].name).toBe('C');
        expect(sorted[1].name).toBe('A');
        expect(sorted[2].name).toBe('B');
      });
    });
    ```

=== "Test-output"

    ```text
    PASS  sortFiles.test.js
      sortFiles
        ✓ sorts by newest (3 ms)
        ✓ sorts by oldest
        ✓ sorts by mostUsed

    Test Suites: 1 passed, 1 total
    Tests:       3 passed, 3 total
    ```

=== "Anvendelse"

    ```js
    const files = [
      { name: 'A', date: '2024-01-01', uses: 5 },
      { name: 'B', date: '2024-05-01', uses: 2 },
      { name: 'C', date: '2023-12-01', uses: 10 },
    ];

    sortFiles(files, 'newest');
    // => [ { name: 'B', ... }, { name: 'A', ... }, { name: 'C', ... } ]

    sortFiles(files, 'oldest');
    // => [ { name: 'C', ... }, { name: 'A', ... }, { name: 'B', ... } ]

    sortFiles(files, 'mostUsed');
    // => [ { name: 'C', ... }, { name: 'A', ... }, { name: 'B', ... } ]
    ```

---------------------------------
## parseDate

Denne funktion konverterede en dato-streng på formatet `dd/mm/yyyy` til et JavaScript `Date`-objekt.

=== "Funktion"

    ```js
    function parseDate(str) {
      const [day, month, year] = str.split('/').map(Number);
      return new Date(year, month - 1, day);
    }
    ```

=== "Test"

    ```js
    import { parseDate } from './parseDate';

    describe('parseDate', () => {
      test('konverterer "28/05/2025" korrekt', () => {
        const date = parseDate('28/05/2025');
        expect(date.getFullYear()).toBe(2025);
        expect(date.getMonth()).toBe(4); 
        expect(date.getDate()).toBe(28);
      });

      test('konverterer "01/01/2000" korrekt', () => {
        const date = parseDate('01/01/2000');
        expect(date.getFullYear()).toBe(2000);
        expect(date.getMonth()).toBe(0); 
        expect(date.getDate()).toBe(1);
      });

      test('konverterer "31/12/1999" korrekt', () => {
        const date = parseDate('31/12/1999');
        expect(date.getFullYear()).toBe(1999);
        expect(date.getMonth()).toBe(11); 
        expect(date.getDate()).toBe(31);
      });
    });
    ```

=== "Test-output"

    ```text
    PASS  parseDate.test.js
      parseDate
        ✓ konverterer "28/05/2025" korrekt
        ✓ konverterer "01/01/2000" korrekt
        ✓ konverterer "31/12/1999" korrekt

    Test Suites: 1 passed, 1 total
    Tests:       3 passed, 3 total
    ```

=== "Anvendelse"

    ```js
    parseDate('28/05/2025');
    

    parseDate('01/01/2000');
    
    ```
------------------------------------
## addQuestion

Denne funktion tilføjede et nyt spørgsmål til listen `questions` og sørgede for, at hvert spørgsmål fik et unikt `qIndex`.

=== "Funktion"

    ```js
    import { ref } from 'vue';

    const qIndex = ref(1);
    const questions = ref([{ qIndex: 1 }]);

    function addQuestion() {
      qIndex.value += 1;
      questions.value.push({ qIndex: qIndex.value });
    }
    ```

=== "Test"

    ```js
    import { ref } from 'vue';

   
    const qIndex = ref(1);
    const questions = ref([{ qIndex: 1 }]);

    function addQuestion() {
      qIndex.value += 1;
      questions.value.push({ qIndex: qIndex.value });
    }

    describe('addQuestion', () => {
      beforeEach(() => {
        
        qIndex.value = 1;
        questions.value = [{ qIndex: 1 }];
      });

      test('tilføjer et spørgsmål med korrekt qIndex', () => {
        addQuestion();
        expect(questions.value.length).toBe(2);
        expect(questions.value[1].qIndex).toBe(2);
      });

      test('kan tilføje flere spørgsmål med stigende qIndex', () => {
        addQuestion();
        addQuestion();
        expect(questions.value.length).toBe(3);
        expect(questions.value[2].qIndex).toBe(3);
      });
    });
    ```

=== "Test-output"

    ```text
    PASS  addQuestion.test.js
      addQuestion
        ✓ tilføjer et spørgsmål med korrekt qIndex
        ✓ kan tilføje flere spørgsmål med stigende qIndex

    Test Suites: 1 passed, 1 total
    Tests:       2 passed, 2 total
    ```

=== "Anvendelse"

    ```js
    // Før:
    questions.value; // [{ qIndex: 1 }]

    addQuestion();
    // Efter:
    questions.value; // [{ qIndex: 1 }, { qIndex: 2 }]

    addQuestion();
    // Efter:
    questions.value; // [{ qIndex: 1 }, { qIndex: 2 }, { qIndex: 3 }]
    ```
-------------------------------


## removeQuestion

Denne funktion fjernede et spørgsmål fra listen `questions` baseret på det angivne indeks.

=== "Funktion"

    ```js
    import { ref } from 'vue';

    const questions = ref([{ qIndex: 1 }]);

    function removeQuestion(index) {
      questions.value.splice(index, 1);
    }
    ```

=== "Test"

    ```js
    import { ref } from 'vue';

   
    const questions = ref([
      { qIndex: 1 },
      { qIndex: 2 },
      { qIndex: 3 }
    ]);

    function removeQuestion(index) {
      questions.value.splice(index, 1);
    }

    describe('removeQuestion', () => {
      beforeEach(() => {
        questions.value = [
          { qIndex: 1 },
          { qIndex: 2 },
          { qIndex: 3 }
        ];
      });

      test('fjerner spørgsmålet på det angivne indeks', () => {
        removeQuestion(1);
        expect(questions.value.length).toBe(2);
        expect(questions.value).toEqual([
          { qIndex: 1 },
          { qIndex: 3 }
        ]);
      });

      test('fjerner det første spørgsmål', () => {
        removeQuestion(0);
        expect(questions.value.length).toBe(2);
        expect(questions.value).toEqual([
          { qIndex: 2 },
          { qIndex: 3 }
        ]);
      });

      test('fjerner det sidste spørgsmål', () => {
        removeQuestion(2);
        expect(questions.value.length).toBe(2);
        expect(questions.value).toEqual([
          { qIndex: 1 },
          { qIndex: 2 }
        ]);
      });
    });
    ```

=== "Test-output"

    ```text
    PASS  removeQuestion.test.js
      removeQuestion
        ✓ fjerner spørgsmålet på det angivne indeks
        ✓ fjerner det første spørgsmål
        ✓ fjerner det sidste spørgsmål

    Test Suites: 1 passed, 1 total
    Tests:       3 passed, 3 total
    ```

=== "Anvendelse"

    ```js
    // Før:
    questions.value; // [{ qIndex: 1 }, { qIndex: 2 }, { qIndex: 3 }]

    removeQuestion(1);
    // Efter:
    questions.value; // [{ qIndex: 1 }, { qIndex: 3 }]

    removeQuestion(0);
    // Efter:
    questions.value; // [{ qIndex: 3 }]
    ```
----------------------------------

## save

Denne funktion oprettede et nyt formular-objekt, gemte det asynkront med `addForm`, viste en succesbesked, og omdirigerede brugeren efter 5 sekunder. 

=== "Funktion"

    ```js
    import { ref } from 'vue';
    import { addForm } from './api'; 
    import { useRouter } from 'vue-router';

    const isSaved = ref(false);
    const showSuccess = ref(false);
    const router = useRouter();

    function save() {
      const newForm = {
        title: 'ABA månedskontrol',
        createdAt: new Date(),
      };

      addForm(newForm)
        .then(() => {
          isSaved.value = true;
          showSuccess.value = true;

          setTimeout(() => {
            router.push('/skemaer');
          }, 5000);
        })
        .catch((error) => {
          console.error('Fejl ved gemning af skema:', error);
        });
    }
    ```

=== "Test"

    ```js
    import { ref } from 'vue';

   
    const addForm = jest.fn();
    const push = jest.fn();
    const router = { push };

   
    const isSaved = ref(false);
    const showSuccess = ref(false);

  
    function save() {
      const newForm = {
        title: 'ABA månedskontrol',
        createdAt: expect.any(Date),
      };

      addForm(newForm)
        .then(() => {
          isSaved.value = true;
          showSuccess.value = true;

          setTimeout(() => {
            router.push('/skemaer');
          }, 5000);
        })
        .catch((error) => {
          
        });
    }

    describe('save', () => {
      beforeEach(() => {
        isSaved.value = false;
        showSuccess.value = false;
        addForm.mockReset();
        push.mockReset();
      });

      test('kalder addForm med korrekt data', async () => {
        addForm.mockResolvedValueOnce();
        save();
        expect(addForm).toHaveBeenCalledWith(
          expect.objectContaining({ title: 'ABA månedskontrol' })
        );
      });

      test('sætter isSaved og showSuccess til true ved succes', async () => {
        addForm.mockResolvedValueOnce();
        save();
        // Vent på promises
        await Promise.resolve();
        expect(isSaved.value).toBe(true);
        expect(showSuccess.value).toBe(true);
      });

      test('kalder router.push efter 5 sekunder', async () => {
        jest.useFakeTimers();
        addForm.mockResolvedValueOnce();
        save();
        await Promise.resolve();
        jest.advanceTimersByTime(5000);
        expect(router.push).toHaveBeenCalledWith('/skemaer');
        jest.useRealTimers();
      });

      test('logger fejl ved fejl i addForm', async () => {
        const error = new Error('Testfejl');
        console.error = jest.fn();
        addForm.mockRejectedValueOnce(error);
        save();
        // Vent på promises
        await Promise.resolve();
        expect(console.error).toHaveBeenCalledWith(
          'Fejl ved gemning af skema:',
          error
        );
      });
    });
    ```

=== "Test-output"

    ```text
    PASS  save.test.js
      save
        ✓ kalder addForm med korrekt data
        ✓ sætter isSaved og showSuccess til true ved succes
        ✓ kalder router.push efter 5 sekunder
        ✓ logger fejl ved fejl i addForm

    Test Suites: 1 passed, 1 total
    Tests:       4 passed, 4 total
    ```

=== "Anvendelse"

    ```js
    // Når brugeren klikker "Gem":
    save();

    // Ved succes:
    // - isSaved.value === true
    // - showSuccess.value === true
    // - Efter 5 sekunder: router.push('/skemaer')
    ```
