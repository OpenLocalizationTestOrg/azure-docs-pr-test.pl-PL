
* Witaj serii M oferuje hello największa liczba vCPU (up too128 Vcpu) i największy pamięci (w górę too2.0 TiB) żadnej maszyny Wirtualnej w chmurze hello.  Jest to idealne rozwiązanie dla bardzo dużych baz danych lub innych aplikacji, które korzystają z dużej liczby procesorów wirtualnych vCPU i dużych ilości pamięci.

* Dv2 serii, D-series, G serii i odpowiedniki DS/GS hello idealnie nadają się do aplikacji, które popytu szybsze Vcpu, lepszą wydajność magazyn tymczasowy, lub mieć wyższe wymagania pamięci.  Oferują one kombinację opcji o dużych możliwościach dla wielu aplikacji klasy korporacyjnej.

* D-series maszyny wirtualne są zaprojektowane toorun aplikacji, które wymaga wyższej moc obliczeniową i wydajność dysku tymczasowym. Maszyny wirtualne serii D zapewniają szybsze procesory, większą ilość pamięci na procesor wirtualny vCPU i dyski półprzewodnikowe (SSD) dla magazynów tymczasowych. Aby uzyskać więcej informacji, zobacz anons hello na powitania Azure blog [nowe rozmiary maszyny wirtualnej D-Series](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Dv2-series, finałowa toohello oryginalnego D-series, funkcje większe możliwości procesora CPU. Hello serii Dv2 Procesora CPU D-series jest około 35% szybciej niż hello. Jest on oparty na powitania najnowszej generacji 2.4 v3® GHz Intel Xeon E5-2673 procesora (Haswell) i z hello Intel Turbo zwiększanie wyniku technologii 2.0, może przejść w górę too3.1 GHz. ma Hello serii Dv2 hello takie same konfiguracje pamięci i dysku, ponieważ hello D-series.


## <a name="esv3-series"></a>Seria ESv3

ACU: 160–190

Seria ESv3 wystąpienia są oparte na powitania 2.3 v4® GHz Intel XEON E5-2673 procesora (Broadwell) i można osiągnąć wersji 3.5GHz z Intel Turbo zwiększanie wyniku technologii 2.0 i używać magazyn w warstwie premium. Wystąpienia serii Ev3 są idealne dla aplikacji korporacyjnych intensywnie korzystających z pamięci.


| Rozmiar             | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standardowa_E2s_v3  | 2      | 16          | 32             | 4              | 4000 / 32 (50)                                                       | 3200 / 48                                | 2 / średnia                                   |
| Standardowa_E4s_v3  | 4      | 32          | 64             | 8              | 8000 / 64 (100)                                                      | 6400 / 96                                | 2 / średnia                                   |
| Standardowa_E8s_v3  | 8      | 64          | 128            | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / wysoka                                       |
| Standardowa_E16s_v3 | 16     | 128         | 256            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / wysoka                                       |
| Standardowa_E32s_v3 | 32     | 256         | 512            | 32             | 64 000 / 512 (800)                                                    | 51 200 / 768                              | 8 / ekstremalnie wysoka                             |
| Standardowa_E64s_v3 | 64     | 432         | 864            | 32             | 128 000/1024 (1600)                                                   | 80 000 / 1200                             | 8 / ekstremalnie wysoka                             |



## <a name="ev3-series"></a>Seria Ev3

ACU: 160–190 

Seria Ev3 wystąpienia są oparte na powitania 2.3 v4® GHz Intel XEON E5-2673 procesora (Broadwell) i można osiągnąć wersji 3.5GHz z Intel Turbo zwiększanie wyniku technologii 2.0. Wystąpienia serii Ev3 są idealne dla aplikacji korporacyjnych intensywnie korzystających z pamięci.

Opłaty za magazyn dysków danych są naliczane oddzielnie od opłat za maszyny wirtualne. dyski magazynu premium toouse, użyj rozmiarów ESv3 hello. Cennik Hello i metod rozliczeń rozmiarów ESv3 są hello taki sam jak Ev3 serii. 


| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba kart sieciowych / przepustowość sieci |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standardowa_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2 / średnia                 |
| Standardowa_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2 / średnia                 |
| Standardowa_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4 / wysoka                     |
| Standardowa_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8 / wysoka                     |
| Standardowa_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8 / ekstremalnie wysoka           |
| Standardowa_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8 / ekstremalnie wysoka           |


## <a name="m-series"></a>Seria M*

ACU: 160–180

| Rozmiar            | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standardowa_M64ms  | 64   | 1792        | 2048           | 32             | 80 000 / 800 (6348)       | 40 000 / 1000                            | 8 / 16 000          |
| Standardowa_M128s** | 128  | 2048        | 4096           | 64             | 160 000 / 1 600 (12 696) | 80 000 / 2000                            | 8 / 25 000          |



* Maszyny wirtualne serii M korzystają z technologii hiperwątkowości Intel®

** Więcej niż 64 procesory wirtualne wymagają jednego z następujących systemów operacyjnych gościa: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 z dodatkiem SP2 i Red Hat Enterprise Linux lub CentOS 7.3 z usługami LIS 4.2.1 

<br>

## <a name="gs-series"></a>Seria GS*

ACU: 180–240

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_GS1 |2 |28 |56 |4 |10 000 / 100 (264) |5000 / 125 |2 / 2000 |
| Standardowa_GS2 |4 |56 |112 |8 |20 000 / 200 (528) |10 000 / 250 |2 / 4000 |
| Standardowa_GS3 |8 |112 |224 |16 |40 000 / 400 (1056) |20 000 / 500 |4 / 8000 |
| Standardowa_GS4 |16 |224 |448 |32 |80 000 / 800 (2112) |40 000 / 1000 |8 / 6000–16 000 &#8224; |
| Standardowa_GS5** |32 |448 |896 |64 |160 000 / 1600 (4224) |80 000 / 2000 |8 / 20 000 |

* hello maksymalną przepływność dysku (IOPS lub MB/s) przy użyciu serii GS maszyny Wirtualnej może być ograniczony przez hello liczba, rozmiar i rozkładanie hello dołączone dyski. Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure). 

