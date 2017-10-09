Fabryka danych jest usługą wielodostępne, która ma hello następujące domyślne limity w miejscu toomake się, że subskrypcjami klientów są chronione przez obciążeń. Wiele hello limity można łatwo wygenerowany dla Twojej subskrypcji się maksymalny limit toohello za pośrednictwem pracowników pomocy technicznej.

| **Zasób** | **Limit domyślny** | **Limit maksymalny** |
| --- | --- | --- |
| fabryki danych w subskrypcji platformy Azure |50 |[Kontakt z pomocą techniczną](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| potoki w fabryce danych |2500 |[Kontakt z pomocą techniczną](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| zestawy danych w fabryce danych |5000 |[Kontakt z pomocą techniczną](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Współbieżne wycinki dla zestawu danych |10 |10 |
| bajtów dla każdego obiektu dla potoku obiektów <sup>1</sup> |200 KB |200 KB |
| Liczba bajtów na obiekt zestawu danych i obiektów powiązanych z <sup>1</sup> |100 KB |2000 KB |
| Rdzeni na żądanie klastra usługi HDInsight w ramach subskrypcji <sup>2</sup> |60 |[Kontakt z pomocą techniczną](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Jednostka przepływu danych w chmurze <sup>3</sup> |32 |[Kontakt z pomocą techniczną](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Liczba uruchomień działania potoku ponownych prób |1000 |MaxInt (32-bitowe) |

<sup>1</sup> potoku, zestawu danych i obiektów powiązanych z reprezentują logiczne grupowanie obciążenie. Limity dla tych obiektów nie odnoszą się tooamount danych można przenieść i przetwarzać z hello usługi fabryka danych Azure. Fabryka danych jest zaprojektowana tooscale toohandle petabajtów danych.

<sup>2</sup> rdzeni na żądanie usługi HDInsight są przydzielane poza hello subskrypcji, która zawiera hello fabryki danych. W związku z tym hello przekracza limit jest hello fabryki danych wymuszone limit podstawowych rdzeni HDInsight na żądanie i różni się od limit rdzeni hello skojarzone z subskrypcją platformy Azure.

<sup>3</sup> jednostki przepływu danych w chmurze (DMU) jest używany w operacji kopiowania w chmurze z chmurą. Stanowi ona miarę reprezentujący hello zasilania (kombinacja Procesora, pamięci i alokacji zasobów sieciowych) z pojedynczą jednostkę w fabryce danych. Wyższej przepustowości kopii można osiągnąć dzięki wykorzystaniu więcej DMUs w niektórych scenariuszach. Odwołuje się zbyt[jednostki przepływu danych w chmurze](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) sekcji Szczegóły.

| **Zasób** | **Dolny limit domyślny** | **Minimalny limit** |
| --- | --- | --- |
| Interwał harmonogramu |15 minut |15 minut |
| Interwał między ponownymi próbami |1 sekunda |1 sekunda |
| Spróbuj ponownie wartość limitu czasu |1 sekunda |1 sekunda |

### <a name="web-service-call-limits"></a>Ograniczenia wywołania usługi sieci Web
Usługa Azure Resource Manager ma limity dla interfejsu API. Możesz wprowadzić wywołań interfejsu API z szybkością w hello [ogranicza interfejsu API usługi Azure Resource Manager](../articles/azure-subscription-service-limits.md#resource-group-limits).
