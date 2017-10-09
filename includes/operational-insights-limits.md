
>[!NOTE]
>Usługa Log Analytics wcześniej nosiła nazwę Operational Insights.
>
>

Witaj następujące limity Zastosuj tooLog analizy zasobów dla subskrypcji:

| Zasób | Limit domyślny | Komentarze
| --- | --- | --- |
| Liczba wolnych obszarów roboczych na subskrypcję | 10 | Tego limitu nie można zwiększyć. |
| Liczba płatnych obszarów roboczych na subskrypcję | Nie dotyczy | Są ograniczone przez hello liczbę zasobów w grupie zasobów i wiele grup zasobów dla subskrypcji | 


Witaj następujące limity Zastosuj tooeach obszaru roboczego analizy dzienników:

|  | Bezpłatna | Standardowa | Premium | Autonomiczna | OMS |
| --- | --- | --- | --- | --- | --- |
| Ilość danych zebranych na dzień |500 MB<sup>1</sup> |Brak |Brak | Brak | Brak
| Okres przechowywania danych |7 dni |1 miesiąc |12 miesięcy | 1 miesiąc<sup>2</sup> | 1 miesiąc <sup>2</sup>|

<sup>1</sup> klientów osiągnięciu limitu transferu danych codzienne ich 500 MB danych analizy zatrzyma się i zostanie wznowione na początku hello hello następnego dnia. Dzień jest oparty na czasie UTC.

<sup>2</sup> okres przechowywania danych hello hello autonomicznych i OMS planów cenowych może być zwiększona too730 dni.

| Kategoria | Limity | Komentarze
| --- | --- | --- |
| Interfejs API modułu zbierającego dane | Maksymalny rozmiar pojedynczego wpisu to 30 MB<br>Maksymalny rozmiar wartości pól to 32 KB | Dziel większe woluminy na wiele wpisów<br>Pola dłuższe niż 32 KB są obcinane. |
| Interfejs API wyszukiwania | 5000 rekordów zwracanych dla danych niezagregowanych<br>500 000 rekordów dla danych zagregowanych | Zagregowane dane są wyszukiwania, która obejmuje hello `measure` polecenia
 
