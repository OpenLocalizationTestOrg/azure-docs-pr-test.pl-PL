
Zoptymalizowanych pod kątem pamięci oferta rozmiary maszyny Wirtualnej wysokiego współczynnika pamięci do Procesora, który jest wspaniała relacyjnej bazy danych serwerów, pamięci podręcznych średnich i dużych i analizy w pamięci. Ten artykuł zawiera informacje o liczbie Vcpu, dysków z danymi i karty sieciowe, a także przepustowości przepływności i sieć magazynu dla każdego rozmiaru w tej metodzie grupowania. 

* M-Series oferuje największa liczba vCPU (maksymalnie 128 Vcpu) i pamięci największego (TiB do 3.8) żadnej maszyny Wirtualnej w chmurze.  Jest to idealne rozwiązanie dla bardzo dużych baz danych lub innych aplikacji, które korzystają z dużej liczby procesorów wirtualnych vCPU i dużych ilości pamięci.

* Serie Dv2, D, G i ich odpowiedniki DS/GS są idealne dla aplikacji wymagających szybszych procesorów wirtualnych vCPU, magazynów tymczasowych o lepszej wydajności lub większych ilości pamięci.  Oferują one kombinację opcji o dużych możliwościach dla wielu aplikacji klasy korporacyjnej.

* Maszyny wirtualne serii D są zaprojektowane do uruchamiania aplikacji wymagających większej mocy obliczeniowej i wydajności dysków tymczasowych. Maszyny wirtualne serii D zapewniają szybsze procesory, większą ilość pamięci na procesor wirtualny vCPU i dyski półprzewodnikowe (SSD) dla magazynów tymczasowych. Szczegółowe informacje zawiera ogłoszenie [New D-Series Virtual Machine Sizes](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/) (Nowe rozmiary maszyn wirtualnych serii D) w blogu platformy Azure.

* Seria Dv2, kontynuacja oryginalnej serii D, jest wyposażona w procesor CPU o większych możliwościach. Procesor CPU serii Dv2 jest o około 35% szybszy niż procesor CPU serii D. Seria Dv2 jest oparta na procesorze najnowszej generacji Intel Xeon® E5-2673 v3 (Haswell) z zegarem 2,4 GHz, który dzięki technologii Intel Turbo Boost 2.0 może osiągnąć częstotliwość 3,1 GHz. Konfiguracje pamięci i dysków serii Dv2 są takie same jak w przypadku serii D.


## <a name="esv3-series-sup1sup"></a>Seria Esv3 <sup>1</sup>

ACU: 160–190

Wystąpienia serii ESv3 są oparte na procesorach Intel XEON® E5-2673 v4 (Broadwell) z zegarem 2,3 GHz, które dzięki technologii Intel Turbo Boost 2.0 mogą osiągnąć częstotliwość 3,5 GHz i korzystają z magazynu Premium Storage. Wystąpienia serii Ev3 są idealne dla aplikacji korporacyjnych intensywnie korzystających z pamięci.


| Rozmiar             | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standardowa_E2s_v3  | 2      | 16          | 32             | 4              | 4000 / 32 (50)                                                       | 3200 / 48                                | 2 / 1,000                                   |
| Standardowa_E4s_v3  | 4      | 32          | 64             | 8              | 8000 / 64 (100)                                                      | 6400 / 96                                | 2 / 2,000                                   |
| Standardowa_E8s_v3  | 8      | 64          | 128            | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / 4,000                                       |
| Standardowa_E16s_v3 | 16     | 128         | 256            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / 8,000                                       |
| Standard_E32s_v3 <sup>2</sup> | 32     | 256         | 512            | 32             | 64 000 / 512 (800)                                                    | 51 200 / 768                              | 8 / 16,000                             |
| Standard_E64s_v3 <sup>2</sup> | 64     | 432         | 864            | 32             | 128 000/1024 (1600)                                                   | 80 000 / 1200                             | 8 / 30,000                             |

<sup>1</sup> Esv3 serii maszyny Wirtualnej funkcji technologią Intel® Hyper-Threading <sup>2</sup> ograniczone dostępne rozmiary core 

## <a name="ev3-series-sup1sup"></a>Seria Ev3 <sup>1</sup>

