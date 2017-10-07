---
title: "warstwy pamięci podręcznej Redis Azure Premium toohello aaaIntroduction | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate trwałość Redis, klaster Redis i obsługa sieci Wirtualnej dla swoich wystąpień pamięci podręcznej Redis Azure warstwy Premium oraz zarządzanie nimi"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Wprowadzenie toohello pamięci podręcznej Redis Azure Premium warstwy
Pamięć podręczna Redis Azure jest pamięcią podręczną rozproszonych, zarządzanych, ułatwiające tworzenie wysoce skalowalne i szybko reagowały aplikacji przez udostępnienie danych tooyour nadrzędne szybki dostęp. 

Witaj, Nowa warstwa Premium jest warstwy gotowy przedsiębiorstwa, który zawiera wszystkie funkcje warstwy Standard hello i więcej informacji, takich jak lepszą wydajność, większych obciążeń, odzyskiwania po awarii, import/eksport i zwiększonych zabezpieczeń. Nadal toolearn odczytu więcej informacji na temat dodatkowych funkcji hello hello Premium pamięci podręcznej warstwy.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Lepszą wydajność w porównaniu tooStandard lub warstwa podstawowa
**Lepsza wydajność na standardowy lub podstawowa warstwy.** Pamięci podręczne w warstwie Premium hello są wdrażane na sprzęcie, szybkich procesorów i zapewnia lepszą wydajność w porównaniu toohello Basic lub warstwy standardowa. Pamięci podręczne warstwy Premium ma wyższą przepływność i dolnym opóźnienia. 

**Przepływności hello tej samej wielkości pamięci podręcznej jest wyższy w warstwie Premium jako tooStandard porównaniu warstwy.** Na przykład hello przepływności 53 GB P4 (Premium) pamięci podręcznej jest 250 KB żądań na sekundę jako too150K w porównaniu do C6 (Standard).

