# `<NAZWA PROJEKTU>` — Specyfikacja

> **[Szablon STC — usuń ten callout przed użyciem.]** **Pierwszy** dokument projektu i jedyny, który właściciel pisze sam. Powstaje przed `Logic.md` i jest celowo nietechniczny: czego chcesz i jak sobie wyobrażasz, że to działa — nie jak zostanie zbudowane. Angielski bliźniak leży obok jako `Specification Template.md`; wybierz jeden język i w nim pisz treść. Układ jest identyczny. Wypełniony plik projektu zawsze nazywa się `Specification.md`, niezależnie od języka, w którym go napisałeś.

**To piszesz Ty. Nie agent.** Asystent może zadawać pytania, wskazywać, gdzie dwa Twoje zdania się nie zgadzają, mówić, gdy czegoś brakuje, ostrzegać, gdy §5 rozjechał się z §2, i przenieść linię do sekcji, do której faktycznie należy. Nie wolno mu tu niczego projektować, proponować architektury ani wypełniać tego za Ciebie.

**Pisz treścią w języku, w którym myślisz.** Zwykłe zdania są lepsze niż techniczne. Jeśli sięgasz po słowo, które musiałbyś sprawdzić, prawdopodobnie opisujesz *jak*, a nie *co*.

**Jedna granica, która utrzymuje ten dokument w użyteczności:** żadnych nazw plików, funkcji, flag konfiguracyjnych, bibliotek ani silników — nigdzie poza **§6.3**. Test jest prosty — *czy ktoś przeczytałby to bez otwierania repozytorium?* Jeśli nie, wszedłeś na teren `Logic.md`, i agent powinien Cię odesłać.

**Co się z tym plikiem dzieje.** Piszesz pierwszą wersję, potem przerabiasz ją w rozmowie tyle rund, ile trzeba. Gdy **Ty** uznasz, że opisuje to, czego naprawdę chcesz, praca przechodzi do `Logic.md`, gdzie zapadają wszystkie decyzje techniczne. **Od tego dnia ten plik jest zamrożony, przeniesiony do `ARCH/` i nigdy więcej nie służy do budowania.** Jego jedyna pozostała rola to odpowiedź na *"jak bardzo to odeszło od tego, o co pierwotnie prosiłem?"* — a odpowie na to tylko wtedy, gdy nikt go potem nie „porządkował”.

---

## 1. Jednym akapitem — czym to jest?

`<Opisz to tak, jak koledze, który ma dziewięćdziesiąt sekund. Jeśli nie mieści się w jednym akapicie, lepiej wiedzieć to teraz niż po tym, jak ktoś to zbuduje.>`

## 2. Założenie — co chcę osiągnąć i w jakim kierunku

`<To jest punkt odniesienia całego dokumentu. Nie lista funkcji: zamysł. Po co to jest, jak ma się czuć, gdy już to masz, jaka jest ogólna idea, która spina wszystkie części. Potem garść zasad, które obowiązują wszędzie — „ma zawsze odpowiadać szybko”, „ma działać bez internetu”, „ma pamiętać, o czym już rozmawialiśmy”, „nigdy nie ma wymagać, żebym siedział przy biurku”.>`

> **§4 i §5 sprawdza się wobec tej sekcji, i właśnie po to tu jest.** Jeśli czegoś z listy funkcji nie da się wywieść z założenia, prawdziwe jest jedno z dwojga: założenie jest niepełne, albo ta pozycja nie należy do tego projektu. **To najwcześniejsze miejsce, w którym widać, że projekt idzie w złą stronę**, i nic to tu nie kosztuje — ten sam rozjazd po napisaniu `Logic.md` kosztuje Mod bump, a po powstaniu kodu przebudowę. Agent, który to zauważy, ma powiedzieć to na głos; nie wolno mu cicho tego obchodzić.

## 3. Pierwszy szkic struktury

