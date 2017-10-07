---
title: "Omówienie modelu programowania sieci szkieletowej aaaService | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług oferuje dwie struktury umożliwiający tworzenie usług: hello aktora framework i hello usługi framework. Oferują one kompromisy różne prostoty i kontroli."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Omówienie modelu programowania sieci szkieletowej usług
Sieć szkieletowa usług oferuje wiele sposobów toowrite i zarządzania usługami. Usługi można wybrać hello toouse interfejsów API usługi Service Fabric tootake pełne korzystanie z funkcji i platform aplikacji hello platformy. Można także skompilowany program wykonywalny napisane w dowolnym języku lub kodu uruchamianego w kontenerze, po prostu hostowanych w klastrze usługi sieć szkieletowa usług.

## <a name="guest-executables"></a>Pliki wykonywalne gościa
A [pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md) jest istniejące, dowolnego pliku wykonywalnego (zapisany w dowolnym języku) może zostać uruchomiony jako usługa w aplikacji. Pliki wykonywalne gościa należy wywoływać bezpośrednio hello interfejsów API zestawu SDK sieci szkieletowej usług. Jednak są nadal korzystać z funkcji hello platformy oferuje, takie jak usługi odnajdywania, niestandardowe kondycji i obciążenia raportowania przez wywoływanie interfejsów API REST udostępnianych przez usługi sieć szkieletowa usług. Mają one również pełny cykl życia pomocy technicznej.

Wprowadzenie do plików wykonywalnych gościa przez wdrożenie pierwszego [aplikacja wykonywalna gościa](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Kontenery
Domyślnie usługi sieć szkieletowa wdraża i aktywuje usługi jako procesów. Sieć szkieletowa usług można także wdrożyć usług w [kontenery](service-fabric-containers-overview.md). Sieć szkieletowa usług obsługuje wdrażanie kontenery systemu Linux i kontenery systemu Windows w systemie Windows Server 2016. Kontener obrazów można ściągnąć z dowolnym repozytorium kontenera i wdrożyć toohello maszyny. Istniejące aplikacje można wdrożyć jako gość exectuables, sieć szkieletowa usług bezstanowych i stanowych niezawodne usługi lub Reliable Actors w kontenerach, a można mieszać usług w procesach i usług w kontenerach w hello tej samej aplikacji.

[Dowiedz się więcej o containerizing usług w systemie Windows lub Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Niezawodne usługi to platforma lekki dla usług, które integrują się z platformy sieć szkieletowa usług hello i korzystać z pełnego zestawu funkcji platformy hello zapisu. Niezawodne usługi zapewniają minimalny zestaw interfejsów API zezwalające na powitania sieci szkieletowej usług środowiska uruchomieniowego toomanage hello cyklem życia usługi i korzystający z usług toointeract ze środowiskiem uruchomieniowym hello. Struktura aplikacji Hello jest minimalny, umożliwiając pełną kontrolę nad opcje projektowania i implementacji i może być używane toohost wszelkie inne struktury aplikacji, takich jak ASP.NET Core.

Niezawodne usługi może być toomost bezstanowych, podobne usługi platform, takich jak serwery sieci web, w których każde wystąpienie usługi hello jest tworzony taki sam, a w zewnętrznych rozwiązania, takie jak bazy danych platformy Azure lub magazynu tabel platformy Azure jest trwały stan.

Niezawodne usługi mogą być również stanowe, wyłącznego tooService sieci szkieletowej, gdzie bezpośrednio w samej przy użyciu kolekcji niezawodnej usługi hello jest trwały stan. Stanu wprowadzone wysokiej dostępności przy użyciu replikacji i dystrybuowane za pośrednictwem partycje, wszystkie zarządzane automatycznie przez sieć szkieletowa usług.

[Dowiedz się więcej o usługach Reliable Services](service-fabric-reliable-services-introduction.md) lub Rozpoczynanie pracy przez [pisanie pierwszej usługi niezawodnego](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Wbudowane niezawodne usługi, framework niezawodnego aktora hello jest struktury aplikacji, która implementuje wzorca aktora wirtualnego hello, oparte na wzorcu projektowym aktora hello. Platforma niezawodnego aktora Hello korzysta niezależne jednostki zasobów obliczeniowych i stan z jednowątkowego wykonywania o nazwie złośliwych użytkowników. Witaj niezawodnego aktora framework zapewnia komunikacji wbudowanej złośliwych użytkowników i wstępnie ustawiony stan stanu trwałego i skalowalnego w poziomie konfiguracji.

Reliable Actors sam jest struktury aplikacji w oparciu niezawodne usługi, pełni jest zintegrowany z platformy sieć szkieletowa usług hello i korzysta z pełnego zestawu funkcji oferowanych przez platformę hello hello.

[Dowiedz się więcej o Reliable Actors](service-fabric-reliable-actors-introduction.md) lub Rozpoczynanie pracy przez [pisanie pierwszej usługi niezawodnego aktora](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Core
Sieć szkieletowa usług integruje się z [platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) do tworzenia usług sieci Web i interfejsu API, które mogą być dołączane jako część aplikacji. 

[Tworzenie usługi frontonu przy użyciu platformy ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Następne kroki
[Omówienie sieci szkieletowej usług i kontenerów](service-fabric-containers-overview.md)

[Niezawodne usługi — omówienie](service-fabric-reliable-services-introduction.md)

[Niezawodne usługi — omówienie](service-fabric-reliable-actors-introduction.md)

[Sieć szkieletowa usług i ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)




