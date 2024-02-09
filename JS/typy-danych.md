## Jakie typy danych istnieją w JavaScript?
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

## Opisz kiedy stosować bigInt i jak utworzyć taką liczbę
`bigInt` powinien być stosowany tylko wtedy, gdy mamy do czynienia z liczbą większą niż 2<sup>53</sup> - 1. Wymaga większej liczby bitów do przechowywania w pamięci, więc jest mniej wydajny niż typ `number`

**Sposoby na utowrzenie są dwa**
- `BigInt(4789579843547395)` (zauważ, że nie ma tu słowa kluczowego `new`)
- `745235698437578934759834n` (litera `n` na końcu)

Ważne jest również to, że wartości utworzone w ten sposób nie będą równe (chyba, że użyjemy `==` zamiast `===`) liczbom stworzonym bez użycia wymienionych wyżej sposobów:
```javascript
100n == 100 // true
100n === 100 // false
```