`<Ta sekcja nie jest opcjonalna. Narysuj kawałki, które sobie wyobrażasz, w formie poniżej — ta forma jest tu po to: późniejsze przebiegi w §4 wiszą na tych nazwach, a Logic.md §2.1 czyta ten szkic jako wejście. Zagnieżdżone drzewo z jednym zdaniem odpowiedzialności w każdej linii to sposób, w jaki struktura jest wprowadzana w tym dokumencie. Zamień przykładowe nazwy na swoje; kształt zostaw.>`

```text
<katalog główny>
├─ <grupa plików kodu realizujących zadania z tego samego obszaru>  — <jednozdaniowy opis tego, za co odpowiada ta grupa>
│   ├─ <komponent 1>                                               — <jednozdaniowy opis tego, za co odpowiada ten plik>
│   └─ <komponent 2>                                               — <jednozdaniowy opis tego, za co odpowiada ten plik>
├─ <grupa plików kodu realizujących zadania z innego obszaru>      — <jednozdaniowy opis tego, za co odpowiada ta grupa>
│   ├─ <komponent 3>                                               — <jednozdaniowy opis tego, za co odpowiada ten plik>
│   └─ <komponent 4>                                               — <jednozdaniowy opis tego, za co odpowiada ten plik>
├─ <część odpowiedzialna za pozostałe zadania>                     — <jednozdaniowy opis tego, za co odpowiada ta grupa>
│   ├─ <…>
│   └─ <…>
└─ <elementy, które istnieją, ale na razie są puste>               — nazwane, aby nikt później nie tworzył ich ponownie; ich wyjaśnienie znajduje się w §6.2
```

> **Nic tutaj nie jest decyzją.** To Twoja pierwsza mapa, i `Logic.md` może ją wymienić w całości — inny podział, inne nazwy, inna liczba kawałków — i to nie jest porażka żadnego z dokumentów. Każdą linię pisz jako *odpowiedzialność* („część, która rozmawia z ludźmi”, „część, która pamięta”), a nie jako nazwę pliku, a jeśli już wiesz, że coś musi być osobnym kawałkiem z jakiegoś powodu — napisz ten powód w tej linii. Zagnieżdżanie jest dozwolone i oczekiwane: część, która zawiera części, to sposób, w jaki pokazujesz, gdzie coś mieszka. Części, które narysujesz, ale świadomie jeszcze nie chcesz, zostają na drzewie *i* należą do §6.2.

## 4. Jak to ma działać

`<Serce dokumentu i miejsce, w którym możesz być tak szczegółowy, jak chcesz. Grupuj tak, jak naprawdę myślisz — po częściach („kawałek od wiadomości”, „kawałek, który pamięta”) albo po ficzerach. Każdy przebieg jako ponumerowana sekwencja zwykłym językiem: najpierw to, potem tamto, jeśli X to Y, w przeciwnym razie Z. Przebieg może mieć dwadzieścia kroków, jeśli ma dwadzieścia kroków. Gdzie krok niesie prawdziwą liczbę — ile tego przychodzi, jak często, jak duże — napisz ją w tym kroku, bo tam jest jej miejsce; nie wymyślaj jej: brak liczby to pytanie, które ktoś Ci zada, a zmyślona liczba staje się później zamrożonym limitem.>`

### `<nazwa części albo ficzera>`

1. `<co się dzieje najpierw — co przychodzi, albo co to odpala>`
2. `<...potem co, łącznie z rozgałęzieniami: „jeśli to polecenie, wykonaj je i nie traktuj jak rozmowy”>`
3. `<...aż do tego, co wychodzi, i co zostaje zapamiętane>`

**W przypadku awarii lub błędu:** `<Twoimi słowami — spróbuj jeszcze raz po cichu, powiedz mi, zatrzymaj wszystko, jedź dalej bez tej części. To decyzja biznesowa, nie techniczna, i jeśli nie podejmiesz jej tutaj, ktoś podejmie ją za Ciebie.>`

### `<następna część>` `<...powtórz>`