** Wystąpienie jest izolowane toohardware dedykowanych tooa jednego odbiorcy.


<br>

## <a name="g-series"></a>Seria G

ACU: 180–240

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4 / 4 x 500                       | 2 / 2000                     |
| Standardowa_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 8 / 8 x 500                       | 2 / 4000                     |
| Standardowa_G3  | 8         | 112         | 1536          | 24000 / 375 / 187                                        | 16 / 16 x 500                     | 4 / 8000                |
| Standardowa_G4  | 16        | 224         | 3072          | 48000 / 750 / 375                                        | 32 / 32 x 500                     | 8 / 6000–16 000 &#8224;          |
| Standardowa_G5* | 32        | 448         | 6144          | 96000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20 000           |

* Wystąpienie jest izolowane toohardware dedykowanych tooa jednego odbiorcy.
<br>


## <a name="dsv2-series"></a>Seria DSv2*

ACU: 210–250

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS11_v2 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 96 |2 / 1500 |
| Standardowa_DS12_v2 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 192 |4 / 3000 |
| Standardowa_DS13_v2 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 384 |8 / 6000 |
| Standardowa_DS14_v2 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 768 |8 / 6000–12 000 &#8224; |
| Standardowa_DS15_v2** |20 |140 |280 |40 |80 000 / 640 (720) |64 000 / 960 |8 / 20 000***

* hello maksymalną przepływność dysku (IOPS lub MB/s) przy użyciu serii DSv2 maszyny Wirtualnej może być ograniczony przez hello liczba, rozmiar i rozkładanie hello dołączone dyski.  Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure).

** Wystąpienia jest izolowane węzeł czy gwarantuje maszyny Wirtualnej jest hello tylko maszyny Wirtualnej w węźle naszych Intel Haswell.

***25 000 Mb/s z przyspieszoną siecią.

<br>

## <a name="dv2-series"></a>Seria Dv2

ACU: 210–250

| Rozmiar              | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standardowa_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standardowa_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standardowa_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000–12 000 &#8224;          |
| Standardowa_D15_v2* | 20        | 140         | 1000          | 60000 / 937 / 468                                        | 40 / 40 x 500                       | 8 / 20 000** |

* Wystąpienia jest izolowane węzeł czy gwarantuje maszyny Wirtualnej jest hello tylko maszyny Wirtualnej w węźle naszych Intel Haswell.

** 25 000 Mb/s z przyspieszoną siecią.

<br>

## <a name="ds-series"></a>Seria DS*

ACU: 160

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standardowa_DS11 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 64 |2 / 1000 |
| Standardowa_DS12 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 128 |4 / 2000 |
| Standardowa_DS13 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 256 |8 / 4000 |
| Standardowa_DS14 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 512 |8 / 6000–8000 &#8224; |

* hello maksymalną przepływność dysku (IOPS lub MB/s) z serii DS maszyny Wirtualnej może być ograniczony przez hello liczba, rozmiar i rozkładanie hello dołączone dyski.  Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure).


## <a name="d-series"></a>Seria D

ACU: 160

| Rozmiar         | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maksymalna przepływność magazynu tymczasowego: operacje we/wy na sek. / odczyt MB/s / zapis MB/s | Maksymalna liczba dysków danych / przepływność: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standardowa_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1000                     |
| Standardowa_D12 | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2000                     |
| Standardowa_D13 | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4000                     |
| Standardowa_D14 | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000–8000 &#8224;                |

<br>