ACU: 160–190 

Wystąpienia serii Ev3 są oparte na procesorach Intel XEON® E5-2673 v4 (Broadwell) 2,3 GHz i technologią Intel Turbo Boost 2.0, dzięki której mogą osiągnąć częstotliwość 3,5 GHz. Wystąpienia serii Ev3 są idealne dla aplikacji korporacyjnych intensywnie korzystających z pamięci.

Opłaty za magazyn dysków danych są naliczane oddzielnie od opłat za maszyny wirtualne. Aby korzystać z dysków magazynu Premium Storage, użyj rozmiarów ESv3. Liczniki cen i rozliczeń dla rozmiarów ESv3 są takie same jak dla serii Ev3. 


| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba kart sieciowych / przepustowość sieci |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standardowa_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2 / 1,000                 |
| Standardowa_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2 / 2,000                 |
| Standardowa_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4 / 4,000                     |
| Standardowa_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8 / 8,000                     |
| Standardowa_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8 / 16,000                 |
| Standardowa_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8 / 30,000           |

<sup>1</sup> serii Ev3 maszyny Wirtualnej funkcji technologią Intel® Hyper-Threading

## <a name="m-series-sup1sup"></a>M-series <sup>1</sup>

ACU: 160–180

| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64s  | 64   | 1024        | 2048           | 64             | 80 000 / 800 (6348)       | 40 000 / 1000                            | 8 / 16 000          |
| Standardowa_M64ms  | 64   | 1792        | 2048           | 64             | 80 000 / 800 (6348)       | 40 000 / 1000                            | 8 / 16 000          |
| Standard_M128s <sup>2. 3</sup> | 128  | 2048        | 4096           | 64             | 160 000 / 1 600 (12 696) | 80 000 / 2000                            | 8 / 30000          |
| Standard_M128ms <sup>2. 3</sup> | 128  | 3800        | 4096           | 64             | 160 000 / 1 600 (12 696) | 80 000 / 2000                            | 8 / 30000          |

<sup>1</sup> funkcja wirtualna serii M technologią Intel® Hyper-Threading

<sup>2</sup> więcej niż 64 vCPU, muszą mieć jedną z tych gościa obsługiwanych systemów operacyjnych: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 z dodatkiem SP2 i Red Hat Enterprise Linux, CentOS 7.3 lub Oracle 7.3 Linux z LIS 4.2.1 

<sup>3</sup> ograniczone dostępne rozmiary core.

<br>

## <a name="gs-series-sup1sup"></a>GS-series <sup>1</sup>

ACU: 180–240

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|---|---|---|---|---|---|---|---|
| Standardowa_GS1 |2 |28 |56 |8 |10 000 / 100 (264) |5000 / 125 |2 / 2000 |
| Standardowa_GS2 |4 |56 |112 |16 |20 000 / 200 (528) |10 000 / 250 |2 / 4000 |
| Standardowa_GS3 |8 |112 |224 |32 |40 000 / 400 (1056) |20 000 / 500 |4 / 8000 |
| Standard_GS4 <sup>3</sup> |16 |224 |448 |64 |80 000 / 800 (2112) |40 000 / 1000 |8 / 16 000 |
| Standard_GS5 <sup>2, 3</sup> |32 |448 |896 |64 |160 000 / 1600 (4224) |80 000 / 2000 |8 / 20 000 |

<sup>1</sup> przepustowość maksymalna liczba dyskowych operacji to (IOPS lub MB/s) możliwe z serii GS maszyny Wirtualnej może być ograniczony przez kod, rozmiar i rozkładanie dołączone dyski. Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/virtual-machines/windows/premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure). 

<sup>2</sup> wystąpienia jest izolowana sprzętu przeznaczonego do jednego odbiorcy.

<sup>3</sup> ograniczone dostępne rozmiary core 

<br>

## <a name="g-series"></a>Seria G

ACU: 180–240

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 8 / 8 x 500                       | 2 / 2000                     |
| Standardowa_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 16 / 16 x 500                       | 2 / 4000                     |
| Standardowa_G3  | 8         | 112         | 1536          | 24000 / 375 / 187                                        | 32 / 32 x 500                     | 4 / 8000                |
| Standardowa_G4  | 16        | 224         | 3072          | 48000 / 750 / 375                                        | 64 / 64 x 500                     | 8 / 16 000          |
| Standard_G5 <sup>1</sup> | 32        | 448         | 6144          | 96000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20 000           |

