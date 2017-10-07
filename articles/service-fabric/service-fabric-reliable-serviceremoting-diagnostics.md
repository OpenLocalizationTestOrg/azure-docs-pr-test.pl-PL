---
title: aaaAzure ServiceFabric Diagnostyka i monitorowanie | Dokumentacja firmy Microsoft
description: "W tym artykule opisano hello funkcje monitorowania wydajności w środowisku uruchomieniowym usługi sieć szkieletowa niezawodnej ServiceRemoting hello, jak liczniki wydajności emitowane przez nią."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnostyka i monitorowanie wydajności dla niezawodnego Remoting Service
emituje środowiska uruchomieniowego niezawodnej ServiceRemoting Hello [liczniki wydajności](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Te zapewniają wgląd w działania hello ServiceRemoting i ułatwić rozwiązywanie problemów i monitorowania wydajności.


## <a name="performance-counters"></a>Liczniki wydajności
środowiska uruchomieniowego niezawodnej ServiceRemoting Hello definiuje hello następujących kategorii licznika wydajności:

| Kategoria | Opis |
| --- | --- |
| Usługa sieci szkieletowej usług |Liczniki określone tooAzure Service Fabric Service Remoting, na przykład tooprocess Średni czas żądania |
| Metody usługi sieci szkieletowej usług |Liczniki określone toomethods implementowanych przez usługi sieć szkieletowa usług zdalnych, na przykład częstotliwość wywoływana jest metoda usługi |

Każdy z hello poprzedzających kategorii ma co najmniej jeden licznik.

Witaj [Monitor wydajności systemu Windows](https://technet.microsoft.com/library/cc749249.aspx) aplikacji, która jest dostępna domyślnie w systemie operacyjnym Windows hello mogą być używane dane o liczników wydajności toocollect i widoku. [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) jest inną opcją w przypadku zbierania danych licznika wydajności i przekazać go tooAzure tabel.

### <a name="performance-counter-instance-names"></a>Nazwy wystąpień liczników wydajności
Klaster ma dużą liczbę usług ServiceRemoting lub partycje ma dużą liczbę wystąpień liczników wydajności. wystąpienie licznika wydajności Hello nazwy mogą pomóc w zidentyfikowaniu hello określonej partycji i metody usługi (jeśli dotyczy) danego wystąpienia licznika wydajności hello jest skojarzony.

#### <a name="service-fabric-service-category"></a>Kategoria Usługa sieci szkieletowej usług
Dla kategorii hello `Service Fabric Service`, nazwy wystąpień liczników hello znajdują się w hello następującego formatu:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* jest hello identyfikator partycji usługi sieć szkieletowa hello wystąpienie licznika wydajności jest skojarzony z reprezentację ciągu hello. Identyfikator partycji: Hello jest identyfikatorem GUID i reprezentacji ciągu jest generowany przez hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metody z specyfikator formatu "D".

*ServiceReplicaOrInstanceId* jest reprezentacją ciągu hello hello jest skojarzony identyfikator repliki i wystąpienia sieci szkieletowej usług hello wystąpienie licznika wydajności.

*ServiceRuntimeInternalID* hello reprezentacja ciągu 64-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe usługi sieć szkieletowa hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

Witaj poniżej przedstawiono przykład nazwę wystąpienia licznika licznika, który należy toohello `Service Fabric Service` kategorii:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

W hello poprzedzających przykład `2740af29-78aa-44bc-a20b-7e60fb783264` hello reprezentacja ciągu Identyfikatora partycji usługi sieć szkieletowa hello, `635650083799324046` jest reprezentację ciągu repliki/InstanceId i `5008379932` jest hello 64-bitowy identyfikator, który jest generowany podczas wewnętrznego hello środowiska wykonawczego Użycie.

#### <a name="service-fabric-service-method-category"></a>Kategoria metody usługi sieci szkieletowej usług
Dla kategorii hello `Service Fabric Service Method`, nazwy wystąpień liczników hello znajdują się w hello następującego formatu:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* jest hello Nazwa metody usługi hello hello wystąpienie licznika wydajności jest skojarzony. Hello format nazwy metody hello jest określana w oparciu logikę w środowisku uruchomieniowym usługi sieć szkieletowa hello, który równoważy czytelność hello hello nazwy z ograniczeń hello maksymalna długość nazwy wystąpienia licznika wydajności hello w systemie Windows.

*ServiceRuntimeMethodId* reprezentacja ciąg hello 32-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe usługi sieć szkieletowa hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

*ServiceFabricPartitionID* jest hello identyfikator partycji usługi sieć szkieletowa hello wystąpienie licznika wydajności jest skojarzony z reprezentację ciągu hello. Identyfikator partycji: Hello jest identyfikatorem GUID i reprezentacji ciągu jest generowany przez hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metody z specyfikator formatu "D".

*ServiceReplicaOrInstanceId* jest reprezentacją ciągu hello hello jest skojarzony identyfikator repliki i wystąpienia sieci szkieletowej usług hello wystąpienie licznika wydajności.

*ServiceRuntimeInternalID* hello reprezentacja ciągu 64-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe usługi sieć szkieletowa hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

Witaj poniżej przedstawiono przykład nazwę wystąpienia licznika licznika, który należy toohello `Service Fabric Service Method` kategorii:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

W hello poprzedzających przykład `ivoicemailboxservice.leavemessageasync` jest nazwą metody hello, `2` jest hello używać 32-bitowy identyfikator generowane podczas wewnętrznego hello środowiska uruchomieniowego, `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello reprezentacja ciągu Identyfikatora partycji usługi sieć szkieletowa hello,`635650083804480486` ciąg hello Reprezentacja hello identyfikator repliki/wystąpienia usługi sieci szkieletowej i `5008380` za pomocą hello 64-bitowy identyfikator wygenerować dla środowiska uruchomieniowego hello obiektu wewnętrznego.

## <a name="list-of-performance-counters"></a>Lista liczników wydajności
### <a name="service-method-performance-counters"></a>Liczniki wydajności usług — metoda

środowisko uruchomieniowe niezawodnej usługi Hello publikuje hello następujące liczniki wydajności toohello powiązane wykonywanie metody usługi.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Metody usługi sieci szkieletowej usług |Wywołania na sekundę |Ile razy hello usługi metoda jest wywoływana na sekundę |
| Metody usługi sieci szkieletowej usług |Średnia liczba milisekund dla wywołania |Metoda usługi hello tooexecute czas w milisekundach |
| Metody usługi sieci szkieletowej usług |Wyjątki zgłaszane na sekundę |Ile razy hello metody usługi zwrócił wyjątek na sekundę |

### <a name="service-request-processing-performance-counters"></a>Liczniki wydajności przetwarzania żądania usługi
Gdy klient wywołuje metodę za pośrednictwem obiektu serwera proxy usługi, wynikiem są wysyłane za pośrednictwem usługi remoting toohello sieci hello komunikat żądania. Usługa Hello przetwarza komunikat żądania hello i wysyła klientowi wstecz toohello odpowiedzi. środowiska uruchomieniowego niezawodnej ServiceRemoting Hello publikuje powitania po przetwarzania żądań powiązanych tooservice liczników wydajności.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Usługa sieci szkieletowej usług |Liczba oczekujących żądań |Liczba żądań przetwarzanych w usłudze hello |
| Usługa sieci szkieletowej usług |Średnia liczba milisekund dla żądania |Czas trwania (w milisekundach) tooprocess usługi hello żądania |
| Usługa sieci szkieletowej usług |Średni czas deserializacji żądania (milisekundy) |Czas wykonania (w milisekundach) toodeserialize usługi komunikat żądania po odebraniu hello usługi |
| Usługa sieci szkieletowej usług |Średni czas serializacji odpowiedzi (milisekundy) |Komunikatu odpowiedzi czas wykonania (w milisekundach) tooserialize hello usług Usługa hello przed wysłaniem odpowiedzi powitania klienta toohello |

## <a name="next-steps"></a>Następne kroki
* [Przykładowy kod](https://github.com/Azure/servicefabric-samples)
* [Element EventSource dostawców w narzędzia PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
