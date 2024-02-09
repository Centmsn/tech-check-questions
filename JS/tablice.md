## Jakie są różnice między tablicami w JavaScript a innymi strukturami danych, takimi jak obiekty?
Tablice w JavaScript są uporządkowanymi kolekcjami elementów, do których można odwoływać się za pomocą indeksów liczbowych, podczas gdy obiekty są kolekcjami 
nieuporządkowanych par klucz-wartość. Warto pamiętać, że pod "spodem" tablice to nadal obiekty, a JavaScript nie posiada osobnego typu, dedykowanego dla tablic.

```javascript
const arr = [];

typeof(arr) // "object"
```

## W jaki sposób możemy sprawdzić, czy zmienna zawiera tablicę?
Najprostszym sposobem jest użycie metody `Array.isArray(zmienna)` i przekazanie do niej sprawdzanej zmiennej. Pamiętaj, że sprawdzenie za pomocą `typeof` zwróci w przypadku tablicy
`object`, więc jest to niewystarczające.

## Jakie są różnice między metodami `push()` i `unshift()` w kontekście tablic w JavaScript?
Metoda `push()` dodaje nowy element na koniec tablicy, zwiększając jej długość, natomiast metoda `unshift()` 
dodaje nowy element na początek tablicy, przesuwając istniejące elementy. Z tego powoda **metoda** `unshift` **jest znacznie mniej wydajna od** `push` (w tym przypadku nie musimy nic przesuwać, 
po prostu dodajemy nowy element na koniec tablicy). 

## Jak można usunąć element z tablicy w JavaScript?
Można to zrobić za pomocą metody `splice()`, która usuwa elementy z tablicy w danym zakresie indeksów.

```javascript
let arr = [1, 2, 3, 4, 5];

arr.splice(2, 1); // Usuwa jeden element z indeksem 2
```

## W jaki sposób można skopiować tablicę w JavaScript?

Istnieje wiele sposobów na utworzenie kopii tablicy.
- Zastosowanie operatora spread `...`:
```javascript
const arr = [1, 2, 3];

const arrCopy = [...arr];
```
- Metoda `slice`:
```javascript
const arr = [1, 2, 3];

const arrCopy = arr.slice();
```
- Z użyciem metody `from`:
```javascript
const arr = [1, 2, 3];

const arrCopy = Array.from(arr);
```

Warto pamiętać, że powyższe sposoby tworzą płytką kopię tablicy `arr`.

## Czym różnią się metody destrukcyjne od niedestrukcyjnych?
Metody destrukcyjne, takie jak `splice`, `sort`, `reverse` oraz `fill` (nie jest to pełna lista) **modyfikując tablicę na której zostaną użyte**. 
Z kolei metody niedestrukcyjne (ty przykładami mogą być: `slice`, `concat`, `includes`, `every`) **nie zmieniają zawartości oryginalnej tablicy**, a zamiast tego zwracają
nową wartość (najczęściej kopię tablicy, chociaż nie zawsze).

## Czy tablice można destrukturyzować?
**Tak**. Istnieje jednak kilka różnić między destrukturyzacją tablic, a destrukturyzacją obiektów:

- zmienne mogą być nazwane dowolnie (w obiekcie muszą odpowiadać nazwom kluczy), a ich kolejność ma znaczenie. W przypadku tablic, **stosujemy nawiasy
  kawdratowe, zamiast klamrowych**:
```javascript
const arr = [1, 2, 3];

const [element1, element2, element3] = arr;
element1 // 1
element2 // 2
element3 // 3
```
- można pomijać element tablicy z wykorzystaniem `,` - w obiekcie wystarczy nie przypisywać danego klucza do zmiennej, nie ma potrzeby pomijania, ponieważ kolejność nie ma tam znaczenia:
```javascript
const arr = [1, 2, 3];

const [,, element3] = arr; // dwa pierwsze elementy zostają pominięte
element3 // 3
```

## Wyjaśnij metodę `reduce`
Metoda `reduce` zazwyczaj stosowana do przekształcenia tablicy w inną wartość. Przykładem może być sytuacja, gdy chcemy zsumować wszystkie elementy tablicy, zawierającej liczby (tablica
zostaje przekształcona na `number`).

