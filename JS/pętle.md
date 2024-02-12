## Czym różnią się od siebie pętle `for...of` oraz `for...in`
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
