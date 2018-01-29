---
title: "Omówienie usługi aplikacji: Azure stosu | Dokumentacja firmy Microsoft"
description: "Omówienie usługi aplikacji Azure stosu"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/10/2017
ms.author: anwestg
ms.openlocfilehash: fd2d355b2556faddb06acf2998b54ffcc9aa7919
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2017
---
# <a name="app-service-on-azure-stack-overview"></a>Omówienie usługi App Service w usłudze Azure Stack

Usługa aplikacji Azure na stosie Azure jest ofertę platformy jako — usługa (PaaS) systemu Microsoft Azure dostępnych do stosu Azure. Usługa umożliwia klientom — wewnętrzne lub zewnętrzne — tworzenie sieci web, interfejsu API i usługi Azure Functions aplikacje dla dowolnej platformy lub urządzenia. Mogą pozwala integrować aplikacje z aplikacjami lokalnymi i automatyzację procesów biznesowych. Operatorzy chmury stosu Azure mogą korzystać z aplikacji klienta w pełni zarządzanych maszynach wirtualnych (VM), z ich wyboru udostępnianych zasobów maszyn lub dedykowanych maszyn wirtualnych.

Usługa aplikacji Azure zawiera funkcje do automatyzacji procesów biznesowych i hostowania interfejsów API w chmurze. Jako pojedyncza zintegrowana usługa Azure App Service umożliwia korzystanie z różnych składników — witryn sieci Web, interfejsy API RESTful i procesów biznesowych — w ramach jednego rozwiązania.

## <a name="why-offer-azure-app-service-on-azure-stack"></a>Dlaczego oferuje usługi Azure App Service na stosie Azure?

Poniżej przedstawiono niektóre najważniejszych funkcji i możliwości usługi App Service:
- **Wiele języków i struktur**: Usługa App Service oferuje najwyższej jakości pomoc techniczną dla platformy ASP.NET, Node.js, Java, PHP i Python. Można również uruchomić środowiska Windows PowerShell oraz inne skrypty lub pliki wykonywalne na maszynach wirtualnych usługi App Service.
- **Optymalizacja metodyki DevOps**: Konfigurowanie ciągłej integracji i wdrażanie za pomocą usługi GitHub, lokalne Git lub BitBucket. Promowanie aktualizacji za pomocą środowisk testowych i przejściowych. Zarządzanie aplikacjami w usłudze App Service przy użyciu programu Azure PowerShell lub międzyplatformowego interfejsu wiersza polecenia (CLI).
- **Integracja z programem Visual Studio**: dedykowane narzędzia w programie Visual Studio usprawniają procesy tworzenia i wdrażania aplikacji.

## <a name="app-types-in-app-service"></a>Typy aplikacji w usłudze App Service

Usługa App Service oferuje kilka typów aplikacji, z których każdy jest przeznaczony do obsługi określonego obciążenia:

- [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) do obsługi aplikacji sieci web i witryn sieci Web.
- [Aplikacje interfejsu API](https://docs.microsoft.com/azure/app-service-api/app-service-api-apps-why-best-platform) do hostowania interfejsów API RESTful.
- Środowisko Azure Functions do hostowania zdarzeniami, niekorzystającą obciążeń.

W tym miejscu aplikacji word odwołuje się do zasobów hostowania przeznaczonych do obsługi obciążenia. Na przykład wyrażenie „aplikacja sieci Web” kojarzy się prawdopodobnie z zasobami obliczeniowymi i kodem aplikacji, które łącznie realizują funkcje używane w przeglądarce. Jednak w usłudze App Service aplikacji sieci web jest zasoby obliczeniowe, które udostępnia stosu Azure do hostowania kodu aplikacji.

Aplikacja może składać się z wielu aplikacji usługi App Service różnego rodzaju. Na przykład jeśli aplikacja składa się z frontonu sieci web i zakończeniu interfejsu API RESTful Wstecz, możesz:
- Wdrożyć oba rozwiązania (fronton i interfejs API) w jednej aplikacji sieci Web.
- Wdrożyć kod frontonu w aplikacji sieci Web i kod zaplecza w aplikacji interfejsu API.

   ![](media/azure-stack-app-service-overview/image01.png)

## <a name="what-is-an-app-service-plan"></a>Co to jest plan usługi App Service?

Dostawcy zasobów usługi aplikacji używa tego samego kodu, który używa usługi Azure App Service. W związku z tym niektóre typowe pojęcia są warto opisujące. W usłudze App Service cenową kontener dla aplikacji nosi nazwę planu usługi aplikacji. Reprezentuje zestaw dedykowanych maszyn wirtualnych, które służy do przechowywania aplikacji. W ramach danej subskrypcji może mieć wiele planów usługi aplikacji.

Na platformie Azure Brak udostępnionego i dedykowanych procesów roboczych. Obsługuje udostępnionego procesu roboczego obsługującego o wysokiej gęstości wielodostępnych aplikacji, a istnieje tylko jeden zestaw udostępnionego pracowników. Dedykowanych serwerów są używane przez tylko jednego dzierżawcy i są dostępne w trzech rozmiarach: mały, średni i duży. Potrzeb klientów lokalnych nie zawsze opisana przy użyciu tych warunków. W usłudze aplikacji Azure stosu Administratorzy dostawcy zasobów można zdefiniować warstw procesu roboczego, które mają być dostępne. Oparte na unikalne potrzeby hostingu, można zdefiniować wiele zestawów pracowników udostępnionego lub różnych zestawów dedykowanych procesów roboczych. Korzystając z tych definicji warstwy procesu roboczego, ich może następnie zdefiniować własne cennik jednostki SKU.

## <a name="portal-features"></a>Funkcje portalu

Usługi aplikacji Azure stosu używa ten sam interfejs użytkownika, które używa usługi Azure App Service, podobnie jak na zapleczu. Niektóre funkcje są wyłączone i nie są funkcjonalne w stosie Azure. Oczekiwań specyficzne dla platformy Azure lub usługi, które wymagają te funkcje nie są jeszcze dostępne w stosie Azure.

## <a name="next-steps"></a>Następne kroki


- [Przed rozpoczęciem pracy z usługi aplikacji Azure stosu](azure-stack-app-service-before-you-get-started.md)
- [Zainstaluj dostawcę zasobów usługi aplikacji](azure-stack-app-service-deploy.md)

Możesz również wypróbować innych [platforma jako usługa (PaaS) usługi](azure-stack-tools-paas-services.md), takiej jak [dostawcy zasobów programu SQL Server](azure-stack-sql-resource-provider-deploy.md) i [dostawcy zasobów MySQL](azure-stack-mysql-resource-provider-deploy.md).