`reduce` różni się nieco od innych metod tablicowych ponieważ przyjmuje dwa argumenty: callback (który otrzymuje 4 argumenty - tak, jak w innych
metodach tablicowych) oraz wartość początkową (domyślnie jest to `0`).

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
}, 0);

sum // 15
```

W tym przykładzie wartość początkowa to `0`. `accumulator` początkowo jest równy wartości początkowej, a więc w pierwszej iteracji `accumulator === 0`, z kolei w parametrze
`currentValue` otrzymujemy po kolei każdy element tablicy. Istotne jest również wartość, która zostanie zwrócona przez podany do `reduce` callback, ponieważ to ona zostanie 
przypisana do `accumulator`. 

Można to rozpisać tak:
![reduce](https://github.com/Centmsn/tech-check-questions/assets/65851661/44a74132-9e8f-4d08-b37f-398218540700)

Z użyciem `reduce` możemy osiągnać dowolny rezultat i otrzymać dowolny typ w wyniku jego działania - jest to najbardziej uniwersalna metoda ze wszystkich dostępnych metod tablicowych. 
Warto zaznaczyć, że nie powinniśmy jej nadużywać. Jeżeli jakąś operację można przeprowadzić za pomocą np. `map` lub `filter`, to lepiej jest użyć dedykowanej metody.

## Wyjaśnij metodę sort
Metoda sort służy do sortowania elementów w tablicy, jest to metoda destrukcyjna (zmienia oryginalną tablicę). Przyjmuje jeden argument - funkcję, która następnie otrzyma dwa argumenty:
elementA oraz elementB. W ich miejsca będą po kolei podstawiane wszystkie elementy tablicy.

Wynikiem działania tej funkcji powinna być liczba. W zależności od tego, co zwrócimy elementy zostaną posortowane w odpowiedni sposób:

- **jeżeli funkcja zwróci wartość > 0**: oznacza to, że `elementA` powinien zostać umieszczony **po** `elementB`
- **jeżeli funkcja zwróci wartość < 0**: oznacza to, że `elementA` powinien zostać umieszczony **przed** `elementB`
- **jeżeli funkcja zwróci wartość == 0**: oznacza to, że elementy `elementA` i `elementB` zostaną w obecnym miejscu

W najprostszym przypadku jej użycie wygląda tak:
```javascript
const numbers = [3, 1, 4, 2, 5];

numbers.sort((a, b) => a - b);

numbers // [1, 2, 3, 4, 5]
```

Zwróć uwagę, że w przypadku sortowania stringów lepiej jest zastosować metodę `localCompare`
```javascript
const strings = ['Apple', 'banana', 'Orange'];

strings.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
```

## Opisz metodę every or some
Metoda `every` zwraca wartość `true` jeżeli dla wszystkich elementów w tablicy, przekazany callback zwróci `true`. Jeżeli chociaż jeden element nie spełni podanego warunku, to cała
metoda zwraca również `false`.
```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.every((element) => element > 0); // true - każdy element jest większy od 0
numbers.every((element) => element > 2); // false - jeden z elementów jest mniejszy od 2
```

Metoda `some` zwraca wartość `true` jeżeli dla przynajmniej jednego elementu w tablicy, przekazany callback zwróci `true`. Gdy żaden element nie spełni podanego warunku, to cała
metoda zwraca również `false`.
```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.some((element) => element > 4); // true - jeden element jest większy od 4
numbers.some((element) => element > 5); // false - żaden z elementów nie jest większy od 5
```

## Czym różni się metoda forEach od map?
`forEach` jest alternatywą dla pętli, a wartośc zwrócona przez przekazaną do środka funkcję nie ma znaczenia - nie wpływa na elementy tablicy. Warto pamiętać, że metoda `forEach` zawsze zwraca `undefined`, a więc nie ma sensu przypisywać jej wywołania do zmiennej.

```javascript
const numbers = [1, 2, 3, 4, 5];
const result = numbers.forEach((element) => element * 2);

result // undefined, oryginalna tablica również pozostała niezmieniona
```

Metoda `map` również iteruje po tablicy, jednak w jej przypadku, wartość zwracana przez callback ma duże znaczenie - `map` służy do transformacji / modyfikacji elementów tablicy. Jest niedestrukcyjny i zwraca nową tablicę.
```javascript
const numbers = [1, 2, 3, 4, 5];
const result = numbers.map((element) => element * 2);

result // [2, 4, 6, 8, 10]
```
