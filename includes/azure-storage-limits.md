| Zasób | Limit domyślny |
| --- | --- |
| Liczba kont magazynu dla subskrypcji |200<sup>1</sup> |
| Maksymalna pojemność konta |500 TB<sup>2</sup> |
| Maksymalna liczba kontenerów obiektów blob, obiekty BLOB, udziałów plików, tabel, kolejek, jednostki lub wiadomości dla konta magazynu |Bez ograniczeń |
| Maksymalny rozmiar kontenera pojedynczego obiektu blob, tabel lub kolejek |Identyczny maksymalnej pojemności konta |
| Maksymalna liczba bloków w blokowych obiektów blob lub uzupełnialnych obiektów blob |50,000 |
| Maksymalny rozmiar bloku w blokowych obiektów blob |100 MB |
| Maksymalny rozmiar blokowych obiektów blob |50 000 x 100 MB (około 4,75 TB) |
| Maksymalny rozmiar bloku w uzupełnialnym obiekcie blob |4 MB |
| Maksymalny rozmiar uzupełnialnego obiektu blob |50 000 x 4 MB (około 195 GB) |
| Maksymalny rozmiar obiektu blob strony |8 TB |
| Maksymalny rozmiar jednostki tabeli |1 MB |
| Maksymalna liczba właściwości w obiekcie tabeli |252 |
| Maksymalny rozmiar wiadomości w kolejce |64 KB |
| Maksymalny rozmiar udziału plików |5 TB |
| Maksymalny rozmiar pliku w udziale plików |1 TB |
| Maksymalna liczba plików w udziale plików |Tylko limit wynosi 5 TB całkowita pojemność udziału plików |
| Maksymalna liczba IOPS udziału |1000 |
| Maksymalna liczba plików w udziale plików |Tylko limit wynosi 5 TB całkowita pojemność udziału plików |
| Maksymalna liczba zasady dostępu przechowywanych na kontenera, udziału plików, tabel lub kolejek |5 |
| Maksymalna szybkość żądania na konto magazynu |Obiekty BLOB: 20 000 żądań na sekundę<sup>2</sup> dla obiektów blob o dowolnym rozmiarze prawidłowe (ograniczone tylko przez limity wejście/wyjście konta) <br />Pliki: 1000 IOPS (o rozmiarze 8 KB) dla udziału plików <br />Kolejki: 20 000 komunikatów na sekundę (przyjmuje rozmiar komunikatu o rozmiarze 1 KB)<br />Tabele: 20 000 transakcji na sekundę (przyjmuje rozmiar jednostki o rozmiarze 1 KB) |
| Przepływność docelowy dla pojedynczego obiektu blob |60 MB na drugi lub do 500 żądań na sekundę |
| Przepływność docelowy dla pojedynczej kolejki (1 KB wiadomości) |Maksymalnie 2000 komunikatów na sekundę |
| Przepływność docelowy dla pojedynczej tabeli partycji (o rozmiarze 1 KB jednostki) |Maksymalnie 2000 jednostek na sekundę |
| Docelowy przepływności jeden udział pliku |60 MB na sekundę |
| Maksymalna liczba wejściowych<sup>3</sup> na konto magazynu (nam regiony) |10 GB/s Jeśli GRS/ZRS<sup>4</sup> włączone, 20 GB/s dla LRS<sup>2</sup> |
| Maksymalna liczba wyjście<sup>3</sup> na konto magazynu (nam regiony) |20 GB, jeśli RA-GRS/GRS/ZRS<sup>4</sup> włączone 30 GB/s dla LRS<sup>2</sup> |
| Maksymalna liczba wejściowych<sup>3</sup> na konto magazynu (regiony Non-US) |5 GB/s Jeśli GRS/ZRS<sup>4</sup> włączone 10 GB/s dla LRS<sup>2</sup> |
| Maksymalna liczba wyjście<sup>3</sup> na konto magazynu (regiony Non-US) |10 GB/s Jeśli RA-GRS/GRS/ZRS<sup>4</sup> włączone, 15 GB/s dla LRS<sup>2</sup> |

<sup>1</sup>obejmuje zarówno standardowa i Premium konta magazynu. Jeśli potrzebujesz więcej niż 200 kont magazynu, wyślij żądanie za pośrednictwem [Pomocy technicznej platformy Azure](https://azure.microsoft.com/support/faq/). Zespół usługi Azure Storage przejrzy Twój przypadek biznesowy i może zatwierdzić do 250 kont magazynu. 

<sup>2</sup> można uzyskać konta magazynu w warstwie standardowa do zwiększenia poza granicami anonsowany w polu Szybkość pojemności, wejście/wyjście i żądania, Wyślij żądanie za pośrednictwem [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/faq/). Zespół usługi Azure Storage będzie Przejrzyj żądanie i może zatwierdzić wyższe limity na podstawie przypadku.

<sup>3</sup>*wejściowych* odwołuje się do wszystkich danych (liczba żądań) są wysyłane do konta magazynu. *Ruch wychodzący* odnosi się do wszystkich danych (żądań) wysyłanych z konta magazynu.  

<sup>4</sup>dostępne są następujące opcje replikacji usługi azure Storage:
* **RA-GRS**: dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu. Jeśli włączono RA-GRS, docelowe wyjście dodatkowej lokalizacji są identyczne jak do lokalizacji głównej.
* **GRS**: Magazyn geograficznie nadmiarowy. 
* **Magazyn ZRS**: Magazyn Strefowo nadmiarowy. Dostępne tylko dla blokowych obiektów blob. 
* **Magazyn LRS**: Magazyn lokalnie nadmiarowy. 


