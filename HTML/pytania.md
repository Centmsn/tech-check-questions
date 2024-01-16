# HTML - pytania i odpowiedzi z sesji tech-check

## 1. Co to są meta tagi, do czego są wykorzystywane?

Metatagi pełnią kilka funkcji:

- **Odpowiadają za połączenie pomiędzy zewnętrznymi skryptami, arkuszami** itp.
- **Dostarczają informacji na temat samej strony**, które mogę być wykorzystane np. przez przeglądarkę, lub inne strony internetowe i skrypty (przykładem takiego tagu jest `<title>`, który informuje przeglądarkę, jaka powinna być nazwa danej karty, z kolei Facebook korzysta z meta tagów OG - open graph)
- **Poprawiają SEO** (np. `<title>`, `<meta name='description' content='...' />`)

Zazwyczaj umieszcza się je na początku pliku HTML, wewnątrz tagu `<head>`. Zdecydowana większość `meta` tagów nie jest widoczna dla użytkownika strony.

## 2. Czym są atrybuty w HTML?

**Atrybuty to dodatkowe informacje, które mogą zostać dodane do większości tagów HTML**. modyfikują ich zachowanie, lub doprecyzowują ich przeznaczenie (często mają znaczenie jedynie semantyczne, ale nie zawsze). Warto pamiętać, że poszczególne tagi mogą różnić się tym, jakie atrybuty przyjmują.

Przykładowo tag `<img />` może przyjąć src, alt i wiele innych (`<img src="image.jpg" alt="Description of the image">`), ale tab `<p>` nie posiada atrybutu `src`.

## 3. Za co odpowiadają atrybuty ARIA?

**ARIA** to skrót od **A**ccessible **R**ich **I**nternet **A**pplication, co w wolnym tłumaczeniu oznacza aplikację internetową, dostępną dla wszystkich.

Mówiąc wszystkich, mam tu na myśli szczególnie osoby, które mogą mieć problemy z obsługą strony / aplikacji w standardowy sposób. Przykładem mogą być **osoby niedowidzące, niewidome, sparaliżowane itd.. Tacy użytkownicy wymagają dodatkowych informacji w tagach HTML** (oraz poprawnie zbudowanej, semantycznej struktury tagów), **które precyzują ich przeznaczenie i zastosowanie. Za to właśnie odpowiadają tagi z grupy ARIA.**

Przykładem może być przycisk, który ma tylko ikonę kosza, bez żadnego tekstu. Dla użytkownika, który widzi, jego zastosowanie jest oczywiste - usuwa on jakiś element. Jeżeli jednak nie możemy zobaczyć ikony, to w efekcie mamy pusty przycisk. Sprawia to, że użytkownik korzystający z czytnika ekranowego nie wie, do czego może go wykorzystać.

Rozwiązaniem jest dodanie atrybutu `aria-label` i opisanie, do czego służy dany przycisk: `<button aria-label="Delete">`. Atrybutów ARIA jest [znacznie więcej](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA), ale nie polecam uczyć się ich na pamięć.

## 4. Wyjaśnij zastosowanie tagu `<picture>`

`<picture>` **służy do wyświetlenia responsywnych obrazów. Umożliwia programiście podanie kilku źródeł** (różne wymiary) obrazka. Następnie przeglądarka sama decyduje, który powinna wybrać, w zależności od rozdzielczości urządzenia, rozmiaru viewportu, itp.

Stosowanie tego tagu może znacznie poprawić czas wczytywania grafik i tym samym pozytywnie wpłynąć na UX (_user experience_).

Przykładowe zastosowanie:

```
<picture>
  <source srcset="image-large.jpg" media="(min-width: 1200px)">
  <source srcset="image-medium.jpg" media="(min-width: 600px)">
  <img src="image-small.jpg" alt="Description of the image">
</picture>
```

## 5. Wyjaśnij różnicę pomiędzy atrybutem defer i async w tagu script

