Magazyn jest ograniczane przez miejsca na dysku lub nienaruszalne ograniczenie hello *maksymalną liczbę* indeksy lub dokumenty zależności zostanie osiągnięty jako pierwszy.

| Zasób | Bezpłatna | Podstawowa | S1 | S2 | S3 | S3 (wysoka gęstość) |
| --- | --- | --- | --- | --- | --- | --- |
| Umowa dotycząca poziomu usług (SLA) |Nie<sup>1</sup> |Tak |Tak |Tak |Tak |Tak |
| Magazyn na partycję |50 MB |2 GB |25 GB |100 GB |200 GB |200 GB |
| Partycje na usługę |Nie dotyczy |1 |12 |12 |12 |3<sup>2</sup> |
| Rozmiar partycji |Nie dotyczy |2 GB |25 GB |100 GB |200 GB |200 GB |
| Repliki |Nie dotyczy |3 |12 |12 |12 |12 |
| Maksymalna liczba indeksów |3 |5 |50 |200 |200 |1000 na partycję lub 3000 na usługę |
| Maksymalna liczba indeksatorów |3 |5 |50 |200 |200 |Brak obsługi indeksatorów |
| Maksymalna liczba źródeł danych |3 |5 |50 |200 |200 |Brak obsługi indeksatorów |
| Maksymalna liczba dokumentów |10 000 |1 mln |15 mln na partycję lub 180 mln na usługę |60 mln na partycję lub 720 mln na usługę |120 mln na partycję lub 1,4 mld na usługę |1 mln na indeks lub 200 mln na partycję |
| Szacowana liczba zapytań na sekundę |Nie dotyczy |Około 3 na replikę |Około 15 na replikę |Około 60 na replikę |Około 60 na replikę |Ponad 60 na replikę |

<sup>1</sup> bezpłatnej warstwy i Podgląd funkcji nie pochodzą z umów dotyczących poziomu usług (SLA). Dla wszystkich warstw rozliczeniowy umowy SLA zaczną obowiązywać podczas obsługi administracyjnej nadmiarowość wystarczające dla Twojej usługi. Co najmniej dwa repliki są wymagane do umowy SLA kwerendy (odczyt). Co najmniej trzech repliki są wymagane dla zapytań i indeksowania SLA (odczytu i zapisu). Hello liczby partycji nie jest brany pod uwagę umowy dotyczącej poziomu usług. 

<sup>2</sup> S3 HD ma górny limit 3 partycji mniejszy niż limit partycji hello S3. Dolna granica partycji Hello nakłada się, ponieważ liczba indeksu hello S3 HD jest znacznie wyższa. Podane ograniczenia usługi istnieje dla obu zasobów obliczeniowych (przechowywania i przetwarzania), a zawartości (indeksów oraz dokumentów), hello zawartości limit zostanie osiągnięty jako pierwszy.
