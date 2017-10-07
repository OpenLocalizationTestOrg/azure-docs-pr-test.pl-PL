---
title: "aaaDesign i wdrożenie Oracle bazy danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Projektowania i implementacji bazy danych programu Oracle w środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Projektowania i implementacji bazy danych programu Oracle na platformie Azure

## <a name="assumptions"></a>Wartości domyślne

- Planowane jest toomigrate z tooAzure lokalnej bazy danych Oracle.
- Masz zrozumienia hello różnych metryk w raportach Oracle AWR.
- Możesz wiedzę na temat linii bazowej wydajności aplikacji oraz wykorzystania platformy.

## <a name="goals"></a>Cele

- Zrozumienie sposobu toooptimize wdrożenia programu Oracle na platformie Azure.
- Poznaj opcje dla bazy danych Oracle w środowisku Azure dostrajania wydajności.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Witaj różnice między lokalnymi i Azure implementacji 

Poniżej przedstawiono niektóre istotne tookeep rzeczy pamiętać podczas migracji lokalnych tooAzure aplikacji. 

Jedną istotną różnicą jest to, że w implementacji platformy Azure, zasobów, takich jak maszyn wirtualnych, dysków i sieci wirtualne są współużytkowane przez innych klientów. Ponadto zasobów może być ograniczony na podstawie wymagań hello. Zamiast koncentrujących się na temat niepowodzenia (MTBF), Azure więcej koncentruje się na pozostałych hello awarii (MTTR).

Witaj poniższej tabeli przedstawiono niektóre hello różnic między implementacją lokalną i Azure implementacji bazy danych programu Oracle.