**`defer`** - oznacza, że **skrypt zostanie wykonany dopiero w momencie, gdy cały HTML zostanie w pełni sparsowany** (a więc po zdarzeniu `DOMContentLoaded`). Podobnie jak `async`, jest to operacja asynchroniczna i wczytywanie skryptu może rozpocząć się zanim HTML zostanie załadowany, jednak nie zostanie on wykonany. Dodatkowo, jeżeli w strukturze HTML występuje kilka tagów `<script>` z rzędu i wszystkie z nich mają atrybut `defer`, to mamy gwarancję, że zostaną wykonane w kolejności, w jakiej występują w pliku HTML.

`<script defer src="script1.js"></script>`

---

**`async`** - oznacza, że skrypt powinien być wczytywany asynchronicznie, a następnie uruchomiony tak szybko, jak to możliwe i nie czekać na pełne sparsowanie pliku HTML. Kolejność wykonywania skryptów może się różnić od tej z pliku HTML, w zależności od tego, który z nich wczyta się jako pierwszy.

`<script async src="script1.js"></script>`

**Podsumowując**: jeżeli skrypt ingeruje w HTML lub kolejność wczytywania jest ważna, to powinniśmy użyć defer. Async zastosuj, gdy chcesz wczytać skrypty tak szybko, jak to możliwe, nie czekając na HTML (pamiętaj, że kolejność wczytywania jest właściwie losowa).

## 6. Czy na jednej stronie może występować więcej niż jeden tag `<h1>`?

