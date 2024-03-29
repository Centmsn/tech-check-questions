## Jakie typy danych istnieją w JavaScript?
<details>
  <summary>Odpowiedź</summary>
  
  Jest ich 8, jednak najczęściej wykorzystuje się 6:
- `string`
- `number`
- `boolean`
- `object` (JS nie rozróżnia specjalnego typu dla tablic, ani funkcji. Co prawda użycie operatora `typeof` może wyświetlić `"function"`, jednak operator ten nie zwraca zawsze typów zgodnych ze specyfikacją)
- `null`
- `undefined`

Pozostałe dwa to:
- `symbol`
- `bigInt` (używane do tworzenia naprawdę dużych liczb)
</details>

## Opisz kiedy stosować bigInt i jak utworzyć taką liczbę
<details>
  <summary>Odpowiedź</summary>
  
`bigInt` powinien być stosowany tylko wtedy, gdy mamy do czynienia z liczbą większą niż 2<sup>53</sup> - 1. Wymaga większej liczby bitów do przechowywania w pamięci, więc jest mniej wydajny niż typ `number`

**Sposoby na utowrzenie są dwa**
- `BigInt(4789579843547395)` (zauważ, że nie ma tu słowa kluczowego `new`)
- `745235698437578934759834n` (litera `n` na końcu)

Ważne jest również to, że wartości utworzone w ten sposób nie będą równe (chyba, że użyjemy `==` zamiast `===`) liczbom stworzonym bez użycia wymienionych wyżej sposobów:
```javascript
100n == 100 // true
100n === 100 // false
```
</details>

## Wytłumacz różnicę pomiędzy operatorem == a ===
<details>
  <summary>Odpowiedź</summary>
  
  Operator `==` potocznie nazywany płytkim porównaniem dokonuje niejawnej konwersji typów (ang. _type coercion_). Oznacza to, że:
  ```javascript
  2 == "2" // true - udało się zamienić typ number na typ string, więc porównanie wyglądało tak: "2" == "2"
  false == 0 // true - udało się zamienić false, na typ number, a porównanie wyglądało tak 0 == 0
  null == undefined // true
  [] == "" // true
  
  2 == 2 // true
  [] == [] // false - typ referencyjny, porównywana jest lokalizacja w pamięci, a nie wartości w środku
  ```

Operator `===`, czyli głębokie porównanie, działa nieco inaczej. Nie dopuszcza on do niejawnej konwersji typów, więc wynik jego działania będzie zupełnie inny:
```javascript
2 === "2" // false - typ string nigdy nie będzie równy typowi number, jeżeli zastosujemy ===
false === 0 // false - typ boolean nie jest równy typowi number
null === undefined // false - null i undefined to inne typy
[] === "" // false - pusta tablica nie jest pustym stringiem

2 === 2 // true
[] === [] // false - typ referencyjny, porównywana jest lokalizacja w pamięci, a nie wartości w środku
```

Zazwyczaj zaleca się używanie `===` ponieważ jego wyniki są bardziej przewidywalne, a jendocześnie ograniczamy możliwość popełnienia błędu związanego z niejawną zmianą typu.
</details>

## Wyjaśnij czym jest `symbol` i kiedy go stosować
<details>
  <summary>Odpowiedź</summary>

`symbol` pisany małą literą to typ prymitywny. Podobnie, jak `string`, posiada on swój odpowiednik pisany wielką literą - `Symbol` (w tym przypadku mamy do czynienia z obiektem). **Symbol jest zawsze unikatową wartością i nie da się utworzyć dwóch identycznych symboli**. Z tego właśnie wynika jego główna zaleta i zastosowanie. **Najczęściej wykorzystywany jest w obiektach, jako klucz**.

JavaScript posiada także kilka wbudowanych w język symboli, za pomocą których możemy modyfikować zachowanie niektórych elementów język. Więcej na temat symboli znajdziesz [tutaj](https://www.4spacje.pl/article/symbole-w-javascript)
</details> 
