>[!NOTE]
>Dla zasobów, które nie zostały usunięte może poprosić o toobe przydziały hello wywoływane przez otwarcie biletu pomocy technicznej. Czy **nie** utworzyć dodatkowych kont usługi Azure Media Services, próbując tooobtain wyższe limity.

| Zasób | Limit domyślny | 
| --- | --- | 
| Konta usługi Azure Media Services (AMS) w jednej subskrypcji | 25 (stały) |
| Jednostki zarezerwowane multimediów na konto AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Zadania na konto AMS | 50,000<sup>(2)</sup> |
| Łańcuchowe zadania podrzędne na zadanie | 30 (stały) |
| Elementy zawartości na konto AMS | 1 000 000|
| Elementy zawartości na zadanie podrzędne | 50 |
| Elementy zawartości na zadanie | 100 |
| Unikatowe lokalizatory jednocześnie skojarzone z elementem zawartości | 5<sup>(4)</sup> |
| Kanały na żywo dla każdego konta AMS |5|
| Programy w stanie zatrzymania na kanał |50|
| Programy w stanie działania na kanał |3|
| Punkty końcowe przesyłania strumieniowego w stanie działania na konto AMS|2|
| Jednostki przesyłania strumieniowego na punkt końcowy przesyłania strumieniowego |10 |
| Konta magazynu | 1000<sup>(5)</sup> (stały) |
| Zasady | 1 000 000<sup>(6)</sup> |
| Rozmiar pliku| W niektórych scenariuszach istnieje limit na powitania maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services. <sup>7</sup> |
  
<sup>1</sup> Jednostki zarezerwowane S3 nie są dostępne w regionie Indie Zachodnie. maksymalny limit RU Hello resetowane zmiana powitania klienta hello typu (np. z S2 tooS1). 

<sup>2</sup> Ta liczba obejmuje zadania umieszczone w kolejce, zakończone, aktywne i anulowane. Nie obejmuje usuniętych zadań. Można usunąć zadania starego hello przy użyciu **IJob.Delete** lub hello **usunąć** żądania HTTP.

Uruchamianie 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 90 dni zostaną automatycznie usunięte, wraz z jego skojarzonych rekordów zadań, nawet jeśli hello całkowita liczba rekordów jest poniżej hello maksymalny limit przydziału. Jeśli potrzebujesz informacji zadania lub zadanie hello tooarchive, można użyć kodu hello opisane [tutaj](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> podczas tworzenia żądania toolist zadania jednostek, zostanie zwrócony maksymalnie 1000 na żądanie. Jeśli potrzebujesz tookeep track przesłane wszystkich zadań, możesz użyć top/skip zgodnie z opisem w [opcje zapytania systemu OData](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Lokalizatory nie są przeznaczone do zarządzania kontrolą dostępu dla poszczególnych użytkowników. toogive użytkowników tooindividual prawa dostępu różnych, użycie rozwiązań zarządzania prawami cyfrowymi (DRM). Więcej informacji znajduje się w [tej](../articles/media-services/media-services-content-protection-overview.md) sekcji.

<sup>5</sup> hello konta magazynu musi mieć długość od hello tej samej subskrypcji platformy Azure.

<sup>6</sup> Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / uprawnień dostępu / itd. Informacje i przykład możesz znaleźć w [tej](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) sekcji.

<sup>7</sup>podczas przekazywania tooan zawartości zasobów w Azure Media Services z tooprocess konwersji hello nią za pomocą jednego hello procesory multimediów w naszej usługi (np. koderów, takich jak aparaty Media Encoder Standard i Media Encoder Premium w przepływie pracy lub analizy Podobnie jak krój detektora) następnie należy zwrócić uwagę ograniczenia hello na powitania maksymalny rozmiar. 

Począwszy od 15 maja 2017 hello maksymalny rozmiar obsługiwany dla pojedynczego obiektu blob 195 TB — z pliku largers przekracza ten limit, zadanie zakończy się niepowodzeniem. Pracujemy nad tooaddress poprawka ten limit. Ponadto hello ograniczenie maksymalnego rozmiaru hello hello zasobów ma następującą składnię.

| Typ jednostki zarezerwowanej multimediów | Maksymalny rozmiar wejściowe (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