> 
> |  | **Implementacja lokalna** | **Implementacja Azure** |
> | --- | --- | --- |
> | **Sieć** |LAN/WAN  |SDN (technologia Sdn)|
> | **Grupy zabezpieczeń** |Ograniczenia adresu IP i portu narzędzi |[Grupy zabezpieczeń sieci (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Odporność** |MTBF (Średni czas między awariami) |MTTR (toorecovery średniego czasu)|
> | **Planowana konserwacja** |Stosowanie poprawek do uaktualnienia|[Zestawy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (poprawki/uaktualniania zarządzane przez usługę Azure) |
> | **Zasób** |Dedykowany  |Współużytkowane z innymi klientami|
> | **Regiony** |Centra danych |[Pary regionu](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Storage** |Dyski fizyczne/w sieci SAN |[Zarządzane Azure magazynu](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Skalowanie** |Skalowanie w pionie |Skalowanie w poziomie|


### <a name="requirements"></a>Wymagania

- Określenie hello stopy rozmiaru i wzrostu bazy danych.
- Ustal wymagania dotyczące IOPS hello, które można oszacować na podstawie raportów Oracle AWR lub innych narzędzi do monitorowania sieci.

## <a name="configuration-options"></a>Opcje konfiguracji

Istnieją cztery potencjalnych obszarów dostroić tooimprove wydajności w środowisku platformy Azure:

- Rozmiar maszyny wirtualnej
- Przepustowość sieci
- Typy dysków i konfiguracji
- Ustawienia pamięci podręcznej dysku

### <a name="generate-an-awr-report"></a>Generowanie raportu AWR

Jeśli korzystasz z istniejącej bazy danych programu Oracle i planowania toomigrate tooAzure, masz kilka opcji. Możesz uruchomić hello Oracle AWR raport tooget hello metryki (IOPS, MB/s, GiBs i tak dalej). Następnie wybierz powitalne maszyny Wirtualnej w oparciu metryki hello zebranych. Lub możesz skontaktować się infrastruktury zespołu tooget podobne informacje.

Należy rozważyć działania raportu AWR podczas obciążeń zarówno regularne i szczytu, więc możesz porównać. Na podstawie tych raportów, można rozmiar powitalne maszyn wirtualnych na podstawie obciążenia średni hello lub hello maksymalne obciążenie.

Poniżej przedstawiono przykładowy sposób toogenerate AWR raportu:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Kluczowych metryk

Poniżej przedstawiono metryki hello można uzyskać z hello AWR raportu:

- Całkowita liczba rdzeni
- Szybkość zegara Procesora
- Całkowitej ilości pamięci w GB
- Użycie procesora CPU
- Szczytowa szybkość transferu danych
- Liczba operacji We/Wy zmiany (odczyt/zapis)
- Wykonaj ponownie szybkość dziennika (MB/s)
- Przepustowość sieci
- Szybkość opóźnienia sieci (niski/wysoka)
- Rozmiar bazy danych w GB
- Bajty odebrane za pomocą programu SQL * Net z / tooclient

### <a name="virtual-machine-size"></a>Rozmiar maszyny wirtualnej

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Szacowanie rozmiaru maszyny Wirtualnej, na podstawie użycia Procesora, pamięci i operacji We/Wy z hello AWR raportu

Jedyną operacją, której może wyglądać na jest hello najwyższego pięć czasu pierwszego planu zdarzenia wskazujące, gdzie są hello wąskich gardeł systemu.

Na przykład w hello po diagramu, synchronizacji plików dziennika hello jest u góry hello. Wskazuje liczbę hello czeka przed hello LGWR zapisuje plik dziennika Powtórz toohello hello dziennika buforu. Te wyniki wskazują, że lepiej wykonuje magazynu lub dyski są wymagane. Ponadto hello diagram przedstawia również, hello liczba procesora CPU (rdzenie) oraz hello ilości pamięci.

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/cpu_memory_info.png)

Witaj Poniższy diagram przedstawia hello całkowita liczba operacji We/Wy odczytu i zapisu. Znaleziono 59 GB do odczytu i 247.3 zapisane w czasie hello hello raportu.

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Wybierz Maszynę wirtualną

Na podstawie hello informacji zebranych od hello AWR raportu, hello następnym krokiem jest toochoose maszyny Wirtualnej o rozmiarze podobne, który spełnia wymagania. Listę dostępnych maszyn wirtualnych można znaleźć w artykule hello [zoptymalizowanych pod kątem pamięci](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Dostosowywanie rozmiaru maszyny Wirtualnej hello oparte na powitania ACU podobne serią maszyny Wirtualnej

Po wybraniu hello maszyny Wirtualnej, należy zwrócić uwagę toohello ACU dla hello maszyny Wirtualnej. Można wybrać innej maszyny Wirtualnej, oparte na powitania wartość ACU, dostosowany do potrzeb. Aby uzyskać więcej informacji, zobacz [jednostki rozwiązań usługi obliczenia Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Zrzut ekranu przedstawiający stronę jednostki ACU hello](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Przepustowość sieci

powitania po diagram przedstawia hello relację między przepływności i IOPS:

![Zrzut ekranu przedstawiający przepływność](./media/oracle-design/throughput.png)

przepustowość sieci Całkowita Hello jest szacowana oparte na powitania następujących informacji:
- SQL * Net ruchu
- MB/s x wielu serwerów (strumienia wychodzącego takich jak Oracle Data Guard)
- Innych czynników, takich jak replikacja aplikacji

![Zrzut ekranu przedstawiający hello SQL * przepustowość sieci](./media/oracle-design/sqlnet_info.png)

Zgodnie z wymaganiami przepustowości sieci, istnieją różne typy bramy dla toochoose z. Obejmują one basic, VpnGw i usługa Azure ExpressRoute. Aby uzyskać więcej informacji, zobacz hello [bramy sieci VPN, na stronie dotyczącej cen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Zalecenia**

- Opóźnienie sieci jest wyższy porównaniu tooan lokalnego wdrożenia. Zmniejszenie sieci round rund może znacznie poprawić wydajność.
- aplikacje, które mają wysokie transakcji lub "chatty" aplikacji na powitania skonsolidować przechodzenia tooreduce tej samej maszyny wirtualnej.

### <a name="disk-types-and-configurations"></a>Typy dysków i konfiguracji

- *Domyślna dysków systemu operacyjnego*: tych typów dysków oferują trwałych danych i buforowania. Są zoptymalizowane pod kątem dostępu do systemu operacyjnego podczas uruchamiania, a nie są przeznaczone dla jednej transakcyjnej lub magazynu danych obciążenia (analitycznych).

- *Niezarządzane dysków*: Z tych typów dysku zarządzasz kont magazynu hello, w których są przechowywane pliki wirtualnego dysku twardego (VHD) hello, które odpowiadają tooyour dysków maszyny Wirtualnej. Pliki VHD są przechowywane jako stronicowe obiekty BLOB na kontach magazynu Azure.

- *Dyski zarządzane*: Azure zarządza kontami magazynu hello, których używasz dla dysków maszyny Wirtualnej. Należy określić typ dysku hello (standardowy lub premium) i hello rozmiar dysku hello, które są potrzebne. Azure tworzy i którymi zarządza hello dysku dla Ciebie.

- *Dyski magazynu Premium*: tych typów dysków są najbardziej odpowiednie dla obciążeń produkcyjnych. Dyski maszyny Wirtualnej obsługuje magazynu Premium, które można dołączyć toospecific rozmiar serii maszyn wirtualnych, takie jak seria DS, DSv2 i GS oraz F maszyn wirtualnych. dysku premium Hello jest dostarczany z różnych rozmiarach i można wybrać dyski od too4 32 GB, 096 GB. Rozmiar każdego dysku ma specyfikacjami wydajności. W zależności od wymagań aplikacji można dołączyć co najmniej jeden tooyour dysków maszyny Wirtualnej.

Po utworzeniu nowego dysku zarządzanego z hello portalu można wybrać hello **typ konta** dla typu hello dysku ma toouse. Należy pamiętać, że nie wszystkie dostępne dyski są wyświetlane w menu rozwijanym hello. Po wybraniu określonego rozmiaru maszyny Wirtualnej hello menu pokazuje tylko hello magazynu premium dostępne jednostki SKU, które są oparte na rozmiar tej maszyny Wirtualnej.

![Zrzut ekranu przedstawiający stronę dysków zarządzanych w hello](./media/oracle-design/premium_disk01.png)

Aby uzyskać więcej informacji, zobacz [zarządzanych dysków dla maszyny wirtualne i Magazyn w warstwie Premium wysokiej wydajności](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Po skonfigurowaniu magazynu na maszynie Wirtualnej można tooload testu hello dysków przed utworzeniem bazy danych. Znajomość szybkości operacji We/Wy hello pod względem zarówno opóźnienia i przepływności pozwalają określić, czy maszyny wirtualne hello obsługuje hello oczekiwano przepływności z obiektami docelowymi opóźnienia.

Istnieje wiele narzędzi dla aplikacji testów obciążenia, takich jak Oracle Orion, Sysbench i Fio.

Ponownie uruchom test obciążenia powitania po wdrożeniu bazy danych programu Oracle. Uruchom regularne i szczytowa obciążeń i hello Pokaż wyniki hello linii bazowej środowiska.

Może być większe znaczenie toosize hello magazynu na podstawie współczynnika IOPS hello zamiast hello rozmiar magazynu. Na przykład w razie potrzeby hello IOPS jest 5000, ale wymagane jest tylko 200 GB można nadal otrzymać hello P30 klasy premium dysku nawet, jeśli zawiera więcej niż 200 GB pamięci masowej.

szybkość IOPS Hello można uzyskać z hello AWR raportu. Określono hello Powtórz dziennika, fizyczne odczyty i zapisy szybkości.

![Zrzut ekranu przedstawiający stronę z raportem AWR hello](./media/oracle-design/awr_report.png)

Na przykład rozmiar Powtórz hello jest 12,200,000 bajtów na sekundę, która jest równa too11.63 MB/s.
Witaj IOPS jest 12,200,000 / 2,358 = 5,174.

Po umieszczeniu jasny obraz powitania wymagań operacji We/Wy, można wybrać kombinację dysków, które są najlepiej nadaje się toomeet tych wymagań.

**Zalecenia**

- Dla tabel danych rozmieszczenie obciążenia We/Wy hello liczba dysków za pomocą funkcji ASM Oracle lub zarządzanego magazynu.
- Jak zwiększa rozmiar bloku hello we/wy dla operacji intensywnego odczytu i zapisu intensywnie, Dodaj więcej dysków danych.
- Zwiększenie rozmiaru bloku hello dużych sekwencyjnych procesów.
- Użyj danych kompresji tooreduce we/wy (dla danych i indeksów).
- Oddzielne Powtórz dzienniki systemu i temps, a cofnąć usług terminalowych na dyskach danych.
- Nie należy umieszczać plików aplikacji na domyślne dysków systemu operacyjnego (/ dev/sda). Te dyski nie są zoptymalizowane dla maszyny Wirtualnej szybkiego czas uruchamiania i nie może zawierać dobrą wydajność aplikacji.

### <a name="disk-cache-settings"></a>Ustawienia pamięci podręcznej dysku

Istnieją trzy opcje buforowania na hoście:

- *Tylko do odczytu*: wszystkie żądania są buforowane dla przyszłych operacji odczytu. Zapisuje wszystkie są zachowywane bezpośrednio tooAzure magazynu obiektów Blob.

- *Odczyt i zapis*: jest to "odczytu z wyprzedzeniem" algorytmu. Witaj odczytuje i zapisuje są buforowane dla przyszłych operacji odczytu. Zapisy non-write-through są najpierw utrwalone toohello lokalnej pamięci podręcznej. Dla programu SQL Server zapisy są tooAzure utrwalonego magazynu, ponieważ używa go do zapisu. Zapewnia także hello można uzyskać najmniejsze opóźnienia dysku światła obciążeń.

- *Brak* (wyłączone): za pomocą tej opcji, można pominąć hello pamięci podręcznej. Wszystkie dane hello jest przeniesione toodisk i utrwalone tooAzure magazynu. Dzięki temu metody hello najwyższej szybkości operacji We/Wy dla intensywnych obciążeń we/wy. Należy również tootake "kosztów transakcji" pod uwagę.

**Zalecenia**

toomaximize hello przepływności, zalecamy rozpocząć od **Brak** dla buforowania na hoście. Dla usługi Premium Storage należy pamiętać o tym, należy wyłączyć bariery"hello" w przypadku zainstalowania systemu plików hello za pomocą hello **tylko do odczytu** lub **Brak** opcje. Zaktualizuj plik /etc/fstab hello hello UUID toohello dysków.

Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium dla maszyn wirtualnych systemu Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Zrzut ekranu przedstawiający stronę dysków zarządzanych w hello](./media/oracle-design/premium_disk02.png)

- W przypadku dysków systemu operacyjnego, użyj domyślnej **odczytu/zapisu** buforowania.
- Dla systemu, TEMP i cofania użyj **Brak** do buforowania.
- W przypadku danych, użyj **Brak** do buforowania. Ale jeśli bazy danych jest tylko do odczytu lub intensywnego odczytu, użyj **tylko do odczytu** buforowania.

Po zapisaniu ustawień dysku danych, chyba że Odinstaluj dysku hello na powitania poziomu systemu operacyjnego i ponownie zainstaluj po dokonaniu zmiany hello nie można zmienić ustawienia pamięci podręcznej hello hosta.


## <a name="security"></a>Bezpieczeństwo

Po Konfigurowanie i skonfigurowania środowiska Azure hello następnym krokiem jest toosecure sieci. Poniżej przedstawiono kilka zaleceń:

- *Zasady grupy NSG*: grupy NSG można zdefiniować przy podsieci lub kartę sieciową. Jest prostsze toocontrol dostęp na poziomie podsieci hello zabezpieczeń i Wymuś routingu dla elementów, jak zapór aplikacji.

- *Jumpbox*: bezpieczniejszego dostępu administratorów nie należy bezpośrednio łączyć toohello aplikacji usługi lub bazy danych. Jumpbox jest używane jako nośniki między hello administratora komputera i zasobów platformy Azure.
![Zrzut ekranu przedstawiający stronę topologii Jumpbox hello](./media/oracle-design/jumpbox.png)

    Witaj administratora maszyny powinno oferować tylko jumpbox toohello dostęp ograniczony IP. Witaj jumpbox powinien mieć dostęp toohello aplikacji i baz danych.

- *Sieć prywatna* (podsieci): zaleca się, czy masz usługi aplikacji hello i bazy danych w różnych podsieciach, lepszą kontrolę można ustawić przez zasady grupy NSG.


## <a name="additional-reading"></a>Dodatkowe materiały

- [Configure Oracle ASM (Konfigurowanie programu Oracle ASM)](configure-oracle-asm.md)
- [Skonfiguruj Oracle Data Guard](configure-oracle-dataguard.md)
- [Konfigurowanie bramy Golden Oracle](configure-oracle-golden-gate.md)
- [Oracle kopii zapasowych i odzyskiwania](oracle-backup-recovery.md)

## <a name="next-steps"></a>Następne kroki

- [Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności](../../linux/create-cli-complete.md)
- [Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej](../../linux/cli-samples.md)
