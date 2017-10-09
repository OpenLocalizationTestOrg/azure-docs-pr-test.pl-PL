Witaj w poniższej tabeli opisano wszystkie główne przydziały hello, limity ustawień domyślnych i limity w harmonogramie Azure.

| Zasób | Opis elementu limit |
| --- | --- |
| **Rozmiar zadania** |Maksymalny rozmiar zadania jest 16 KB. Jeśli PUT lub POPRAWKĘ powoduje większe niż limity te zadania, 400 Niewłaściwe żądanie kod stanu jest zwracany. |
| **Rozmiar adresu URL żądania** |Maksymalny rozmiar adresu URL żądania hello to 2048 znaków. |
| **Rozmiar nagłówka agregacji** |Rozmiar maksymalny łączny nagłówka to 4096 znaków. |
| **Liczba nagłówka** |Liczba maksymalna nagłówka jest 50 nagłówków. |
| **Rozmiar treści** |Rozmiar maksymalny treści to 8192 znaków. |
| **Zakres cyklu** |Maksymalna wartość cyklu zakres jest 18 miesięcy. |
| **Czas toostart czasu** |"Czas toostart czas" Maksymalna liczba to 18 miesięcy. |
| **Historia zadania** |Treść odpowiedzi maksymalną przechowywanych w historii zadań wynosi 2048 bajtów. |
| **Częstotliwość** |przydział maksymalnej częstotliwości domyślny Hello jest 1 godzina bezpłatna kolekcja zadań i 1 minuta w kolekcji standardowych zadania. częstotliwość max Hello jest konfigurowany na toobe kolekcji zadań mniejszy niż maksymalny hello. Wszystkie zadania w kolekcji zadań hello są ograniczone hello wartość na powitania kolekcji zadań. Jeśli próba toocreate zadania z częstotliwością wyższe niż maksymalna częstotliwość hello na kolekcji zadań hello żądanie zakończy się niepowodzeniem z kodem stanu 409 konflikt. |
| **Zadania** |Hello domyślnego przydziału maksymalnej zadania jest 50 zadań w kolekcji standardowych zadania i 5 zadania w bezpłatna kolekcja zadań. Maksymalna liczba zadań Hello jest można skonfigurować na kolekcji zadań. Wszystkie zadania w kolekcji zadań hello są ograniczone hello wartość na powitania kolekcji zadań. Jeśli próba toocreate większą liczbę zadań niż hello zadania maksymalny przydział, a następnie hello żądanie kończy się niepowodzeniem z kodem stanu 409 konflikt. |
| **Kolekcje zadań** |Maksymalna liczba kolekcji zadań dla subskrypcji to 200 000. |
| **Przechowywanie historii zadań** |Historii zadań został zachowany na potrzeby too2 miesięcy lub zapasowej toohello ostatniego wykonania 1000. |
| **Przechowywanie zadań została zakończona i błędnej** |Zadania ukończone i błędnej są przechowywane przez 60 dni. |
| **Limit czasu** |Brak statyczne (nie można konfigurować) żądania limitu czasu 60 sekund dla akcji HTTP. W przypadku operacji dłużej wykonaj asynchroniczne protokołów HTTP; na przykład zwracać 202 natychmiast, ale nadal działa w tle hello. |

