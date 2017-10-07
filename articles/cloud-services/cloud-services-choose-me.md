---
title: "Opcje - usługi w chmurze obliczania aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hostingu opcje i jak działają obliczeń platformy Azure: App Service, Cloud Services i maszyny wirtualne"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Należy wybrać usługi w chmurze lub coś innego?
Usługi w chmurze Azure hello wybór jest dla Ciebie? Platforma Azure oferuje różne modele hostingu uruchamiania aplikacji. Każda z nich zapewnia inny zestaw usług, więc która z nich wybierzesz zależy od tego, dokładnie co próbujesz toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Podaj informacje o usługi w chmurze
Usługi w chmurze jest przykładem [platforma jako usługa](https://azure.microsoft.com/overview/what-is-paas/) (PaaS). Podobnie jak [usługi aplikacji](../app-service-web/app-service-web-overview.md), ta technologia jest zaprojektowana toosupport aplikacji, które są skalowalne, niezawodne i tanie toooperate. Podobnie jak usługi aplikacji znajduje się na maszynach wirtualnych, więc są zbyt usługi w chmurze, jednak masz większą kontrolę nad hello maszyn wirtualnych. Można zainstalować lokalnie własne oprogramowanie na maszynach wirtualnych usługi chmury, a także zdalnego do nich.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Większa kontrola oznacza również mniej łatwość użycia. Jeśli nie potrzebujesz hello kontroli dodatkowe opcje, jest zwykle szybsze i łatwiejsze tooget aplikacji sieci web i tooCloud usług uruchomionych w aplikacji sieci Web w usłudze App Service w porównaniu.

Istnieją dwa rodzaje ról usługi w chmurze. Hello jedyna różnica między hello dwa jest sposób roli użytkownika jest hostowana na maszynie wirtualnej hello.

* **Rola sieci Web**  
Automatycznie wdraża i hostuje aplikację za pośrednictwem usług IIS.

* **Rola procesu roboczego**  
Nie korzysta z usług IIS i uruchamia autonomiczny Twojej aplikacji.

Prosta aplikacja może na przykład użyć tylko jednego rolę sieci web, obsługująca witryny sieci Web. Bardziej złożonych aplikacji mogą używać toohandle roli sieci web przychodzące żądania od użytkowników, następnie przekaż te żądania na tooa roli procesu roboczego do przetwarzania. (Można użyć tej komunikacji [usługi Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) lub [kolejek Azure](../storage/common/storage-introduction.md).)

Jako hello powyższej ilustracji sugeruje, hello wszystkie maszyny wirtualne w jednej aplikacji uruchamiane w hello sama usługa w chmurze. Aplikacji hello dostępu użytkowników za pomocą pojedynczego publicznego adresu IP, z żądaniami automatycznie zrównoważonym obciążeniu na maszynach wirtualnych hello aplikacji. Platforma Hello [skaluje i wdraża](cloud-services-how-to-scale.md) hello maszyn wirtualnych w aplikacji usługi w chmurze w taki sposób, który pozwala uniknąć pojedynczy punkt awarii sprzętowej.

Mimo że aplikacje są uruchamiane na maszynach wirtualnych, jest ważne toounderstand, że usługi w chmurze zapewnia PaaS, nie IaaS. W tym miejscu jest jednym ze sposobów toothink o: Z IaaS, takich jak maszyny wirtualne Azure należy najpierw utworzyć i skonfigurować środowisko hello aplikacja działa w, a następnie wdrożyć aplikację w tym środowisku. Wszystko jest odpowiedzialny za zarządzanie znacznie tego world funkcji, takich jak wdrażanie nowych poprawioną wersji systemu operacyjnego hello w każdej maszyny Wirtualnej. W PaaS natomiast jest tak, jakby hello środowisko już istnieje. Wszystkie masz toodo, jest wdrażanie aplikacji. Zarządzanie platformy hello jest uruchamiany na, takich jak wdrażanie nowych wersji systemu operacyjnego hello jest już obsługiwane.

## <a name="scaling-and-management"></a>Skalowanie i zarządzanie
Usługi w chmurze nie Tworzenie maszyn wirtualnych. Zamiast tego Podaj pliku konfiguracji, który informuje Azure, ile ma się, takich jak **trzy wystąpienia ról sieci web** i **dwa wystąpienia roli procesu roboczego**, i platformy hello utworzy je.  Wybierz nadal [jaki rozmiar](cloud-services-sizes-specs.md) tych kopii maszyn wirtualnych powinny być, ale nie jawnie tworzyć je samodzielnie. Jeśli aplikacja wymaga toohandle większe obciążenie, może poprosić o więcej maszyn wirtualnych, a system Azure utworzy tych wystąpień. Jeśli zmniejsza obciążenie hello, możesz zamknąć te wystąpienia i Zatrzymaj płatności dla nich.

Aplikacja usługi w chmurze zwykle obejmuje toousers dostępne za pośrednictwem dwuetapowego procesu. Projektant pierwszy [aplikacji hello przekazywania](cloud-services-how-to-create-deploy.md) toohello platformy na obszarze tymczasowym. Gdy hello developer jest gotowy aplikacji hello toomake na żywo, korzystają z hello Azure tooswap portalu przemieszczania z produkcji. To [przełączanie między tymczasowych i produkcyjnych](cloud-services-nodejs-stage-application.md) może odbywać się bez przestojów, co pozwala działającej aplikacji jest nowa wersja uaktualniona tooa bez zakłócania jego użytkowników.

## <a name="monitoring"></a>Monitorowanie
Usługi w chmurze zapewnia również monitorowanie. Podobnie jak maszyny wirtualne Azure wykryje nie powiodło się serwerze fizycznym i uruchamia ponownie hello maszyn wirtualnych, które były uruchomione na tym serwerze, na nowych komputerach. Jednak usługi w chmurze wykrywa również nie powiodło się maszyn wirtualnych i aplikacji, nie tylko na awarie sprzętowe. W przeciwieństwie do maszyn wirtualnych składa się z agentem wewnątrz każdej roli sieci web i proces roboczy, a jest możliwe toostart nowych maszyn wirtualnych i wystąpień aplikacji w przypadku wystąpienia awarii.

Witaj PaaS rodzaj usługi w chmurze ma zbyt innych skutków. Jednym z najważniejszych hello jest czy aplikacje oparte na technologii ten powinien być zapisywany toorun poprawnie gdy wystąpienie roli sieci web lub procesu roboczego nie powiodło się. tooachieve to usługi w chmurze aplikacji nie powinien obsługiwać prezentować hello system plików własnych maszyn wirtualnych. W odróżnieniu od maszyny wirtualne utworzone z maszyn wirtualnych platformy Azure zapisy wprowadzone maszyn wirtualnych usługi tooCloud nie są trwałe; Brak nie przypomina dysku danych maszyny wirtualnej. Zamiast tego usługi w chmurze aplikacji należy jawnie zapisać wszystkie tooSQL stan bazy danych, obiektów blob, tabel lub innych magazynu zewnętrznego. Tworzenie aplikacji w ten sposób sprawia, że ich tooscale łatwiejsze i bardziej odporne toofailure zarówno ważne celów usługi w chmurze.

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji usługi w chmurze w .NET](cloud-services-dotnet-get-started.md)  
[Tworzenie aplikacji usługi w chmurze w środowisku Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Tworzenie aplikacji usługi w chmurze w języku PHP](../cloud-services-php-create-web-role.md)  
[Tworzenie aplikacji usługi w chmurze w języku Python](cloud-services-python-ptvs.md)

