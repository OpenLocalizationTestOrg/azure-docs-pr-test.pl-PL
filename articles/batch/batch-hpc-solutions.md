---
title: "aaaBatch i HPC rozwiązań w chmurze hello - Azure | Dokumentacja firmy Microsoft"
description: "Scenariusze i opcje rozwiązań obliczania wsadowego i obliczeń o wysokiej wydajności (obliczenia HPC i duże obliczenia) na platformie Azure"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Rozwiązania usługi Batch i HPC dla dużych obciążeń obliczeniowych

Platforma Azure oferuje wydajne, skalowalne rozwiązania w chmurze dla usługi Batch i obliczeń o wysokiej wydajności (HPC) — zwanych również *dużymi obliczeniami*. Dowiedz się więcej tutaj o obliczeniowe dużych obciążeń i toosupport usług platformy Azure je lub przejść bezpośrednio za[scenariuszy rozwiązań](#scenarios) dalszej części tego artykułu. Ten artykuł dotyczy głównie decydentów technicznych, menedżerów i niezależnym dostawcom oprogramowania, ale inne Informatycy i deweloperzy mogą używać it toofamiliarize się z tych rozwiązań.

Organizacje zajmują się zagadnieniami obliczeniowymi na dużą skalę, m.in. projektowaniem inżynierskim i analizą, renderowaniem obrazu, złożonym modelowaniem, symulacjami Monte Carlo oraz obliczeniami w zakresie ryzyka finansowego. Azure pomaga organizacjom w rozwiązaniu tych problemów z zasobów hello, skala i harmonogram, które są im potrzebne. Za pomocą platformy Azure organizacje mogą:

* Tworzenie hybrydowych rozwiązań, rozszerzanie lokalnego HPC klastra toooffload szczytowego obciążenia toohello chmury
* uruchamiać narzędzia klastra HPC i obciążenia w całości na platformie Azure;
* Użyj zarządzanego i skalowalnych usług platformy Azure, takiego jak [partii](https://azure.microsoft.com/documentation/services/batch/) obciążeń obliczeniowych toorun bez konieczności toodeploy infrastruktury obliczeń i zarządzanie nią

Mimo że poza zakres tego artykułu hello, Azure udostępnia deweloperów i partnerów pełny zestaw możliwości, opcje architektury i programowanie narzędzia toobuild na dużą skalę, niestandardowe Big obliczeniowe przepływów pracy. I rosnącym ekosystemem partnerów jest gotowy toohelp wprowadzeniu obliczeniowe dużych obciążeń produkcyjnych w hello chmury Azure.

## <a name="batch-and-hpc-applications"></a>Aplikacje usługi Batch i HPC
W przeciwieństwie do aplikacji sieci Web i wielu aplikacji biznesowych — aplikacje usługi Batch i HPC mają zdefiniowany początek i koniec oraz mogą być uruchamiane zgodnie z harmonogramem lub na żądanie — czasami przez wiele godzin lub dłużej. Większość można podzielić na dwie główne kategorie: *leżą równoległych* (nazywane czasem "embarrassingly równoległe", ponieważ ich rozwiązywania problemów hello redagowanie toorunning równolegle na wielu komputerach lub procesorów) i *silnie sprzężonego*. Zobacz hello, aby uzyskać więcej informacji na temat tych typów aplikacji w poniższej tabeli. Niektóre rozwiązania Azure zbliża się do pracy lepsze dla jednego typu lub hello innych.

> [!NOTE]
> W rozwiązaniach usługi Batch i HPC uruchomione wystąpienie aplikacji jest zwykle nazywane *zadaniem* i każde zadanie może zostać podzielone na *podzadania*. I hello zasoby obliczeniowe klastra dla aplikacji hello są często nazywane *węzły obliczeniowe*.
> 
> 

| Typ | Właściwości | Przykłady |
| --- | --- | --- |
| **Wewnętrznie równoległe**<br/><br/>![Wewnętrznie równoległe][parallel] |• Poszczególne komputery uruchamiają logikę aplikacji niezależnie<br/><br/> Dodawanie komputerów • umożliwia hello tooscale i zmniejszenie obliczenia czas aplikacji<br/><br/>• Aplikacja składa się z oddzielnych plików wykonywalnych lub jest podzielona na usługi wywoływane przez klienta (architekturę zorientowaną na usługi lub SOA, aplikację) |• Modelowanie ryzyka finansowego<br/><br/>• Renderowanie obrazu i przetwarzanie obrazu<br/><br/>• Kodowanie i transkodowanie nośników<br/><br/>• Symulacje Monte Carlo<br/><br/>• Testowanie oprogramowania |
| **Mocno powiązane**<br/><br/>![Mocno powiązane][coupled] |• Aplikacji wymaga obliczeń węzłów toointeract lub exchange pośrednich wyników<br/><br/>• Obliczeniowej węzły mogą komunikować się za pomocą hello komunikat interfejsu (Passing Interface), wspólny protokół komunikacji dla przetwarzania równoległego<br/><br/>• aplikacji hello jest opóźnienia toonetwork poufnych i przepustowości<br/><br/>• Wydajność aplikacji można zwiększyć za pomocą szybkich technologii sieciowych, takich jak InfiniBand i zdalny bezpośredni dostęp do pamięci (RDMA) |• Modelowanie zbiorników ropy naftowej i gazu<br/><br/>• Projektowanie inżynieryjne i analiza, np. obliczeniowa dynamika hydrauliczna<br/><br/>• Fizyczne symulacje, takie jak wypadki samochodowe i reakcje jądrowe<br/><br/>• Prognozowanie pogody |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Zagadnienia dotyczące uruchamiania aplikacji wsadowych i aplikacji HPC w chmurze hello
Łatwo można migrować wiele aplikacji, które są zaprojektowane toorun tooAzure klastrów HPC lokalnymi lub tooa środowiska hybrydowego (między lokalizacjami). Mogą jednak występować pewne ograniczenia lub problemy, m.in.:

* **Dostępność zasobów w chmurze** — w zależności od typu hello chmury zasoby obliczeniowe używasz, może nie być możliwe toorely na dostępność maszyn ciągłego podczas wykonywania zadania. Obsługa stanu i postępu Sprawdź, czy wskazanie są typowe techniki toohandle możliwe przejściowe błędy i bardziej niezbędne podczas korzystania z zasobów w chmurze.
* **Dostęp do danych** -powszechnie dostępne w klastrach przedsiębiorstwa, takie jak NFS, techniki dostępu do danych może wymaga specjalnej konfiguracji w chmurze hello. Lub może być konieczne tooadopt różnych danych access rozwiązania i wzorce hello chmury.
* **Przenoszenie danych** — dla aplikacji, czy Proces dużych ilości danych, strategie są wymagane toomove hello dane do magazynu i toocompute zasobów chmury. Może być też konieczne użycie szybkiej sieci obejmującej różne lokalizacje (takiej jak [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/)). Należy również rozważyć ograniczenia prawne, regulacyjne lub dotyczące zasad w zakresie przechowywania lub uzyskiwania dostępu do danych.
* **Licencjonowanie** — skontaktować się z dostawcą hello stosowania komercyjnych licencjonowania lub inne ograniczenia dotyczące uruchamiania w hello chmury. Nie wszyscy dostawcy oferują licencjonowanie oparte na płatności zgodnie z rzeczywistym użyciem. Może być potrzebna tooplan serwer licencyjny w chmurze hello for rozwiązania lub połączyć tooan lokalnego serwera licencji.

### <a name="big-compute-or-big-data"></a>Duże obliczenia czy dane big data?
Hello podział wiersza między aplikacjami obliczeniowe duży i danych Big Data nie zawsze jest jasne, a niektóre aplikacje mogą mieć cechy obu. Obie kategorie obejmują uruchamianie obliczeń na dużą skalę, zwykle w klastrach komputerów. Ale hello podejścia rozwiązania i narzędzia obsługi mogą się różnić.

• **Obliczeniowe big** zwykle aplikacje tooinvolve, które są oparte na mocy Procesora i pamięci, takich jak engineering symulacje ryzyka finansowego modelowania oraz cyfrowe renderowania. Hello infrastruktury dla rozwiązania obliczeniowe duży może obejmować komputery z obliczeń raw tooperform specjalne wielordzeniowych procesorów i specjalne funkcje szybkich sieci sprzętu tooconnect hello komputerów.

• Funkcja **danych big data** pozwala rozwiązać problemy związane z analizą danych, które polegają na tym, że nie można zarządzać dużą ilością danych przy użyciu jednego komputera lub w jednym systemie zarządzania bazą danych, np. dużą liczbą dzienników sieci Web lub innymi danymi analiz biznesowych. Dane big Data zwykle toorely więcej informacji na temat pojemności dysku i wydajność We/Wy niż na mocy procesora CPU. Dostępne są także specjalne narzędzi danych Big Data, takich jak Apache Hadoop toomanage hello klastra i partycja hello danych. (Informacje o usłudze Azure HDInsight oraz innych rozwiązaniach Azure Hadoop znajdują się w temacie [Hadoop](https://azure.microsoft.com/solutions/hadoop/)).

## <a name="compute-management-and-job-scheduling"></a>Zarządzanie mocą obliczeniową i planowanie zadań
Uruchamianie aplikacji wsadowych i HPC często obejmuje *Menedżera klastra* i *harmonogramu zadań* toohelp zarządzanie zasobami klastra obliczeniowego i przydzielić im toohello aplikacje, które działają hello zadania. Operacje te można wykonać przy użyciu osobnych narzędzi lub zintegrowanego narzędzia bądź usługi.

* **Menedżer klastra** — aprowizuje i zwalnia zasoby obliczeniowe (lub węzły obliczeniowe) oraz nimi zarządza. Menedżer klastra może zautomatyzować instalacji obrazów systemów operacyjnych i aplikacji w węzłach obliczeniowych skalowania zasobów obliczeniowych, zgodnie z toodemands i monitorować wydajność hello hello węzłów.
* **Harmonogram zadań** — określa hello zasoby (na przykład procesorów lub pamięci) aplikacja wymaga i hello warunki po uruchomieniu. Harmonogram zadań przechowuje kolejki zadań i przydziela toothem zasobów na podstawie priorytetem lub inne właściwości.

Klastrowanie i planowanie narzędzia w przypadku klastrów systemu Windows i Linux można migrować dobrze tooAzure. Na przykład [zestaw Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029), bezpłatne rozwiązanie klastra obliczeniowego firmy Microsoft dla obciążeń HPC w systemach Windows i Linux, oferuje kilka opcji uruchamiania na platformie Azure. Można także utworzyć klastry z systemem Linux toorun open source narzędzi, takich jak moment i SLURM. Można również przełączyć tooAzure rozwiązań komercyjnych siatki, takich jak [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [Symphony spektrum IBM i Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), i [Univa siatki aparat](http://www.univa.com/products/grid-engine).

Jak pokazano na powitania następujące sekcje zawierają informacje, można również korzystać z usług Azure toomanage zasoby obliczeniowe i zaplanować zadania bez (lub oprócz) narzędzia do zarządzania tradycyjnego klastra.

## <a name="scenarios"></a>Scenariusze
Poniżej przedstawiono trzy typowe scenariusze toorun obliczeniowe dużych obciążeń na platformie Azure przy użyciu istniejących rozwiązań klastra HPC, usług platformy Azure lub kombinację hello dwa. Najważniejsze kwestie dotyczące wybierania poszczególnych scenariuszy zostały wymienione, ale nie opisano ich tutaj w sposób wyczerpujący. Więcej o hello dostępnych usług Azure używanego w rozwiązaniu jest dalszej części artykułu hello.

| Scenariusz | Powód wybrania? |
| --- | --- | --- |
| **Serii tooAzure klastra HPC**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Więcej informacji:<br/>• [Serii wystąpień procesów roboczych tooAzure pakietem HPC](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Set up a hybrid compute cluster with HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) (Konfigurowanie hybrydowego klastra obliczeniowego za pomocą zestawu HPC Pack)<br/><br/>• [Serii tooAzure partii z pakietem HPC](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Połączenie [zestawu Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) lub innego klastra lokalnego z dodatkowymi zasobami Azure w ramach rozwiązania hybrydowego.<br/><br/>• Rozszerzyć Twoje toorun obliczeniowe dużych obciążeń na platformie jako usługa (PaaS) wystąpień maszyn wirtualnych (obecnie Windows tylko serwery).<br/><br/>• Dostęp do lokalnego serwera licencji lub magazynu danych przy użyciu opcjonalnej sieci wirtualnej Azure. |
| **Utworzenie klastra HPC w całości na platformie Azure**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Więcej informacji:<br/>• [HPC cluster solutions in Azure](big-compute-resources.md) (Rozwiązania klastra HPC na platformie Azure)<br/><br/> |• Szybkie i spójne wdrażanie aplikacji i narzędzi klastra na standardowych i niestandardowych maszynach wirtualnych w modelu IaaS (infrastruktura jako usługa) w systemie Windows lub Linux.<br/><br/>• Uruchom różnych obciążeń z dużą obliczeniowe przy użyciu hello planowanie rozwiązania wybranych przez użytkownika.<br/><br/>• Użyj dodatkowymi usługami platformy Azure, w tym sieci i magazynu toocreate pełną rozwiązań w chmurze. |
| **Skalowanie w poziomie tooAzure aplikacji równoległych**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Więcej informacji:<br/>• [Podstawy usługi Azure Batch](batch-technical-overview.md)<br/><br/>• [Wprowadzenie hello biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md) |• Opracowywania [partii zadań Azure](https://azure.microsoft.com/documentation/services/batch/) tooscale limit różnych toorun obciążenia obliczeniowe Big w pulach maszyn wirtualnych systemu Windows lub Linux.<br/><br/>• Za pomocą wdrażania toomanage usługi platformy Azure i skalowanie automatyczne maszyn wirtualnych, planowanie zadań, odzyskiwania po awarii, przenoszenia danych, zależności zarządzania i wdrażania aplikacji. |

## <a name="azure-services-for-big-compute"></a>Usługi Azure dla dużych obliczeń
Poniżej przedstawiono więcej informacji na temat hello obliczeń, dane, sieci i powiązane usługi, które można łączyć Big obliczeniowe rozwiązań i przepływów pracy. Aby uzyskać szczegółowe wskazówki dotyczące usług Azure, zobacz hello usług Azure [dokumentacji](https://azure.microsoft.com/documentation/). Witaj [scenariusze](#scenarios) wcześniej w tym artykule przedstawiono kilka sposoby używania tych usług.

> [!NOTE]
> Na platformie Azure są systematycznie wprowadzane nowe usługi, które mogą okazać się przydatne w danym scenariuszu. Jeśli masz pytania, skontaktuj się z [partnerem Azure](https://pinpoint.microsoft.com/en-US/search?keyword=azure) lub wyślij wiadomość e-mail na adres *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Usługi obliczeniowe
Usługi obliczeń platformy Azure są core hello rozwiązania obliczeniowe duży i hello obliczeń różnych usług Oferta korzyści dla różnych scenariuszy. Na poziomie podstawowym usługi te oferują różne tryby aplikacji toorun na wystąpienia obliczeniowe na podstawie maszyny wirtualnej, przez platformę Azure przy użyciu technologii Hyper-V dla systemu Windows Server. W tych wystąpieniach można uruchamiać standardowe i niestandardowe systemy operacyjne Linux i Windows oraz obsługiwane w nich narzędzia. Platforma Azure umożliwia wybór [rozmiarów wystąpień](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) z różnymi konfiguracjami rdzeni procesora CPU, pamięci, pojemności dysku i innych właściwościach. W zależności od potrzeb można skalować toothousands wystąpień hello rdzeni i następnie skalować w dół, gdy potrzebne są mniej zasobów.

> [!NOTE]
> Zalety hello Azure [obliczeniowych obiektów, takich jak hello H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove hello wydajności i skalowalności HPC obciążeń. Te wystąpienia obsługują także równoległe aplikacje MPI, które wymagają sieci aplikacji o wysokiej wydajności i małym opóźnieniu. Ponadto dostępne są [N-series](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) maszyn wirtualnych o NVIDIA GPU tooexpand hello zakresu scenariuszy dotyczących przetwarzania danych i wizualizacji na platformie Azure.  
> 
> 

| Usługa | Opis |
| --- | --- |
| **[Maszyny wirtualne](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Zapewniają infrastrukturę obliczeniową typu infrastruktura jako usługa (IaaS) przy użyciu technologii Microsoft Hyper-V.<br/><br/>• Pozwalają tooflexibly udostępniania i zarządzać komputerami trwałe chmury standardowe obrazów systemu Windows Server lub Linux z hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/), lub obrazów i dysków z danymi należy podać<br/><br/>• Mogą być wdrożone i zarządzane jako [zestawy skalowania maszyny Wirtualnej](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild na dużą skalę usług z wiele identycznych maszyn wirtualnych, skalowanie automatyczne tooincrease lub zmniejszenia pojemności automatycznie<br/><br/>• Lokalnie obliczeniowe klastra narzędzi i aplikacji całkowicie w chmurze hello<br/><br/> |
| **[Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Mogą uruchamiać aplikacje funkcji dużych obliczeń w wystąpieniach roli procesu roboczego, które są maszynami wirtualnymi z uruchomioną wersją systemu Windows Server i są zarządzane w całości na platformie Azure.<br/><br/>• Włączają skalowalne, niezawodne aplikacje o niskim obciążeniu administracyjnym, działające w ramach modelu typu platforma jako usługa (PaaS).<br/><br/>• Może wymagać dodatkowych narzędzi lub toointegrate programowanie z lokalnymi rozwiązaniami klastra HPC |
| **[Batch](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Uruchamia obciążenia równoległe i partie zadań na dużą skalę w pełni zarządzanej usłudze.<br/><br/>• Służy do planowania i skalowania automatycznego zadań zarządzanej puli maszyn wirtualnych.<br/><br/>• Umożliwia deweloperom aplikacji toobuild i Uruchom jako usługi lub chmury Włącz istniejących aplikacji<br/> |

### <a name="storage-services"></a>Usługi Storage
Rozwiązanie dużych obliczeń działa zazwyczaj na zestawie danych wejściowych i generuje dane w celu uzyskania wyników. Oto niektóre z usług magazynu Azure hello używanych w rozwiązaniach Big obliczeniowe:

* [Obiekt blob, tabela i Queue Storage](https://azure.microsoft.com/documentation/services/storage/) — do zarządzania dużymi ilościami danych niestrukturalnych, danych NoSQL oraz komunikatów dla przepływów pracy i komunikacji. Na przykład może używać magazynu obiektów blob dla dużych zestawów danych technicznych lub obrazy wejściowe hello lub pliki multimedialne procesów aplikacji. Kolejek można użyć do komunikacji asynchronicznej w ramach rozwiązania. Zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md).
* [Magazyn plików Azure](https://azure.microsoft.com/services/storage/files/) -udziałów wspólne pliki i dane w Azure przy użyciu standardowego protokołu SMB, potrzebnego do rozwiązania klastra HPC hello.
* [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) — zapewnia informatycznych rozproszonego systemu plików Apache Hadoop hello chmury, przydatne w przypadku partii, w czasie rzeczywistym i interaktywne analytics.

### <a name="data-and-analysis-services"></a>Usługi danych i analizy
Niektóre scenariusze funkcji dużych obliczeń obejmują przepływy danych na dużą skalę lub generowanie danych wymagających dalszego przetwarzania lub analizy. Platforma Azure udostępnia kilka usług danych i analizy, w tym:

* [Fabryka danych](https://azure.microsoft.com/documentation/services/data-factory/) — tworzy przepływy pracy oparte na danych (potoki), które dołączają, agregują i przekształcają dane z lokalnych, opartych na chmurze oraz internetowych magazynów danych.
* [Baza danych SQL](https://azure.microsoft.com/documentation/services/sql-database/) — zawiera najważniejsze funkcje hello systemu zarządzania relacyjnymi bazami danych programu Microsoft SQL Server w zarządzanych usług.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) — wdraża oraz inicjuje ich obsługę systemu Windows Server lub platformy Apache Hadoop opartej na systemie Linux klastrów w hello toomanage w chmurze, analizy i raportowania danych big data.
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) — ułatwia tworzenie, testowanie i obsługę rozwiązań z zakresu analiz predykcyjnych oraz zarządzanie nimi w ramach w pełni zarządzanej usługi.

### <a name="additional-services"></a>Usługi dodatkowe
Rozwiązania Big obliczeniowe mogą wymagać innych usług Azure tooconnect tooresources lokalnie lub w innych środowiskach. Przykłady:

* [Sieć wirtualna](https://azure.microsoft.com/documentation/services/virtual-network/) — tworzy logicznie odizolowane sekcji tooeach zasobów Azure Azure tooconnect innych lub tooyour lokalnego centrum danych. Dzięki sieci wirtualnej obejmującej wiele lokalizacji aplikacje dużych obliczeń mogą uzyskać dostęp do danych lokalnych, usług Active Directory i serwerów licencji.
* Usługa [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) umożliwia tworzenie prywatnych połączeń między centrami danych firmy Microsoft i infrastrukturą lokalną lub działającą we wspólnej lokalizacji. ExpressRoute zapewnia wyższy poziom zabezpieczeń, więcej niezawodności szybkości szybsze i opóźnienia niższa niż typowe połączenia za pośrednictwem Internetu hello.
* [Usługa Service Bus](https://azure.microsoft.com/documentation/services/service-bus/) — udostępnia kilka mechanizmów dla aplikacji toocommunicate lub wymiany danych, czy znajdują się na platformie Azure, w innej platformy w chmurze lub w centrum danych.

## <a name="next-steps"></a>Następne kroki
* Zobacz [zasobów technicznych partii i HPC](big-compute-resources.md) toobuild wskazówki techniczne toofind rozwiązania.
* Omów opcje Azure (takie jak Cycle Computing, Rescale czy UberCloud) z partnerami.
* Przeczytaj informacje o rozwiązaniach funkcji dużych obliczeń Azure oferowanych przez firmy [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) oraz [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Dla hello najnowsze anonsów, zobacz hello [blog zespołu programu Microsoft HPC i partii](http://blogs.technet.com/b/windowshpc/) i hello [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
