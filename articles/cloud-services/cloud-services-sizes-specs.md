---
title: "rozmiary aaaVirtual dla usług w chmurze Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla hello rozmiary inną maszynę wirtualną (i identyfikatory) dla usługi chmury Azure role sieci web i proces roboczy."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Rozmiary dla usług w chmurze
W tym temacie opisano dostępne rozmiary hello i opcje dla wystąpień roli usługi w chmurze (role sieci web i proces roboczy). Umożliwia także toobe zagadnienia dotyczące wdrażania uwagę podczas planowania toouse tych zasobów. Rozmiar każdego ma identyfikator umieszczony w sieci [pliku definicji usługi](cloud-services-model-and-package.md#csdef). Ceny dla każdego rozmiaru są dostępne na powitania [cennik usługi w chmurze](https://azure.microsoft.com/pricing/details/cloud-services/) strony.

> [!NOTE]
> toosee związane z limitami Azure, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Rozmiary dla wystąpień roli sieci web i proces roboczy
Istnieje wiele toochoose standardowych rozmiarów z na platformie Azure. Uwagi dotyczące niektórych z tych rozmiarów:

* D-series maszyny wirtualne są zaprojektowane toorun aplikacji, które wymaga wyższej moc obliczeniową i wydajność dysku tymczasowym. Maszyny wirtualne D-series zapewniają szybkich procesorów, większy współczynnik pamięci — podstawowe i dysków półprzewodnikowych (SSD) dla dysku tymczasowym hello. Aby uzyskać więcej informacji, zobacz anons hello na powitania Azure blog [nowe rozmiary maszyny wirtualnej D-Series](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Dv2-series, finałowa toohello oryginalnego D-series, funkcje większe możliwości procesora CPU. Hello serii Dv2 Procesora CPU D-series jest około 35% szybciej niż hello. Jest on oparty na powitania najnowszej generacji 2.4 v3® GHz Intel Xeon E5-2673 procesora (Haswell) i z hello Intel Turbo zwiększanie wyniku technologii 2.0, może przejść w górę too3.1 GHz. ma Hello serii Dv2 hello takie same konfiguracje pamięci i dysku, ponieważ hello D-series.
* Maszyny wirtualne z serii G oferują hello najwięcej pamięci i uruchom na hostach, które mają rodziny procesorów Intel Xeon E5 V3.
* Witaj A-series maszyn wirtualnych może zostać wdrożony w różne typy sprzętu i procesorów. rozmiar Hello jest ograniczany na powitania sprzętu, wydajność procesora spójne toooffer hello uruchomione wystąpienie, niezależnie od sprzętu hello, który jest wdrożony na podstawie. toodetermine hello sprzętu fizycznego wdrożeniu ten rozmiar, zapytania hello sprzęt wirtualny z wewnątrz hello maszyny wirtualnej.
* rozmiar A0 Hello jest nadmiernie subskrybowanego na sprzęcie fizycznym hello. Dla tego określonego rozmiaru tylko wtedy innych wdrożeń klienta może mieć wpływ na wydajność hello obciążenia uruchomione. Hello względną wydajność opisanym poniżej jako jej linia bazowa hello oczekiwano, podmiotu tooan przybliżonej zmienność 15 procent.

Hello rozmiar maszyny wirtualnej hello ma wpływ na powitania cennik. rozmiar Hello wpływa także hello przetwarzania, pamięci oraz Magazyn pojemności hello maszyny wirtualnej. Koszty przechowywania są obliczane osobno na podstawie używane strony w hello konta magazynu. Aby uzyskać więcej informacji, zobacz [szczegóły cennika usługi w chmurze](https://azure.microsoft.com/pricing/details/cloud-services/) i [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

Hello następujące zagadnienia dotyczące mogą pomóc w podjęciu decyzji o rozmiarze:

* Hello rozmiary A8 A11 i H-series są również znane jako *wystąpień obliczeniowych*. Hello sprzęt, który uruchamia te rozmiary został zaprojektowany i zoptymalizowany pod kątem obliczeniowych i aplikacji, modelowania i symulacje klastra aplikacji obciążenie sieci, w tym obliczeniowe wysokiej wydajności (HPC). Witaj serii A8 A11 korzysta Intel Xeon E5-2670 @ 2.6 GHZ, a hello H-series v3 Intel Xeon E5-2667 @ 3,2 GHz. Aby uzyskać szczegółowe informacje i zagadnienia dotyczące korzystania z tych wielkości, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Dv2-series, D-series, G serii idealnie nadają się do aplikacji, które wymagają szybszych procesorów CPU, lokalnego lepszą wydajność dysku lub mają wyższe wymagania pamięci. Oferują one kombinację opcji o dużych możliwościach dla wielu aplikacji klasy korporacyjnej.
* Niektóre hosty fizyczne hello w centrach danych platformy Azure mogą nie obsługiwać większych rozmiarów maszyn wirtualnych, takie jak A5 — A11. W związku z tym może zostać wyświetlony komunikat błędu hello **maszyny wirtualnej nie powiodła się tooconfigure {nazwa komputera}** lub **maszyny wirtualnej nie powiodła się toocreate {nazwa komputera}** podczas zmiany rozmiaru istniejących nowe tooa maszyny wirtualnej rozmiar; Tworzenie nowej maszyny wirtualnej w sieci wirtualnej utworzonej przed 16 kwietnia 2013; lub dodanie nowej maszyny wirtualnej tooan istniejącej usługi w chmurze. Zobacz [błąd: "Maszyny wirtualnej nie powiodła się tooconfigure"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) na powitania forum pomocy technicznej dla rozwiązania dla każdego scenariusza wdrażania.
* Subskrypcji może również ograniczać hello liczba rdzeni, którą można wdrożyć w niektórych rodzin rozmiar. tooincrease limit przydziału, skontaktuj się z pomocą techniczną platformy Azure.

## <a name="performance-considerations"></a>Zagadnienia dotyczące wydajności
Utworzono pojęcie hello hello Azure obliczeniowe jednostki (ACU) tooprovide sposób porównywania wydajności obliczeniowej (procesora CPU) w jednostki SKU Azure i tooidentify, którego jednostka SKU jest najprawdopodobniej toosatisfy wydajność wymaga.  Jednostka ACU jest obecnie standaryzowana na małej maszynie wirtualnej (Standardowa_A1) jako równa 100, a wszystkie pozostałe jednostki SKU reprezentują w przybliżeniu, o ile szybciej dana jednostka SKU może uruchomić standardowy test porównawczy.

> [!IMPORTANT]
> Witaj ACU jest tylko wytyczne. wyniki powitania dla obciążenia mogą się różnić.
>
>

<br>

| Rodzina SKU | ACU/rdzeń |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Mała liczba godzin ExtraLarge](#a-series) |100 |
| [A5 7](#a-series) |100 |
| [Standardowa_A1–8v2](#av2-series) |100 |
| [Standardowa_A2m–8mv2](#av2-series) |100 |
| [A8–A11](#a-series) |225* |
| [D1–14](#d-series) |160 |
| [D1–15v2](#dv2-series) |210 - 250* |
| [G1–5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

ACUs oznaczonych * użyć częstotliwości tooincrease Procesora technologii Intel® Turbo i podaj wzrost wydajności. Hello ilość zwiększanie wyniku hello mogą różnić w zależności od rozmiaru maszyny Wirtualnej hello, obciążenia i innych obciążeń uruchomionych na powitania tego samego hosta.

## <a name="size-tables"></a>Tabele rozmiarów
Witaj w poniższych tabelach hello rozmiary i pojemności hello, które zapewniają.

* Pojemność magazynu jest podawana w jednostkach GiB (1024^3 bajtów). Gdy porównanie dysków mierzony w GB (1000 ^ 3 bajtów) toodisks mierzony w GiB (1024 ^ 3) należy pamiętać, że liczby pojemności podane w GiB może pojawić się mniejszą. Na przykład 1023 GiB = 1098,4 GB.
* Przepływność dysku mierzona jest jako liczba operacji wejścia/wyjścia na sekundę i MB/s, gdzie 1 MB/s = 10^6 bajtów/s.
* Dyski danych mogą działać w trybie buforowanym lub niebuforowanym. Dla operacji dysku danych z pamięci podręcznej, tryb buforowania hosta hello ustawiono zbyt**tylko do odczytu** lub **ReadWrite**. Dla operacji dysku bez buforowania danych, hello hosta pamięci podręcznej jest tryb zbyt**Brak**.
* Maksymalna przepustowość sieci jest hello zagregowanej przepustowości maksymalnej przydzielone i przypisywane do typu maszyny Wirtualnej. Maksymalna przepustowość Hello zawiera wskazówki dotyczące wybierania hello prawo maszyny Wirtualnej typu tooensure pojemność odpowiednie sieci jest dostępna. Podczas przenoszenia między niski, umiarkowany, wysokiej i bardzo wysoka, w związku z tym zwiększa przepływność hello. Rzeczywista wydajność sieci będzie zależeć od wielu czynników, takich jak obciążenia sieciowe i obciążenia aplikacji oraz ustawienia sieciowe aplikacji.

## <a name="a-series"></a>Seria A
| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalny dysk twardy: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| ExtraSmall      | 1         | 0,768        | 20                   | 1 / niska |
| Small           | 1         | 1,75         | 225                  | 1 / średnia |
| Medium          | 2         | 3,5 GB       | 490                  | 1 / średnia |
| Large           | 4         | 7            | 1000                 | 2 / wysoka |
| ExtraLarge      | 8         | 14           | 2040                 | 4 / wysoka |
| A5              | 2         | 14           | 490                  | 1 / średnia |
| A6              | 4         | 28           | 1000                 | 2 / wysoka |
| A7              | 8         | 56           | 2040                 | 4 / wysoka |

## <a name="a-series---compute-intensive-instances"></a>Seria A — wystąpienia intensywnie korzystające z mocy obliczeniowej
Aby informacjami i zagadnieniami dotyczącymi przy użyciu tych rozmiarów, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalny dysk twardy: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8 *             |8          | 56           | 1817                 | 2 / wysoka |
| A9 *             |16         | 112          | 1817                 | 4 / bardzo wysoka |
| A10             |8          | 56           | 1817                 | 2 / wysoka |
| A11             |16         | 112          | 1817                 | 4 / bardzo wysoka |

\*Obsługuje funkcję RDMA

## <a name="av2-series"></a>Seria Av2

| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalne dyski SSD: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standardowa_A1_v2  | 1         | 2            | 10                   | 1 / średnia                 |
| Standardowa_A2_v2  | 2         | 4            | 20                   | 2 / średnia                 |
| Standardowa_A4_v2  | 4         | 8            | 40                   | 4 / wysoka                     |
| Standardowa_A8_v2  | 8         | 16           | 80                   | 8 / wysoka                     |
| Standardowa_A2m_v2 | 2         | 16           | 20                   | 2 / średnia                 |
| Standardowa_A4m_v2 | 4         | 32           | 40                   | 4 / wysoka                     |
| Standardowa_A8m_v2 | 8         | 64           | 80                   | 8 / wysoka                     |


## <a name="d-series"></a>Seria D
| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalne dyski SSD: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standardowa_D1     | 1         | 3,5          | 50                   | 1 / średnia |
| Standardowa_D2     | 2         | 7            | 100                  | 2 / wysoka |
| Standardowa_D3     | 4         | 14           | 200                  | 4 / wysoka |
| Standardowa_D4     | 8         | 28           | 400                  | 8 / wysoka |
| Standardowa_D11    | 2         | 14           | 100                  | 2 / wysoka |
| Standardowa_D12    | 4         | 28           | 200                  | 4 / wysoka |
| Standardowa_D13    | 8         | 56           | 400                  | 8 / wysoka |
| Standardowa_D14    | 16        | 112          | 800                  | 8 / bardzo wysoka |

## <a name="dv2-series"></a>Seria Dv2
| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalne dyski SSD: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standardowa_D1_v2  | 1         | 3,5          | 50                   | 1 / średnia |
| Standardowa_D2_v2  | 2         | 7            | 100                  | 2 / wysoka |
| Standardowa_D3_v2  | 4         | 14           | 200                  | 4 / wysoka |
| Standardowa_D4_v2  | 8         | 28           | 400                  | 8 / wysoka |
| Standardowa_D5_v2  | 16        | 56           | 800                  | 8 / ekstremalnie wysoka |
| Standardowa_D11_v2 | 2         | 14           | 100                  | 2 / wysoka |
| Standardowa_D12_v2 | 4         | 28           | 200                  | 4 / wysoka |
| Standardowa_D13_v2 | 8         | 56           | 400                  | 8 / wysoka |
| Standardowa_D14_v2 | 16        | 112          | 800                  | 8 / ekstremalnie wysoka |
| Standard_D15_v2 | 20        | 140          | 1000                | 8 / ekstremalnie wysoka |

## <a name="g-series"></a>Seria G
| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalne dyski SSD: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standardowa_G1     | 2         | 28           | 384                  |1 / wysoka |
| Standardowa_G2     | 4         | 56           | 768                  |2 / wysoka |
| Standardowa_G3     | 8         | 112          | 1536                |4 / bardzo wysoka |
| Standardowa_G4     | 16        | 224          | 3072                |8 / ekstremalnie wysoka |
| Standard_G5     | 32        | 448          | 6144                |8 / ekstremalnie wysoka |

## <a name="h-series"></a>Seria H
Maszyny wirtualne platformy Azure H-series są hello następnej generacji wysokiej wydajności obliczeniowych, że maszyny wirtualne celem potrzeb obliczeniową górną granicę, jak molekularnej modelowania i obliczeniową dynamics płynu. Te 8 i 16 rdzeni maszyn wirtualnych są utworzone na powitania V3 2667 Haswell E5 Intel technologii DDR4 pamięci i lokalny magazyn na dyskach SSD.

Ponadto toohello znacznej moc procesora CPU, hello H-series oferuje różnych opcji małe opóźnienia sieci RDMA przy użyciu FDR InfiniBand i kilka konfiguracji toosupport pamięci znacznym obliczeniową wymagania dotyczące pamięci.

| Rozmiar            | Rdzenie procesora CPU | Pamięć: GiB  | Lokalne dyski SSD: GiB       | Maksymalna liczba kart sieciowych / przepustowość sieci |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standardowa_H8     | 8         | 56           | 1000                 | 8 / wysoka |
| Standardowa_H16    | 16        | 112          | 2000                 | 8 / bardzo wysoka |
| Standardowa_H8m    | 8         | 112          | 1000                 | 8 / wysoka |
| Standardowa_H16m   | 16        | 224          | 2000                 | 8 / bardzo wysoka |
| Standardowa_H16r*  | 16        | 112          | 2000                 | 8 / bardzo wysoka |
| Standardowa_H16mr* | 16        | 224          | 2000                 | 8 / bardzo wysoka |

\*Obsługuje funkcję RDMA

## <a name="configure-sizes-for-cloud-services"></a>Skonfiguruj rozmiary dla usług w chmurze
Można określić rozmiaru maszyny wirtualnej hello wystąpienia roli w ramach modelu usług hello opisanego przez hello [pliku definicji usługi](cloud-services-model-and-package.md#csdef). rozmiar Hello roli hello określa hello liczba rdzeni Procesora, hello pojemność pamięci i rozmiar systemu lokalnego pliku hello przydzielonej tooa uruchomione wystąpienie. Wybierz rozmiar roli hello oparte na zapotrzebowanie na zasoby aplikacji.

Oto przykład do ustawiania toobe rozmiar roli hello [Standard_D2](#general-purpose-d) dla wystąpienia roli sieci Web:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Zmienianie rozmiaru hello istniejącej roli

Jako hello charakteru zmiany obciążenia lub nowe rozmiary maszyn wirtualnych, które stają się dostępne może być toochange hello rozmiar roli użytkownika. toodo tak, należy zmienić rozmiar maszyny Wirtualnej hello w pliku definicji usługi (jak pokazano powyżej), Spakuj ponownie usługi w chmurze i wdróż je. Nie jest możliwe toochange rozmiarów maszyn wirtualnych bezpośrednio z portalu hello lub programu PowerShell.

>[!TIP]
> Może być toouse różnych rozmiarów maszyn wirtualnych dla roli użytkownika w różnych środowiskach (np.) Produkcja vs test). Jednym ze sposobów toodo to jest toocreate wiele plików definicji (csdef) usługi w projekcie, a następnie utwórz inną chmurę pakietów usług na środowisko podczas automatycznego kompilację za pomocą narzędzia CSPack hello. pakiet usług toolearn więcej informacji na temat elementów hello chmury i toocreate, zobacz temat [co to jest chmura hello usług modelu i jak jest pakiet?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Pobierz listę rozmiary
Możesz użyć programu PowerShell lub interfejsu API REST tooget listę rozmiarów hello. Witaj interfejsu API REST jest udokumentowany [tutaj](https://msdn.microsoft.com/library/azure/dn469422.aspx). Witaj następujący kod jest polecenia programu PowerShell, która będzie zawierała listę wszystkich rozmiarów hello obecnie dostępne dla usługi w chmurze.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat [limitów, przydziałów i ograniczeń usługi i subskrypcji platformy Azure](../azure-subscription-service-limits.md).
* Dowiedz się więcej [o wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dla obciążeń HPC.
