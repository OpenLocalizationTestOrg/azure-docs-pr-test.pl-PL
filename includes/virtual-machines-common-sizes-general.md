
<!-- A-series, Av2-series, D-series, Dv2-series, DS-series*, DSv2-series* -->

- Hello A-series i Av2 serii maszyn wirtualnych może zostać wdrożony w różne typy sprzętu i procesorów. rozmiar Hello jest ograniczany na powitania sprzętu, wydajność procesora spójne toooffer hello uruchomione wystąpienie, niezależnie od sprzętu hello, który jest wdrożony na podstawie. toodetermine hello sprzętu fizycznego wdrożeniu ten rozmiar, zapytania hello sprzęt wirtualny z wewnątrz hello maszyny wirtualnej.

- D-series maszyny wirtualne są zaprojektowane toorun aplikacji, które wymaga wyższej moc obliczeniową i wydajność dysku tymczasowym. Maszyny wirtualne D-series zapewniają szybkich procesorów, większy współczynnik pamięci do vCPU i dysków półprzewodnikowych (SSD) dla dysku tymczasowym hello. Aby uzyskać więcej informacji, zobacz anons hello na powitania Azure blog [nowe rozmiary maszyny wirtualnej D-Series](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

- Dv2-series, finałowa toohello oryginalnego D-series, funkcje większe możliwości procesora CPU. Hello serii Dv2 Procesora CPU D-series jest około 35% szybciej niż hello. Jest on oparty na powitania najnowszej generacji 2.4 v3® GHz Intel Xeon E5-2673 procesora (Haswell) i z hello Intel Turbo zwiększanie wyniku technologii 2.0, może przejść w górę too3.1 GHz. ma Hello serii Dv2 hello takie same konfiguracje pamięci i dysku, ponieważ hello D-series.

- rozmiarów warstw podstawowa Hello są głównie w przypadku obciążeń programowanie i inne aplikacje, które nie wymagają Równoważenie obciążenia, automatyczne skalowanie i pamięć maszyny wirtualne. Aby uzyskać informacje na temat rozmiarów maszyn wirtualnych, które są bardziej odpowiednie dla aplikacji produkcyjnych, zobacz (Rozmiary maszyn wirtualnych) [virtual-machines-size-specs.md]. Aby uzyskać informacje o cenach maszyn wirtualnych, zobacz [Cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="dsv3-series"></a>Seria Dsv3

ACU: 160–190

Rozmiary serii Dsv3 są oparte na powitania 2.3 v4® GHz Intel XEON E5-2673 procesora (Broadwell) i można osiągnąć wersji 3.5GHz z Intel Turbo zwiększanie wyniku technologii 2.0 i używać magazyn w warstwie premium. rozmiary serii Dsv3 Hello oferować połączenie vCPU, pamięci oraz magazyn tymczasowy dla większości obciążeń produkcyjnych.


| Rozmiar             | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standardowa_D2s_v3  | 2      | 8           | 16             | 4              | 4000 / 32 (50)                                                       | 3200 / 48                                | 2 / średnia                                   |
| Standardowa_D4s_v3  | 4      | 16          | 32             | 8              | 8000 / 64 (100)                                                      | 6400 / 96                                | 2 / średnia                                   |
| Standardowa_D8s_v3  | 8      | 32          | 64             | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / wysoka                                       |
| Standardowa_D16s_v3 | 16     | 64          | 128            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / wysoka                                       |


## <a name="dv3-series"></a>Seria Dv3

ACU: 160–190

Rozmiary serii Dv3 są oparte na powitania 2.3 v4® GHz Intel XEON E5-2673 procesora (Broadwell) i można osiągnąć wersji 3.5GHz z Intel Turbo zwiększanie wyniku technologii 2.0. rozmiary serii Dv3 Hello oferować połączenie vCPU, pamięci oraz magazyn tymczasowy dla większości obciążeń produkcyjnych.

Opłaty za magazyn dysków danych są naliczane oddzielnie od opłat za maszyny wirtualne. dyski magazynu premium toouse, użyj rozmiarów Dsv3 hello. Cennik Hello i metod rozliczeń rozmiarów Dsv3 są hello taki sam jak Dv3 serii. 


| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba kart sieciowych / przepustowość sieci |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standardowa_D2_v3  | 2         | 8           | 50             | 4              | 3000/46/23                                               | 2 / średnia                 |
| Standardowa_D4_v3  | 4         | 16          | 100            | 8              | 6000/93/46                                               | 2 / średnia                 |
| Standardowa_D8_v3  | 8         | 32          | 200            | 16             | 12000/187/93                                             | 4 / wysoka                     |
| Standardowa_D16_v3 | 16        | 64          | 400            | 32             | 24000/375/187                                            | 8 / wysoka                     |


## <a name="dsv2-series"></a>Seria DSv2

ACU: 210–250

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS1_v2 |1 |3,5 |7 |2 |4000 / 32 (43) |3200 / 48 |2 / 750 |
| Standardowa_DS2_v2 |2 |7 |14 |4 |8000 / 64 (86) |6400 / 96 |2 / 1500 |
| Standardowa_DS3_v2 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 192 |4 / 3000 |
| Standardowa_DS4_v2 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 384 |8 / 6000 |
| Standardowa_DS5_v2 |16 |56 |112 |32 |64 000 / 512 (688) |51 200 / 768 |8 / 6000–12 000 &#8224;|



## <a name="dv2-series"></a>Seria Dv2

ACU: 210–250

| Rozmiar              | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D1_v2    | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standardowa_D2_v2    | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standardowa_D3_v2    | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standardowa_D4_v2    | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standardowa_D5_v2    | 16        | 56          | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000–12 000 &#8224;          |


<br>

## <a name="ds-series"></a>Seria DS

ACU: 160

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS1 |1 |3,5 |7 |2 |4000 / 32 (43) |3200 / 32 |2 / 500 |
| Standardowa_DS2 |2 |7 |14 |4 |8000 / 64 (86) |6400 / 64 |2 / 1000 |
| Standardowa_DS3 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 128 |4 / 2000 |
| Standardowa_DS4 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 256 |8 / 4000 |

<br>

## <a name="d-series"></a>Seria D 

ACU: 160

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D1  | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 500                 |
| Standardowa_D2  | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1000                     |
| Standardowa_D3  | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2000                     |
| Standardowa_D4  | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4000                     |

<br>


## <a name="av2-series"></a>Seria Av2

ACU: 100

| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) | 
|-----------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_A1_v2  | 1         | 2           | 10             | 1000 / 20 / 10                                           | 2 / 2 x 500               | 2 / 250                 |
| Standardowa_A2_v2  | 2         | 4           | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standardowa_A4_v2  | 4         | 8           | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1000                     |
| Standardowa_A8_v2  | 8         | 16          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2000                     |
| Standardowa_A2m_v2 | 2         | 16          | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standardowa_A4m_v2 | 4         | 32          | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1000                     |
| Standardowa_A8m_v2 | 8         | 64          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2000                     |

<br>

## <a name="a-series"></a>Seria A

ACU: 50–100

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (HDD): GiB | Maks. liczba dysków danych | Maksymalna przepływność dysków danych: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s)  |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_A0* |1 |0,768 |20 |1 |1 x 500 |2 / 100 |
| Standardowa_A1 |1 |1,75 |70 |2 |2 x 500 |2 / 500  |
| Standardowa_A2 |2 |3,5 |135 |4 |4 x 500 |2 / 500 |
| Standardowa_A3 |4 |7 |285 |8 |8 x 500 |2 / 1000 |
| Standardowa_A4 |8 |14 |605 |16 |16 x 500 |4 / 2000 |
| Standardowa_A5 |2 |14 |135 |4 |4 x 500 |2 / 500 |
| Standardowa_A6 |4 |28 |285 |8 |8 x 500 |2 / 1000 |
| Standardowa_A7 |8 |56 |605 |16 |16 x 500 |4 / 2000 |
<br>