> **Zostań powyżej linii kodu.** Sekwencje w stylu „sprawdź, czy nadawca jest na mojej liście, a jeśli nie — zignoruj” są dokładnie tym, o co chodzi. „Wczytaj ID do zbioru przy starcie, żeby było szybko” jest o jeden poziom za głęboko — to decyzja, a decyzje należą do `Logic.md`. Gdy złapiesz się na nazywaniu mechanizmu zamiast zachowania, opisz to, co byś *zobaczył*.

## 5. Co to ma robić

`<Lista wywiedziona z §4: przeczytaj własne przebiegi i nazwij po kolei to, co każdy z nich daje. Jedna numerowana pozycja na każdą rzecz, którą ta rzecz ma umieć — trzymaj je krótko, bo cały szczegół stoi już wyżej. Numeruj F1, F2, … i nigdy nie przenumerowuj, nawet jeśli którąś skasujesz: Logic.md będzie cytować te numery, i każde późniejsze pytanie o dryf też.>`

**F1 — `<krótka nazwa>`**
- **Definicja:** `<jedno albo dwa zdania — co to jest i co robi>`
- **Oczekiwany rezultat:** `<co byś zobaczył, przeczytał, dostał albo zmierzył, tak żeby ktoś inny sprawdził to bez pytania Ciebie. „Dostanę raport do ósmej” da się sprawdzić. „Działa poprawnie” — nie.>`
- **Realizowane przez:** `<nazwy przebiegów z §4, które to realizują — albo „—”, jeśli to własność albo zdolność, a nie sekwencja>`

**F2 — `<krótka nazwa>`** `<...powtórz. Pozycją może być zdolność, zachowanie, doświadczenie albo pytanie, na które ta rzecz ma umieć odpowiedzieć.>`

> **Trzy nawyki.** Jeśli do opisania pozycji potrzebujesz słowa „i”, to pewnie są dwie pozycje — będą budowane i odbierane osobno. Jeśli nie umiesz napisać oczekiwanego rezultatu, to jeszcze nie jest pozycja; to życzenie, i zostanie zbudowane jako czyjś domysł. *Jeśli uczciwa odpowiedź brzmi „musiałbym spojrzeć na wyniki i ocenić je” — napisz dokładnie to* — to jest legalna odpowiedź, i mówi dokumentowi technicznemu, że ta część potrzebuje spisanej reguły, co liczy się jako wystarczająco dobre. A jeśli „realizowane przez” zostaje puste i nie umiesz powiedzieć, że to własność — to nie jest brak w tej linii, tylko brakujący przebieg w §4.
>
> **Nie ma tu ważniejszych i mniej ważnych.** Wszystko na tej liście jest w tej wersji, w całości. Rzecz, której chcesz „kiedyś” albo „jeśli się uda”, nie jest pozycją z połową wagi — jest wpisem w §6.2, i to jedyne uczciwe miejsce, gdzie może stanąć. Kolejności budowania ten plik nie ustala i nie próbuj jej tu przemycić: bierze się ona z zależności między częściami, i ustala ją `Railroad.md`.

## 6. Rules of Engagement

`<Trzy krótkie listy płaskich punktów. Bez prozy, bez akapitów — to jedyna sekcja, w której zdanie ucięte jest lepsze niż wypieszczone. Przykłady poniżej pokazują długość i ton, w jaki celujesz; podmień je.>`

### 6.1 Nigdy

*Reguły, których gotowa rzecz przestrzega przy każdym uruchomieniu, na zawsze. Żadnej z nich nikt nie wymienia na termin.*

- `<nigdy nie wysyłaj niczego do klienta, dopóki tego nie zobaczę>`
- `<nigdy nie kasuj ani nie zmieniaj pliku, który dostała — zawsze pracuj na kopii>`
- `<nigdy nie pokazuj danych jednej osoby w widoku drugiej>`

### 6.2 Nie w tej wersji

*Rzeczy, które potrafisz sobie wyobrazić i których świadomie jeszcze nie prosisz. **Ta lista nie powinna być pusta** — wszystko tu nazwane to coś, czego nikt nie zbuduje po cichu „przy okazji”, i czego nie zdziwisz się, że brakuje.*