Aby uzyskać więcej informacji o rozmiarze, przepływności i przepustowości z pamięci podręcznych premium, zobacz [często zadawane pytania pamięci podręcznej Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Trwałość danych redis
warstwy Premium Hello umożliwia toopersist hello pamięci podręcznej danych na koncie magazynu Azure. W pamięci podręcznej Basic/Standard wszystkie dane hello są przechowywane tylko w pamięci. W przypadku podstawowej infrastruktury istnieje problem może być ryzyko utraty danych. Zalecamy używanie funkcji trwałości danych pamięci podręcznej Redis hello w hello Premium warstwy tooincrease odporności przed utratą danych. Pamięć podręczna Redis Azure oferuje RDB i AOF (wkrótce) opcje w [trwałość Redis](http://redis.io/topics/persistence). 

Aby uzyskać instrukcje na temat konfigurowania trwałości, zobacz [jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Klaster redis
Toocreate pamięci podręcznych większych niż 53 GB lub chcesz tooshard danych między wieloma węzłami Redis, można użyć klastrowania, która jest dostępna w warstwie Premium hello Redis. Każdy węzeł składa się z pary pamięć podręczna podstawowy/replik zarządzanych przez usługę Azure wysokiej dostępności. 

**Klaster redis daje maksymalną skalę i przepustowość.** Przepływność zwiększa liniowo zwiększyć liczbę hello odłamków (węzłów) w klastrze hello. Np. Jeśli tworzenie klastra P4 odłamków 10, a następnie hello dostępna przepustowość wynosi 250K * 10 = 2,5 mln żądań na sekundę. Zobacz hello [często zadawane pytania pamięci podręcznej Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) szczegółowe informacje o rozmiarze, przepływności i przepustowości z pamięci podręcznych premium.

tooget wprowadzenie do klastra, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Większe bezpieczeństwo i izolacja
Pamięci podręczne utworzone w warstwie podstawowa i standardowa hello są dostępne na hello publicznej sieci internet. Toohello dostęp do pamięci podręcznej jest ograniczone hello na podstawie klucza dostępu. Z warstwy Premium hello dalsze zapewni, że tylko klienci w określonej sieci mogą uzyskiwać dostęp hello pamięci podręcznej. Można wdrożyć pamięci podręcznej Redis w [sieci wirtualnej platformy Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). Można używać wszystkich funkcji hello sieci wirtualnej, takie jak podsieci, zasady kontroli dostępu i inne funkcje toofurther ograniczyć tooRedis dostępu.

Aby uzyskać więcej informacji, zobacz [jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Import/Export
Import/Eksport jest pamięć podręczna Redis Azure operacji zarządzania danych, co pozwala tooimport danych w pamięci podręcznej Redis Azure lub eksportowania danych z pamięci podręcznej Redis Azure przez importowanie i Eksportowanie migawki Redis pamięci podręcznej bazy danych (RDB) z obiektu blob strony premium pamięci podręcznej tooa na platformie Azure Konto magazynu. To pozwala toomigrate między różnymi wystąpieniami usługi pamięć podręczna Redis Azure lub wypełnienia pamięci podręcznej hello danych przed użyciem.

Importu mogą być używane toobring Redis zgodne RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, w tym Redis w systemie Linux, Windows albo dowolnego dostawcy chmury, takich jak usług Amazon Web Services i innych użytkowników. Importowanie danych jest łatwe toocreate pamięci podręcznej z wstępnie wypełnione danych. Podczas procesu importowania hello pamięć podręczna Redis Azure ładuje hello RDB pliki z magazynu Azure do pamięci i wstawianie hello klucze do pamięci podręcznej hello.

Eksport umożliwia tooexport hello danych przechowywanych w pamięci podręcznej Redis Azure tooRedis zgodne pliki RDB. Można użyć tych danych toomove funkcji z jednego tooanother wystąpienia pamięci podręcznej Redis Azure lub tooanother serwera Redis. W procesie eksportu hello plik tymczasowy zostanie utworzony na powitania wirtualna hostów hello wystąpienie serwera pamięci podręcznej Redis Azure, czy plik hello jest przekazany toohello wyznaczony konta magazynu. Po ukończeniu operacji eksportowania hello ze stanem powodzenie lub niepowodzenie hello plik tymczasowy zostanie usunięty.

Aby uzyskać więcej informacji, zobacz [jak tooimport dane i eksportowanie danych z pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Ponowne uruchamianie
warstwy premium Hello umożliwia tooreboot jeden lub większą liczbę węzłów z pamięci podręcznej na żądanie. Dzięki temu można tootest aplikacji zapewnia odporność na awarie w zdarzeniu hello awarii. Można ponownie uruchomić hello następujące węzły.

* Główny węzeł pamięci podręcznej
* Węzeł podrzędny z pamięci podręcznej
* Zarówno i podrzędna węzłów pamięci podręcznej
* Korzystając z usługi pamięć podręczna premium z usługą klastrowania, możesz ponownie hello główny, podrzędny lub oba węzły dla poszczególnych fragmentów w pamięci podręcznej hello

Aby uzyskać więcej informacji, zobacz [ponowny rozruch](cache-administration.md#reboot) i [często zadawane pytania dotyczące ponownego uruchamiania](cache-administration.md#reboot-faq).

>[!NOTE]
>Ponowny rozruch funkcja jest teraz włączona dla wszystkich warstw pamięci podręcznej Redis Azure.
>
>

## <a name="schedule-updates"></a>Aktualizacje harmonogramu
Funkcja zaplanowanych aktualizacji Hello pozwala toodesignate okno obsługi pamięci podręcznej. Okna obsługi hello jest określona, wszystkie aktualizacje serwera Redis są wprowadzane podczas tego okna. toodesignate okna konserwacji, wybrać żądaną hello dni i określ hello godzina rozpoczęcia okna konserwacji dla każdego dnia. Należy pamiętać, że czas okna obsługi hello jest w formacie UTC. 

Aby uzyskać więcej informacji, zobacz [Zaplanuj aktualizacje](cache-administration.md#schedule-updates) i [Zaplanuj aktualizacje — często zadawane pytania](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Tylko pamięci podręcznej Redis serwera wprowadzone aktualizacje hello zaplanowanym oknie obsługi. okna obsługi Hello aktualizacji systemu operacyjnego maszyny Wirtualnej toohello lub nie ma zastosowania aktualizacji tooAzure.
> 
> 

## <a name="geo-replication"></a>Replikacja geograficzna

**Replikacja geograficzna** zapewnia mechanizm łączenia dwa wystąpienia pamięci podręcznej Redis Azure warstwy Premium. Jedna pamięć podręczna jest wyznaczony jako hello głównej połączonego pamięci podręcznej i hello innych jako hello dodatkowej połączonego pamięci podręcznej. Hello pamięci podręcznej połączonego dodatkowej staje się tylko do odczytu i jest zapisany toohello głównej pamięci podręcznej danych replikowane toohello dodatkowej połączonego pamięci podręcznej. Ta funkcja może być używana tooreplicate pamięci podręcznej w regionach platformy Azure.

Aby uzyskać więcej informacji, zobacz [jak tooconfigure — replikacja geograficzna dla pamięci podręcznej Redis Azure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>warstwy premium toohello tooscale
warstwy premium toohello tooscale, po prostu wybierz jedną z warstwy premium hello w hello **Zmiana warstwy cenowej** bloku. Można również skalować warstwę premium toohello pamięci podręcznej przy użyciu programu PowerShell i interfejsu wiersza polecenia. Aby uzyskać instrukcje, zobacz [jak tooScale Azure pamięci podręcznej Redis](cache-how-to-scale.md) i [jak tooautomate operacji skalowania](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Następne kroki
Tworzenie pamięci podręcznej i Eksploruj hello nowych funkcji warstwy premium.

* [Jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md)
* [Jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md)
* [Jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md)
* [Jak dane tooimport i eksportowanie danych z pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md)
* [Jak tooadminister Azure pamięci podręcznej Redis](cache-administration.md)

