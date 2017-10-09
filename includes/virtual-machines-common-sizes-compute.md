<!-- F-series, Fs-series* -->

F-series opiera się na powitania 2.4 v3® GHz Intel Xeon E5-2673 procesora (Haswell), który można uzyskać możliwie jak 3.1 GHz z hello Intel Turbo zwiększanie wyniku technologii 2.0 szybkości zegara. Jest to hello sama wydajność Procesora, ponieważ hello Dv2 serii maszyn wirtualnych.  W dolnym godzinową cennika hello F-series jest hello wartość najlepsze w hello Azure portfolio oparte na hello Azure obliczeniowe jednostki (ACU) na vCPU cen — wydajność. 

Maszyny wirtualne z serii F są doskonałym wyborem dla obciążeń wymagających szybszych procesorów CPU, ale nie potrzebujących tak dużej ilości pamięci lub magazynu tymczasowego na każdy procesor wirtualny vCPU.  Obciążeń, takich jak analizy, serwery gier, serwery sieci web i przetwarzania wsadowego będą korzystać z wartości hello hello F serii.

Witaj Fs serii zawiera wszystkie zalety hello hello F-series, w magazynie tooPremium dodanie.

## <a name="fs-series"></a>Seria Fs*

ACU: 210–250

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_F1s |1 |2 |4 |2 |4000 / 32 (12) |3200 / 48 |2 / 750 |
| Standardowa_F2s |2 |4 |8 |4 |8000 / 64 (24) |6400 / 96 |2 / 1500 |
| Standardowa_F4s |4 |8 |16 |8 |16 000 / 128 (48) |12 800 / 192 |4 / 3000 |
| Standardowa_F8s |8 |16 |32 |16 |32 000 / 256 (96) |25 600 / 384 |8 / 6000 |
| Standardowa_F16s |16 |32 |64 |32 |64 000 / 512 (192) |51 200 / 768 |8 / 6000-12000 &#8224; |

MB/s = 10^6 bajtów na sekundę, GiB = 1024^3 bajtów.

* hello maksymalną przepływność dysku (IOPS lub MB/s) przy użyciu serii Fs maszyny Wirtualnej może być ograniczony przez hello liczba, rozmiar i rozkładanie hello dołączone dyski.  Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure).


<br>

## <a name="f-series"></a>Seria F

ACU: 210–250

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standardowa_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standardowa_F4  | 4         | 8           | 64             | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standardowa_F8  | 8         | 16          | 128            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standardowa_F16 | 16        | 32          | 256            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000–12 000 &#8224;           |


<br>