- `<bez wersji na telefon — będę przy biurku, kiedy tego używam>`
- `<bez drugiego użytkownika w tym roku; to tylko ja>`
- `<bez automatycznego wysyłania — zawsze ja klikam>`

### 6.3 I tak narzucam

*Twoje własne ograniczenia co do **„jak”**, każde z powodem. **To jedyna lista w całym dokumencie, której wolno nazwać technologię, maszynę albo miejsce** — a ponieważ każda linia jest wyborem, a nie wymaganiem problemu, każdą da się zakwestionować z ceną w ręku. Nikt nie usunie żadnej bez pytania Cię; mogą Ci powiedzieć, ile kosztuje.*

- `<chodzi na moim komputerze, nie na wynajętym — nie chcę, żeby te dane wychodziły z budynku>`
- `<używa bazy, za którą już płacimy — druga baza to druga rzecz do utrzymywania>`
- `<jest napisane w języku, który zespół już czyta — chcę móc to naprawić bez Ciebie>`

> **Jeśli nie umiesz zdecydować, na którą listę idzie dana linia, zapytaj, kto może ją złamać.** **Działający program**, w dowolny wtorek → **6.1**. Tylko **zbudowanie tego źle**, i *Ty* to wybrałeś → **6.3**. Tylko zbudowanie tego źle, i *nikt* tego nie wybrał — po prostu tak jest tam, gdzie to chodzi → to nie jest w ogóle granica, to teren, i idzie do §7. Listy 6.2 nie łamie nic, i właśnie dlatego jest zakresem, a nie regułą.
>
> Przypadek, na którym potykają się wszyscy: *„nie może potrzebować internetu”*. Jeśli tam, gdzie to chodzi, nie ma połączenia — to **§7**. Jeśli jest, a Ty wolisz, żeby od niego nie zależało — to **6.3**, i to *dlaczego* jest połową wartą zapisania.

## 7. Docelowe Rules of Engagement

`<Siedem pytań. Na każde odpowiedz własnym zdaniem, w miejscu po nim; kursywa pod spodem to podpowiedź, jakiego rodzaju odpowiedzi się tu spodziewamy, a nie menu do wyboru. **„Nie wiem” jest pełną odpowiedzią** — uczciwa luka zostaje później rozwiązana, zmyślona zostaje zamrożona w projekcie.>`

**Kształt, żeby nie było wątpliwości:** na *„co to odpala?”* gotowa odpowiedź brzmi `Odpalam sam, zwykle późnym wieczorem, kiedy wracam z trasy.` Zwykłe zdanie, żadnego mechanizmu — i przy okazji odpowiada też na trzecie pytanie.

- **Co to odpala?** `<...>`
  *ja, ręcznie · inny program · zegar, według harmonogramu · przychodzące zdarzenie · urządzenie*
- **Kto albo co dostaje wynik?** `<...>`
  *ja · ktoś inny niż ja · inny program · ekran, na który nikt nie patrzy · maszyna*
- **Czy ma chodzić samo?** `<...>`
  *„odpalam, kiedy potrzebuję” · „ma się po prostu dziać, beze mnie”. Odpowiedz na to nawet jeśli na nic innego tutaj — to pojedyncze pytanie, które najbardziej zmienia to, jak rzecz musi być zbudowana.*
- **Jakich informacji dotyka?** `<...>`
  *moje notatki · dane osobowe innych ludzi · pieniądze · cudzy system ewidencji · nic, co by bolało, gdyby wyciekło*
- **Gdy coś padnie, co wolisz?** `<...>`
  *poczekaj i spróbuj jeszcze raz po cichu · powiedz mi od razu · zatrzymaj i nic nie zmieniaj · jedź dalej z tą częścią, która jeszcze działa*
- **Gdzie to ostatecznie będzie chodzić?** `<...>`
  *mój laptop · maszyna w pracy, którą administruje ktoś inny · serwer · małe urządzenie gdzieś fizycznie · telefon · „gdziekolwiek, nie mam zdania”. Dopisz, co o tym miejscu wiesz: czy jest internet, czy jest zawsze włączone, czy restartuje się samo, czy ktoś inny się na nie loguje, czy masz prawa administratora.*