* hello A0 rozmiar jest nadmiernie subskrybowanego na sprzęcie fizycznym hello. Dla tego określonego rozmiaru tylko wtedy innych wdrożeń klienta może mieć wpływ na wydajność hello obciążenia uruchomione. Hello względną wydajność opisanym poniżej jako jej linia bazowa hello oczekiwano, podmiotu tooan przybliżonej zmienność 15 procent.

### <a name="standard-a0---a4-using-cli-and-powershell"></a>Standardowa_A0–A4 w przypadku używania interfejsu wiersza polecenia i programu PowerShell
W hello klasycznego modelu wdrażania niektóre nazwy rozmiar maszyny Wirtualnej są nieco inne interfejsu wiersza polecenia i programu PowerShell:

* Standardowa_A0 = Bardzo mała 
* Standardowa_A1 = Mała
* Standardowa_A2 = Średnia
* Standardowa_A3 = Duża
* Standardowa_A4 = Bardzo duża

## <a name="basic-a"></a>Podstawowa A

|Rozmiar — rozmiar\nazwa | Procesor wirtualny |Memory (Pamięć)|Karty sieciowe (maks.)|Maksymalny rozmiar dysku tymczasowego |Maksymalnie z dyski danych 1023 GB każdy)|Maksymalnie z liczba operacji we/wy na sekundę (300 na dysk)|
|---|---|---|---|---|---|---|
|A0\Podstawowa_A0|1|768 MB|2| 20 GB|1|1x300|
|A1\Podstawowa_A1|1|1,75 GB|2| 40 GB |2|2x300|
|A2\Podstawowa_A2|2|3,5 GB|2| 60 GB|4|4x300|
|A3\Podstawowa_A3|4|7 GB|2| 120 GB |8|8x300|
|A4\Podstawowa_A4|8|14 GB|2| 240 GB |16|16x300|
