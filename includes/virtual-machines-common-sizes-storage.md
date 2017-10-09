
Witaj serii Ls jest zoptymalizowana pod kątem obciążeń, które wymagają magazyn tymczasowy małymi opóźnieniami, takich jak bazy danych NoSQL Cloudera Cassandra, bazy danych MongoDB, w tym i Redis. zapewnia Hello serii Ls too32 Vcpu, przy użyciu hello [procesor Intel Xeon® E5 v3 rodziny](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). pobiera Hello serii Ls hello wydajności procesora CPU, jak hello GS-G-Series i wyposażony w 8 GiB pamięci dla vCPU.  

## <a name="ls-series"></a>Seria Ls

ACU: 180–240
 
| Rozmiar          | Procesor wirtualny | Pamięć: GiB | Magazyn tymczasowy (SSD): GiB | Maks. liczba dysków danych | Maksymalna przepływność magazynu buforowanego i tymczasowego: liczba operacji we/wy na sekundę / MB/s (rozmiar pamięci podręcznej w GiB) | Maksymalna przepływność niebuforowanych dysków: liczba operacji we/wy na sekundę / MB/s | Maksymalna liczba kart sieciowych/oczekiwana wydajność sieci (Mb/s) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standardowa_L4s  | 4    | 32   | 678   | 8              | ND / ND (0)          | 5000 / 125                               | 2 / 4000       | 
| Standardowa_L8s  | 8    | 64   | 1,388 | 16             | ND / ND (0)          | 10 000 / 250                              | 4 / 8000  | 
| Standardowa_L16s | 16   | 128  | 2,807 | 32             | ND / ND (0)          | 20 000 / 500                              | 8 / 6000–16 000 &#8224; | 
| Standardowa_L32s* | 32 | 256  | 5,630 | 64             | ND / ND (0)          | 40 000 / 1000                            | 8 / 20 000 | 
 

przepustowość maksymalna liczba dyskowych operacji Hello możliwe Ls serii maszyn wirtualnych może być ograniczone przez hello liczba, rozmiar i rozkładanie dowolnego dołączone dyski. Aby uzyskać szczegółowe informacje, zobacz [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure). 

* Wystąpienie jest izolowane toohardware dedykowanych tooa jednego odbiorcy.