- **Gdzie to będzie budowane, i czy to to samo miejsce?** `<...>`
  *jeśli Ty albo agent będziecie nad tym pracować na więcej niż jednej maszynie — desktop i laptop, praca i dom, jedna z narzędziami i jedna bez — napisz to. Budowa, która się przemieszcza, musi to mieć zapisane przed pierwszą sesją, nie odkryte w trzeciej.*

> **Dlaczego dwa ostatnie pytania są tutaj, a nie w §6.3.** Ten sam temat, odwrotny status. Środowisko, które **wybrałeś**, jest ograniczeniem z §6.3 i da się je wycenić oraz do niego wrócić. Środowisko, które po prostu **jest** — maszyna restartująca się o północy, laptop bez praw administratora — jest terenem: nie Ty je wybrałeś i nie wykupisz się z niego, więc da się je tylko obejść projektem.
>
> **Nadal nie należy ani tu, ani tam:** toolchain. *„Musi działać offline na małym urządzeniu”* to teren. *„Użyj tego frameworka i tej bazy”* to decyzja, i zostaje w `Logic.md` — podjęta wobec wszystkiego, co tu napisane, a nie wybrana, zanim ktokolwiek wiedział, co ta rzecz ma robić.

## 8. Stan obecny w momencie pisania dokumentacji **[OPCJONALNE — skasuj tę sekcję, jeśli ta rzecz nie istnieje jeszcze w żadnej formie]**

`<Tylko jeśli jest jakiś obecny sposób robienia tego: ręczne kroki, arkusz, kopiuj-wklej, „pamiętam, żeby to robić w piątki”. Jeśli projekt jest nowy i nie ma poprzednika — skasuj sekcję. Pusta sekcja jest gorsza niż nieobecna.>`

## 9. Moje otwarte pytania

`<Rzeczy, których jeszcze nie zdecydowałeś, własnymi słowami. Widoczne niedecyzje zostają rozwiązane; niewidoczne decyduje za Ciebie ten, kto buduje tę część.>`

## 10. Doprecyzowania z rozmów

`<Wpisz odpowiedzi z powrotem do tego pliku, własnymi słowami, a nie agenta — okno czatu się przewija. A jeśli zapytają Cię o to samo dwa razy, nie odpowiadaj po prostu jeszcze raz: sekcja, której to dotyczy, jest niejasna, więc popraw sekcję.>`

| # | Pytanie | Moja odpowiedź | Co zmieniło |
|---|---|---|---|
| 1 | `<...>` | `<...>` | `<F3 / §2 / §6>` |

## 11. Dalsze plany rozwoju — zapowiedź, nie zamówienie

`<Kierunki, których jesteś już w miarę pewien i których świadomie nie specyfikujesz: „docelowo to obsłuży cały zespół, nie tylko mnie”, „w pewnym momencie dane będą musiały leżeć tam, gdzie inni je przeczytają”, „spodziewam się, że kiedyś będę chciał, żeby chodziło z harmonogramu”. Napisz, czego się spodziewasz, i z grubsza kiedy, jeśli masz jakieś z grubsza kiedy. **Nie** opisuj, jak to ma działać — to jest ta część, która zmienia tę sekcję z pożytecznej w szkodliwą.>`

> **Czym to się różni od §6.2.** Tamta lista to **nie**: coś, czego chcesz, o co teraz nie prosisz, a dokument techniczny zapisuje to jako pracę odłożoną. Ta sekcja to **tak, kiedyś**: kierunek, w który już wierzysz, i o którego zbudowanie, zaplanowanie ani uwzględnienie nikt nie jest proszony. Oba stoją poza tą wersją — różnica jest w tym, że jedno zostało odrzucone, a drugie przewidziane. Jeden haczyk wart znajomości: linia, która nazywa tu konkretny silnik albo maszynę, nie jest kierunkiem — jest ograniczeniem, które już wybrałeś, i należy do §6.3, gdzie da się ją wycenić.

