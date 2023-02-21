## Odpowiedzi na pytania do kodu, które się pojawiły

### JSON.stringify

```js
const newPre = document.createElement("pre");
newPre.className = "column half-column element";
newPre.innerText = JSON.stringify(object, null, 2);
```

Znacznik `<pre>` umożliwia wyświetlenie na stronie uprzednio sformatowanego tekstu - 
HTML zwykle ignoruje nasze spacje, tabulatory i wcięcia.

`JSON.stringify` umożliwia nam z kolei wstępne sformatowanie wyświetlanego tekstu.

JSON - to format wymiany danych, jeszcze będziemy o nim mówić.
W tym wypadku, żeby ładnie wyświetlić obiekt na stronie, konwertujemy 
nasz obiekt javascriptowy (`object`) na JSONa (JSON wyświetla się na stronie w sekcji "Baza danych").

Testowo można wykonać sobie w konsoli przeglądarki metody konwertujące i zobaczyć, co zwracają:

- obiekt JS -> JSON:
```js
JSON.stringify({name: "Waldek", age: 13})
```

- JSON -> obiekt JS
```js
JSON.parse('{"name": "Waldek", "age": 13}')
```

Metoda `JSON.stringify` może przyjmować więcej argumentów, w przykładowym kodzie:

- drugi argument (w przykładowym kodzie - `null`) - pozwala na wyfiltrowanie niektórych pól z obiektu, gdyby np. interesował nas tylko wiek Waldka:
```js
JSON.stringify({name: "Waldek", age: 13}, ["age"])
``` 

- trzeci argument (w przykładowym kodzie - `2`) - określa wielkość wcięć, jakie są dodane przy formatowaniu JSONa.
Można poeksperymentować - zmienić tam liczbę np. na 10 i spróbować dodać obiekt do bazy - wcięcia w wyświetlanych
JSONach będą większe. 


### FormData

```js
const form = document.getElementById("element-form");
const data = new FormData(form);

const object = {};
for (let el of data.entries()) {
    object[el[0]] = el[1];
}

return object;
```

Ten fragment umożliwia nam wyciągnięcie danych wpisanych do formularza i przerobienie ich na obiekt javascriptowy
(który potem konwertujemy na JSON, metodą `JSON.stringify`).

- najpierw wyszukujemy na stronie formularz - `const form = document.getElementById("element-form");`
- następnie na podstawie formularza tworzymy obiekt `FormData`
- obiekt `FormData` posiada metodę `entries`, która umożliwia iterację po polach formularza
- w pętli tworzymy obiekt - "kluczami" w tym obiekcie są nazwy pól formularza, a "wartościami" zawartości tych pól


### Parametr event

```js
document.addEventListener("DOMContentLoaded", function(event) {
    document.getElementById("test").onmouseenter = test;
});

function test(event) {
    event.target.innerText = "TAK";
}
```

Jest domyślny parametr, który JS zawsze dorzuca jako pierwszy argument funkcji 
wykonującej się po zajściu jakiegoś zdarzenia. 
Jest to obiekt, który reprezentuje właśnie to zdarzenie - 
w przykładzie wywołujemy `event.target` - target jest to element na stronie, 
na którym zdarzenie się odbyło, np. po kliknięciu w znacznik `<button>`
eventem będzie kliknięcie, a przez event.target będziemy mogli się dostać 
do obiektu reprezentującego `<button>`. Ten kod można sobie przetestować:

- przepisać do pliku np. `test.js`
- stworzyć sobie jakiś plik, np. `test.html`, do którego załączymy ten `test.js` 
(na tej stronie powinien się znaleźć jakiś obiekt o id test, np. `<button id='test'>TEST</button>`) i włączyć stronę w przeglądarce
- w narzędziach developerskich odnaleźć plik `test.js` (w Chrome można to zrobić w zakładce "Sources") i ustawić breakpoint wewnątrz funkcji `test`
- po najechaniu myszką na guzik o id `test` powinniśmy się zatrzymać na tym breakpoincie - wówczas w konsoli można wpisać sobie "event" i popatrzeć, jakie tam są informacje
	 
### Co to jest Node

Node to inaczej węzeł w dokumencie HTML - w zasadzie inna nazwa na tag czy element na stronie; węzłem może być div, button itd.