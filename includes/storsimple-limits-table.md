<!--author=alkohli last changed: 12/15/15-->

| Identyfikator limitu | Limit | Komentarze |
| --- | --- | --- |
| Maksymalna liczba poświadczeń konta magazynu |64 | |
| Maksymalna liczba kontenery woluminów |64 | |
| Maksymalna liczba woluminów |255 | |
| Maksymalna liczba harmonogramów na szablon przepustowości |168 |Harmonogram dla każdej godziny, każdego dnia tygodnia hello (24 * 7). |
| Maksymalny rozmiar woluminu warstwowego na fizycznych urządzeniach |64 TB 8100 i 8600 |8100 i 8600 są urządzenia fizyczne. |
| Maksymalny rozmiar woluminu warstwowego na urządzenia wirtualne na platformie Azure |30 TB dla 8010 <br></br> 64 TB dla urządzenia 8020 |urządzenia 8010 i 8020 są urządzeń wirtualnych na platformie Azure używających magazynu w warstwie standardowa i Premium Storage odpowiednio. |
| Maksymalny rozmiar woluminu przypiętego lokalnie na fizycznych urządzeniach |9 TB dla 8100 <br></br> 24 TB dla 8600 |8100 i 8600 są urządzenia fizyczne. |
| Maksymalna liczba połączeń iSCSI |512 | |
| Maksymalna liczba połączeń iSCSI z inicjatorów |512 | |
| Maksymalna liczba rekordów kontroli dostępu na urządzeniu |64 | |
| Maksymalna liczba woluminów na zasad tworzenia kopii zapasowej |24 | |
| Maksymalna liczba kopii zapasowych przechowywane dla poszczególnych zasad tworzenia kopii zapasowej |64 | |
| Maksymalna liczba harmonogramy dla poszczególnych zasad tworzenia kopii zapasowej |10 | |
| Maksymalna liczba migawek dowolnego typu, które mogą być przechowywane na każdym woluminie |256 |Dotyczy to również migawki lokalne i migawki w chmurze. |
| Maksymalna liczba migawek, które mogą być obecne w dowolnym urządzeniu |10 000 | |
| Maksymalna liczba woluminów, które mogą być przetwarzane równolegle do tworzenia kopii zapasowych, przywracania lub klonowania |16 |<ul><li>Jeśli istnieje więcej niż 16 woluminów, będą przetwarzane sekwencyjnie jako udostępnienie gniazda przetwarzania.</li><li>Nowe kopie zapasowe sklonowany lub przywrócony wolumin warstwowy może nastąpić dopiero po zakończeniu operacji hello. Jednak na lokalnym woluminie, kopie zapasowe są dozwolone po woluminu hello jest w trybie online.</li></ul> |
| Przywracanie i klonowanie czas Odzyskaj woluminy warstwowe |< 2 minuty |<ul><li>w ciągu 2 minut operacji przywracania lub klonowania, niezależnie od rozmiaru woluminu hello woluminu Hello staje się dostępny.</li><li>wydajność woluminu Hello początkowo mogą być wolniej niż zwykle, ponieważ znajduje się w chmurze hello większość hello danych i metadanych. Wydajność może zwiększyć jako przepływów danych z urządzenia StorSimple toohello hello w chmurze.</li><li>metadane toodownload całkowity czas Hello zależy od hello przydzielony rozmiar woluminu. Metadane automatycznie wejścia urządzenia hello w tle hello szybkością hello 5 minut na TB danych przydzielonego woluminu. Ta stawka może dotyczyć chmury toohello przepustowości Internetu.</li><li>Witaj przywracania lub Operacja klonowania została ukończona, gdy wszystkie metadane hello jest na urządzeniu hello.</li><li>Nie można wykonać operacji tworzenia kopii zapasowej do przywrócenia hello lub pełni zakończeniu operacji klonowania. |
| Przywracanie odzyskać czas dla woluminów przypiętych lokalnie |< 2 minuty |<ul><li>w ciągu 2 minut hello operacji przywracania, niezależnie od rozmiaru woluminu hello woluminu Hello staje się dostępny.</li><li>wydajność woluminu Hello początkowo mogą być wolniej niż zwykle, ponieważ znajduje się w chmurze hello większość hello danych i metadanych. Wydajność może zwiększyć jako przepływów danych z urządzenia StorSimple toohello hello w chmurze.</li><li>metadane toodownload całkowity czas Hello zależy od hello przydzielony rozmiar woluminu. Metadane automatycznie wejścia urządzenia hello w tle hello szybkością hello 5 minut na TB danych przydzielonego woluminu. Ta stawka może dotyczyć chmury toohello przepustowości Internetu.</li><li>W odróżnieniu od woluminów warstwowych, w przypadku hello woluminów przypiętych lokalnie danych woluminu hello jest również pobierane lokalnie na urządzeniu hello. Operacja przywracania Hello została ukończona, gdy wszystkie dane woluminu hello wprowadziło toohello urządzenia.</li><li>operacje przywracania Hello może trwać długo i hello całkowity czas toocomplete hello przywracania zależy od rozmiaru hello hello udostępniane na lokalnym woluminie, przepustowości połączenia z Internetem i hello istniejące dane na urządzeniu hello. Operacje tworzenia kopii zapasowej na wolumin przypięty lokalnie hello są dozwolone w trakcie operacji przywracania hello jest w toku. |
| Dostępność elastycznej przywracania |Ostatni trybu failover | |
| Przepływność odczytu/zapisu maksymalną klienta (jeśli są udostępniane przez warstwę dysków SSD hello) * |920/720 MB/s z jednym 10 GbE interfejsu sieciowego |Zapasowej too2x wielościeżkowego wejścia/wyjścia i dwa interfejsy sieciowe. |
| Przepływność odczytu/zapisu maksymalną klienta (jeśli są udostępniane przez warstwę HDD hello) * |120/250 MB/s | |
| Przepływność odczytu/zapisu maksymalną klienta (jeśli jest obsługiwana z warstwy chmury hello) * |11/41 MB/s |Przepływność odczytu zależy od klientów generowania i utrzymywania wystarczające głębokość kolejki operacji We/Wy. |

&#42; Maksymalna przepustowość na typ operacji We/Wy zmierzono z scenariusze 100 procent zapisu i odczytu 100 procent. Aktualna przepływność może być niższa i zależy od operacji We/Wy mieszać i warunki sieciowe.

