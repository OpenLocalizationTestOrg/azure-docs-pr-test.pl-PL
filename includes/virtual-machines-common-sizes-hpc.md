<!-- A-series - compute-intensive instances, H-series -->

Hello rozmiary A8 A11 i H-series są również znane jako *wystąpień obliczeniowych*. Hello sprzęt, który uruchamia te rozmiary został zaprojektowany i zoptymalizowany pod kątem obliczeniowych i aplikacji, modelowania i symulacje klastra aplikacji obciążenie sieci, w tym obliczeniowe wysokiej wydajności (HPC). Witaj serii A8 A11 korzysta Intel Xeon E5-2670 @ 2.6 GHZ, a hello H-series v3 Intel Xeon E5-2667 @ 3,2 GHz. 

Maszyny wirtualne platformy Azure H-series są hello następnej generacji wysokiej wydajności obliczeniowych, że maszyny wirtualne celem potrzeb obliczeniową górną granicę, jak molekularnej modelowania i obliczeniową dynamics płynu. Te 8 do 16 vCPU maszyny wirtualne są oparte na technologii procesora hello V3 2667 Haswell E5 Intel oferujący funkcje DDR4 pamięci i tymczasowego magazynu opartego na dysk SSD. 

Ponadto toohello znacznej moc procesora CPU, hello H-series oferuje różnych opcji małe opóźnienia sieci RDMA przy użyciu FDR InfiniBand i kilka konfiguracji toosupport pamięci znacznym obliczeniową wymagania dotyczące pamięci.



## <a name="h-series"></a>Seria H

ACU: 290–300

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność dysków: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standardowa_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standardowa_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standardowa_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standardowa_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standardowa_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*W przypadku aplikacji MPI dedykowana sieć zaplecza RDMA jest zapewniana przez sieć FDR InfiniBand, która gwarantuje ultraniskie opóźnienia i wysoką przepustowość.

<br>



## <a name="a-series---compute-intensive-instances"></a>Seria A — wystąpienia intensywnie korzystające z mocy obliczeniowej

ACU: 225

| Rozmiar | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (HDD): GiB | Maks. liczba dysków danych | Maksymalna przepływność dysków danych: liczba operacji we/wy na sekundę | Maksymalna liczba kart sieciowych|
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_A8* |8 |56 |382 |16 |16 x 500 |2 |
| Standardowa_A9* |16 |112 |382 |16 |16 x 500 |4 |
| Standardowa_A10 |8 |56 |382 |16 |16 x 500 |2  |
| Standardowa_A11 |16 |112 |382 |16 |16 x 500 |4 |

*W przypadku aplikacji MPI dedykowana sieć zaplecza RDMA jest zapewniana przez sieć FDR InfiniBand, która gwarantuje ultraniskie opóźnienia i wysoką przepustowość.

<br>