<sup>1</sup> wystąpienia jest izolowana sprzętu przeznaczonego do jednego odbiorcy.
<br>


## <a name="dsv2-series-sup1sup"></a>Seria DSv2 <sup>1</sup>

ACU: 210–250

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS11_v2 |2 |14 |28 |8 |8000 / 64 (72) |6400 / 96 |2 / 1500 |
| Standardowa_DS12_v2 |4 |28 |56 |16 |16 000 / 128 (144) |12 800 / 192 |4 / 3000 |
| Standardowa_DS13_v2 |8 |56 |112 |32 |32 000 / 256 (288) |25 600 / 384 |8 / 6000 |
| Standardowa_DS14_v2 |16 |112 |224 |64 |64 000 / 512 (576) |51 200 / 768 |8 / 12000 |
| Standard_DS15_v2 <sup>2</sup> |20 |140 |280 |64 |80 000 / 640 (720) |64 000 / 960 |8 / 25000 <sup>3</sup>

<sup>1</sup> przepustowość maksymalna liczba dyskowych operacji to (IOPS lub MB/s) możliwe z serii DSv2 maszyny Wirtualnej może być ograniczony przez kod, rozmiar i rozkładanie dołączone dyski.  Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/virtual-machines/windows/premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure).

<sup>2</sup> wystąpienie jest izolowane węzła, który gwarantuje, że maszyna wirtualna jest tylko maszynę Wirtualną na węźle naszych Intel Haswell.

<sup>3</sup> 25000 MB/s z przyspieszonego w sieci.

<br>

## <a name="dv2-series"></a>Seria Dv2

ACU: 210–250

| Rozmiar              | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 8 / 8 x 500                         | 2 / 1500                     |
| Standardowa_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 16 / 16 x 500                         | 4 / 3000                     |
| Standardowa_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 32 / 32 x 500                       | 8 / 6000                     |
| Standardowa_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 64 / 64 x 500                       | 8 / 12000          |
| Standard_D15_v2 <sup>1</sup> | 20        | 140         | 1000          | 60000 / 937 / 468                                        | 64 / 64 x 500                       | 8 / 25000 <sup>2</sup> |

<sup>1</sup> wystąpienie jest izolowane węzła, który gwarantuje, że maszyna wirtualna jest tylko maszynę Wirtualną na węźle naszych Intel Haswell.

<sup>2</sup> 25000 MB/s z przyspieszonego w sieci.

<br>

## <a name="ds-series-sup1sup"></a>Serii DS <sup>1</sup>

ACU: 160

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS11 |2 |14 |28 |8 |8000 / 64 (72) |6400 / 64 |2 / 1000 |
| Standardowa_DS12 |4 |28 |56 |16 |16 000 / 128 (144) |12 800 / 128 |4 / 2000 |
| Standardowa_DS13 |8 |56 |112 |32 |32 000 / 256 (288) |25 600 / 256 |8 / 4000 |
| Standardowa_DS14 |16 |112 |224 |64 |64 000 / 512 (576) |51 200 / 512 |8 / 8000 |

<sup>1</sup> przepustowość maksymalna liczba dyskowych operacji to (IOPS lub MB/s), możliwe z serii DS maszyny Wirtualnej może być ograniczony przez kod, rozmiar i rozkładanie dołączone dyski.  Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/virtual-machines/windows/premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure).


## <a name="d-series"></a>Seria D

ACU: 160

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych / oczekiwano przepustowości sieci (MB/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 8 / 8 x 500                         | 2 / 1000                     |
| Standardowa_D12 | 4         | 28          | 200            | 12000 / 187 / 93                                         | 16 / 16 x 500                         | 4 / 2000                     |
| Standardowa_D13 | 8         | 56          | 400            | 24000 / 375 / 187                                        | 32 / 32 x 500                       | 8 / 4000                     |
| Standardowa_D14 | 16        | 112         | 800            | 48000 / 750 / 375                                        | 64 / 64 x 500                       | 8 / 8000                |

<br>