> **Jedna reguła, która nie pozwala tej sekcji zaszkodzić — może rozstrzygnąć remis, nigdy nie może kupić struktury.** Tam, gdzie dwa projekty są poza tym równe, lepszy jest ten, który nie zamyka drogi do czegoś tu nazwanego — i to jest cała wartość zapisania tego. Nic z tej listy nie może być powołane jako powód, dla którego abstrakcja, flaga konfiguracyjna, punkt rozszerzeń albo zapasowa warstwa istnieje **dziś**. System pluginów zbudowany, bo ta sekcja wspomina pluginy, jest dokładnie tą porażką, przed którą stoją reguły przeciw przeinżynierowaniu w dokumencie technicznym — a ta sekcja czyni ją łatwiejszą do osiągnięcia, i właśnie dlatego reguła jest zapisana tutaj, a nie zostawiona zdrowemu rozsądkowi. To samo dotyczy Ciebie: jeśli złapiesz się na pisaniu kroków, rozgałęzień albo kształtów dla czegoś z tej listy, przestało to być uprzedzeniem i stało się pozycją z §5, o którą nigdy nie zdecydowałeś się poprosić. Przenieś to albo wytnij.

---

## 12. Czy jestem gotów przejść do `Logic.md`?

To nie formalność — przejście tej listy sprawia, że dokument techniczny da się napisać bez zgadywania.

- [ ] **Każdą pozycję z §5 da się wywieść z założenia w §2**, a §2 nie obiecuje kierunku, którego §5 nie obsługuje.
- [ ] Każda pozycja w §5 ma **oczekiwany rezultat**, który ktoś inny sprawdzi bez pytania mnie.
- [ ] **Każda pozycja z §5 wskazuje przebieg z §4, który ją realizuje** — albo jawnie mówi, że jest własnością, a nie sekwencją; i każdy przebieg z §4 realizuje przynajmniej jedną pozycję.
- [ ] Każda część w §4 ma wypełnione **„W przypadku awarii lub błędu”**.
- [ ] **§6.1, §6.2 i §6.3 mają wpisy**, a §6.2 w szczególności nie jest pusta.
- [ ] **Każde pytanie w §7 ma odpowiedź moimi słowami** — żadna podpowiedź nie stoi w miejscu odpowiedzi, a tam, gdzie taka jest prawda, napisane jest „nie wiem”.
- [ ] **Na pytanie z §7 „czy ma chodzić samo?” jest odpowiedź** — albo fakt, że nie wiem, jest w §9.
- [ ] **§3 ma wypełnione drzewo** w formie, którą pokazuje szablon — części zagnieżdżone pod częściami, jednozdaniowa odpowiedzialność w każdej linii, nie zostawione jako placeholdery i nie napisane jako nazwy plików.
- [ ] Poza **§6.3** nic nie nazywa technologii, biblioteki, pliku ani funkcji, a każda linia w §6.3 ma dopisany powód.
- [ ] **§11 nie opisuje żadnego mechanizmu** — każda linia mówi, *co* nadchodzi, nigdy *jak* miałoby działać.
- [ ] Pozycje są ponumerowane `F#` i nie przenumerowywałem ich.
- [ ] Mógłbym przeprowadzić kogoś przez ten dokument **na jednym posiedzeniu**, i ta osoba umiałaby mi powiedzieć, co ta rzecz robi.

**Gdy to wszystko stoi, otwiera się `Logic.md`** — i każde dalsze doprecyzowanie logiki biznesowej dzieje się *tam*, łącznie z częściami, o których jeszcze nie pomyślałeś. Ten plik przestaje być edytowany tego samego dnia, bez wyjątków: jest teraz zapisem tego, o co pierwotnie prosiłeś, i ten zapis jest wart dokładnie tyle, ile jego opór wobec późniejszego porządkowania.

`Specyfikacja zamrożona: <data> · przeniesiona do ARCH/ · Logic.md Mk <N> Mod <M> A<K> otwarty z niej`
