## Czym różnią się od siebie pętlę `for...of` oraz `for...in`
<details>
<summary>Odpowiedź</summary>
    
Pętla `for...of` powinna być stosowana do iterowalnych obiektów, takich jak `string`, `array`, `map`, itd.

```javascript
const arr = ["a", "b", "c"];

for (const value of arr) {
    console.log(value); // "a", "b", "c"
}

// Jeżeli zastosujemy pętlę for...in zamiast for...of, to uzyskamy taki wynik
for (let index in arr) {
    console.log(index); // "0", "1", "2" - klucze (tablica to tak naprawdę obiekt w którym indexy to klucze)
    console.log(arr[index]); // "a", "b", "c" - elementy tablicy
}
```

Pętla `for...in` służy do iterowania po właściwościach obiektu i do tego powinna być stosowana. Unikaj wykorzystania tej pętli do iteracji po tablicach, stringach, itd. - wyświetli
ona wszystkie wartości, oznaczone jako `enumerable`, co w praktyce oznacza, że mogą się tam znaleźć metody lub właściwości pochodzące z prototypu.
```javascript
const obj = { a: 1, b: 2, c: 3 };

for (let prop in obj) {
    console.log(prop); // 'a', 'b', 'c'
    console.log(obj[prop]); // 1, 2, 3
}
```
</details>

## Wytłumacz działanie pętli `for`
<details>
  <summary>Odpowiedź</summary>

  Pętla `for` jest najbardziej uniwersalną, a zarazem jedną z najszybszych pętli w JavaScript. składa się z trzech głównych części:
  - wartość początkowa / initialization
  - warunek / condition
  - krok / step
  
  ```javascript
    for (initialization; condition; step) {
        // kod
    }

    for (let i = 1; i <= 5; i++) {
        console.log(i);
    }
 ```

**Każda z trzech części jest opcjonalna i może zostać pominięta**. Wtedy trzeba w jej miejsce zastosować po prostu `;`. Jeżeli pominiemy wszystkie opisanej składowe, to uzyskamy
pętlę nieskończoną (ten sam efekt, co przy `while(true)`).

```javascript
for (;;) {
    console.log("Infinite loop");
}
```
</details>

## Porównaj pętlę `while` oraz `do...while`
<details>
  <summary>Odpowiedź</summary>

  Zarówno pętla `while`, jak i `do...while` służą do ponownego wykonywania bloku kodu, dopóki dany warunek pozostaje prawdziwy (truthy). Jedyna różnica pomiędzy tymi pętlami
  to moment w którym sprawdzany jest warunek.

  **W przypadku pętli `while` najpierw sprawdzany jest warunek. Jeżeli jest prawdziwy, to kod w pętli zostanie wykonany. W innym przypadku kod nie zostanie uruchomiony.**
  ```javascript
  // Poniższa pętla wykona się 5 razy (0, 1, 2, 3, 4)
  let i = 0;

  while (i < 5) {
      console.log(i)
      i++
  }

  // Poniższa pętla nie wykona się ani razu
  let j = 5;

  while(j < 5) {
      console.log(j)
  }
  ```

 **Dla pętli `do...while` sytuacja wygląda nieco inaczej - najpierw wykonywany jest blok pętli, a dopiero później sprawdzany jest warunek**. 
 Oznacza to, że ta pętla wykona się co najmniej raz, nawet jeśli warunek jest nieprawdziwy, ponieważ zostanie on sprawdzony dopiero po pierwszej iteracji.

  ```javascript
  // Poniższa pętla wykona się 5 razy (0, 1, 2, 3, 4)
  let i = 0;

  do {
      console.log(i)
      i++
  } while (i < 5)

  // Poniższa pętla nie wykona się raz
  let j = 5;

  do {
      console.log(j)
  } while (j < 5)
  ```

</details>
