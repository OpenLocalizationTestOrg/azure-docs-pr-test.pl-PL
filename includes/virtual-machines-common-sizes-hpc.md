
Rozmiary A8–A11 i serii H są również nazywane *wystąpieniami intensywnie korzystającymi z mocy obliczeniowej*. Sprzęt, na którym działają te rozmiary maszyn wirtualnych, został zaprojektowany i zoptymalizowany pod kątem aplikacji intensywnie korzystających z mocy obliczeniowej i sieci, w tym aplikacji klastrów obliczeń o wysokiej wydajności, modelowania i symulacji. Maszyny wirtualne serii A8–A11 korzystają z procesorów Intel Xeon E5-2670 o częstotliwości 2,6 GHz, a seria H korzysta z procesorów Intel Xeon E5-2667 v3 o częstotliwości 3,2 GHz.  Ten artykuł zawiera informacje o liczbie Vcpu, dysków z danymi i karty sieciowe, a także przepustowości przepływności i sieć magazynu dla każdego rozmiaru w tej metodzie grupowania. 

Maszyny wirtualne serii H platformy Azure to następna generacja maszyn wirtualnych o wysokiej wydajności obliczeniowej, które idealnie sprawdzają się w przypadku najwyższych potrzeb obliczeniowych, na przykład w modelowaniu molekularnym i analizach obliczeniowych dynamiki płynów. Te 8 do 16 vCPU maszyn wirtualnych są tworzone na Intel 2667 Haswell E5 V3 procesora technologii typu DDR4 pamięci i magazyn tymczasowy na dyskach SSD. 

Seria H oferuje, obok znacznej mocy procesora CPU, różnorodne opcje dla sieci obsługujących technologię RDMA i niskie opóźnienia, korzystając z sieci InfiniBand o przepustowości FDR wraz z kilkoma konfiguracjami pamięci do obsługi obliczeń wymagających znacznego wykorzystania pamięci.



## <a name="h-series"></a>Seria H

ACU: 290–300

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność dysków: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_H8 |8 |56 |1000 |32 |32 x 500 |2  |
| Standardowa_H16 |16 |112 |2000 |64 |64 x 500 |4 |
| Standardowa_H8m |8 |112 |1000 |32 |32 x 500 |2  |
| Standardowa_H16m |16 |224 |2000 |64 |64 x 500 |4  |
| Warstwie standardowa_h16r <sup>1</sup> |16 |112 |2000 |64 |64 x 500 |4  |
| Warstwie standardowa_h16mr <sup>1</sup> |16 |224 |2000 |64 |64 x 500 |4 |

<sup>1</sup> dla aplikacji MPI dedykowanej sieci wewnętrznej bazy danych RDMA jest włączana przez FDR InfiniBand sieci, co zapewnia bardzo min. opóźnienie i wysokiej przepustowości.

<br>



## <a name="a-series---compute-intensive-instances"></a>Seria A — wystąpienia intensywnie korzystające z mocy obliczeniowej

ACU: 225

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (HDD): GiB | Maks. liczba dysków danych | Maksymalna przepływność dysków danych: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8 <sup>1</sup> |8 |56 |382 |32 |32 x 500 |2 |
| Standard_A9 <sup>1</sup> |16 |112 |382 |64 |64 x 500 |4 |
| Standardowa_A10 |8 |56 |382 |32 |32 x 500 |2  |
| Standardowa_A11 |16 |112 |382 |64 |64 x 500 |4 |

<sup>1</sup>dla aplikacji MPI dedykowanej sieci wewnętrznej bazy danych RDMA jest włączana przez FDR InfiniBand sieci, co zapewnia bardzo min. opóźnienie i wysokiej przepustowości.

<br>