Tak, może. [Nie ma to negatywnego wpływu na SEO](https://www.stanventures.com/blog/multiple-h1-tags/), jednak może mieć negatywny wpływ na semantykę, jeżeli takie podejście zostanie zastosowane nieumiejętnie. Istnieją dwa obozy - jeden twierdzi, że może być tylko jeden tag `<h1>` (na stronie), natomiast drugi uważa, że nie ma żadnych przeciwwskazań żeby było ich więcej.

**Podsumowując**: technicznie nie jest to zabronione, bezpieczniej jest jednak trzymać się wersji, w której tag `<h1>` jest tylko jeden na stronie.

## 7. Co oznacza pojęcie “semantyczny HTML”?

W praktyce oznacza **to stosowanie odpowiednich tagów, w odpowiednim miejscu**. Pod tym stwierdzeniem kryje się nieco szerszy temat, ale poprawne stosowanie tagów wpływa pozytywnie zarówno na SEO, jak i na dostępność strony. Pomaga także innym developerom zrozumieć jej strukturę.

Przykład prostej, poprawnej pod względem semantyki strony:

```
<!-- Archaiczny tag, nadal stosowany, ale nie jest wymagany -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simplest Semantic Page</title>
</head>

<body>
    <header>
        <h1>Hello, World!</h1>
    </header>

    <main>
        <p>This is a very simple webpage.</p>
    </main>

    <footer>
        <p>&copy; 2024 Simple Page. All rights reserved.</p>
    </footer>
</body>
</html>
```

Stosujemy odpowiednie, pod względem semantyki tagi (np. `<main>`, `<header>`, `<footer>`) zamiast wstawiać wszędzie `<div>` i `<span>`. **Jest to zdecydowanie najlepsza praktyka**. Dodatkowo można tu wspomnieć o atrybutach **ARIA**.

## 8. Co to jest favicon? Jak go dodać?

**Favicon to ikona, która reprezentuje naszą stronę lub aplikację**. Wyświetlany jest w kilku miejscach, np. w zakładkach, w pasku wyszukiwania, na karcie, itd.

Favicon jest niezwykle istotny, ponieważ pozwala użytkownikom rozpoznać witrynę bez sprawdzania jej adresu. Buduje świadomość marki.

Zazwyczaj umieszcza się go wewnątrz tagu `<head>`. Atrybut type zależy od formatu, w jakim została stworzona dana ikona:

`<link rel="icon" href="favicon.ico" type="image/x-icon">`

## 9. Czy kolejność, w jakiej wczytamy zewnętrzne zależności ma znaczenie?

Tak, zdecydowanie ma. W większości przypadków preferowanym podejściem jest wczytanie CSS na samym początku, a dopiero później resztę skryptów.

**Dlaczego? **

- CSS odpowiada za stylowanie i układ, **a wczytanie go jako pierwszego pozwala przeglądarce zacząć renderowanie strony z odpowiednimi stylami**. To z kolei pomaga uniknąć problemów z wyglądem i zapewnia lepszy UX.
- **Wczytywanie CSS na początku dokumentu pozwala przeglądarce pobierać i stosować style równocześnie z pobieraniem innych zasobów**. To może przyczynić się do szybszego odczuwanego czasu ładowania strony.
- Jeśli JavaScript manipuluje DOM-em lub stosuje style dynamicznie, wczytanie CSS jako pierwszego pomaga uniknąć FOUC (_Flash of Unstyled Content_), gdzie strona krótko pojawia się bez stylizacji, zanim zostanie ostylowana przez JS.
- Jeśli kod JavaScript polega na stylach, wczytanie CSS jako pierwszego zapewnia, poprawne działanie strony.

**Podsumowując:** wczytując CSS jako pierwszy strona załaduje się szybciej, UX będzie lepszy, a dodatkowo unikniesz potencjalnych błędów.

## 10. Radio vs checkbox. Co je różni?

Zarówno radio, jak i checkbox to rodzaje inputa. Różnią się jednak przeznaczeniem i zastosowaniem.

Radio (`<input type="radio">`):

- Radio buttony są używane, gdy chcesz, aby użytkownicy dokonali pojedynczego wyboru spośród grupy opcji.
- Wszystkie radio buttony w obrębie grupy mają taki sam atrybut name, tworząc grupę wzajemnie wykluczających się opcji. Oznacza to, że gdy jeden radio button jest wybrany, inne w tej samej grupie są automatycznie odznaczone.

```
<input type="radio" name="gender" value="male">
<input type="radio" name="gender" value="female">
```

Checkbox (`<input type="checkbox">`):

- Checkboxy pozwalają użytkownikom na dokonywanie wielokrotnych wyborów lub nie wybieranie niczego.
- Każdy checkbox jest niezależny, a użytkownicy mogą go zaznaczać/odznaczać indywidualnie. Nie mają one wzajemnie wykluczającego się zachowania, które jest charakterystyczne dla radio buttonów.

```
<input type="checkbox" name="fruit" value="apple">
<input type="checkbox" name="fruit" value="banana">
<input type="checkbox" name="fruit" value="orange">
```

**Podsumowując:**

- Użyj radio buttonów, gdy chcesz, aby użytkownicy wybrali dokładnie jedną opcję spośród grupy.
- Użyj checkboxów, gdy chcesz, aby użytkownicy dokonywali wielokrotnych wyborów lub w ogóle nic nie zaznaczali.

Zarówno radio buttony, jak i checkboxy są istotne do tworzenia przyjaznych dla użytkownika formularzy, a wybór między nimi zależy od konkretnych wymagań formularza i rodzaju danych, jakie chcesz zbierać.

## 11. Wyjaśnij atrybuty noreferrer oraz noopener

Zarówno `rel='noreferrer'`, jak i `rel='noopener'` to atrybuty, które powinny zostać dodanego do tagu `<a>`, jeżeli jest na nim obecny atrybut `target='_blank'`.

- **noopener** - gdy link otwiera nową kartę lub okno przeglądarki, to ma ona częściowy dostęp do strony, która ją otworzyła (wykorzystując JavaScript). Może to stanowić zagrożenie, jeżeli otworzona strona nie jest w pełni zaufana. Atrybut `noopener` **chroni między innymi przed atakami phishingowymi, ponieważ nie pozwala nowo otwartej stronie na dostęp do strony, która ją otworzyła** (właściwość `window.opener` jest pusta)
- **noreferrer** - ten atrybut również wpływa na informacje, które przeglądarka udostępnia nowo otworzonej stronie. Zazwyczaj zawiera url strony otwierającej. **Zastosowanie tego atrybutu pozytywnie wpływa na prywatność i bezpieczeństwo użytkownika** - otworzona strona nie wie, skąd przyszedł użytkownik.
