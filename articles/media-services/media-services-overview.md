---
title: "Omówienie usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie usługi Azure Media Services"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Omówienie usługi Azure Media Services 

Microsoft Azure Media Services to rozszerzalna platforma oparte na chmurze, która umożliwia deweloperom toobuild nośnika skalowalne zarządzanie i dostarczania aplikacji. Media Services są oparte na interfejsach API REST umożliwiające przekazywanie toosecurely, przechowywanie, kodowanie i pakietów zawartości wideo lub audio zarówno na żądanie i na żywo przesyłania strumieniowego dostarczania toovarious klientów (na przykład TV, PC i urządzeń przenośnych).

Korzystając wyłącznie z usługi Media Services, można tworzyć kompleksowe przepływy pracy. Możesz również toouse składników innych firm dla niektórych części przepływu pracy. Na przykład kodowanie można wykonać przy użyciu kodera innego producenta. Natomiast przekazywanie, zabezpieczanie, tworzenie pakietów i dostarczanie można realizować za pomocą usługi Media Services.

Możesz wybrać toostream zawartości na żywo lub dostarczanie zawartości na żądanie. Witaj temat zawiera także linki tooother powiązanych tematów.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
Ścieżki szkoleniowe dotyczące usługi AMS można zobaczyć tutaj:

* [Przepływ pracy transmisji strumieniowej na żywo usługi AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Przepływ pracy transmisji strumieniowej na żądanie usługi AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Wymagania wstępne

toostart przy użyciu usługi Azure Media Services, powinien mieć następujące hello:

* Konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com).
* Konto usługi Azure Media Services. Aby uzyskać więcej informacji, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).
* (Opcjonalnie) Konfigurowanie środowiska deweloperskiego. Wybierz platformę .NET lub interfejs API REST dla środowiska deweloperskiego. Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie środowiska](media-services-dotnet-how-to-use.md).

    Poznaj także sposób zbyt[połączenie programowe tooAMS interfejsu API](media-services-use-aad-auth-to-access-ams-api.md).
* Punkt końcowy przesyłania strumieniowego (standardowy lub Premium) w stanie uruchomionym.  Aby uzyskać więcej informacji, zobacz [Zarządzanie punktami końcowymi przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md)

## <a name="sdks-and-tools"></a>Zestawy SDK i narzędzia

toobuild rozwiązań Media Services, można użyć:

* [Interfejs API REST usługi Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Jeden z zestawów SDK klienta dostępne hello:
    * [Zestaw SDK usługi Azure Media Services dla platformy .NET](https://github.com/Azure/azure-sdk-for-media-services)
    * [Zestaw Azure SDK dla języka Java](https://github.com/Azure/azure-sdk-for-java)
    * [Zestaw Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)
    * [Azure Media Services dla środowiska Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Jest to wersja zestawu Node.js SDK firmy innej niż Microsoft. On obsługiwany przez społeczność i aktualnie nie ma 100 pokrycie hello interfejsów API usług AMS).
* Istniejące narzędzia:
    * [Azure Portal](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) to aplikacja Winforms/C# dla systemu Windows)

## <a name="concepts-and-overview"></a>Pojęcia i omówienie
Pojęcia związane z usługą Azure Media Services zostały przedstawione w temacie [Pojęcia](media-services-concepts.md).

Aby uzyskać jak tooseries wprowadzającej tooall hello głównymi składnikami usługi Azure Media Services, zobacz [samouczki krok po kroku Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Seria zawiera wszechstronne omówienie pojęć i używa zadań toodemonstrate AMS narzędzia AMSE hello. AMSE to narzędzie systemu Windows. To narzędzie obsługuje większość zadań hello można wykonać programowo przy użyciu [AMS SDK dla platformy .NET](https://github.com/Azure/azure-sdk-for-media-services), [zestawu Azure SDK dla języka Java](https://github.com/Azure/azure-sdk-for-java), lub [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Obsługiwane scenariusze i dostępność usługi Media Services w centrach danych

Aby uzyskać szczegółowe informacje, zobacz temat [Scenariusze oraz dostępność funkcji i usług AMS w centrach danych](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Umowa dotycząca poziomu usług (SLA)

* W przypadku usługi Media Services Encoding gwarantujemy dostępność transakcji interfejsu API REST na poziomie 99,9%.
* W zakresie przesyłania strumieniowego zapewniamy pomyślną obsługę żądań z gwarancją dostępności na poziomie 99,9% dla istniejącej zawartości multimedialnej w przypadku zakupu standardowego punktu końcowego przesyłania strumieniowego lub punktu końcowego przesyłania strumieniowego Premium.
* Dla kanałów na żywo gwarantujemy, że uruchomione kanały będą utrzymywać łączność zewnętrzną co najmniej 99,9% czasu hello.
* Content Protection gwarantujemy, że pomyślną realizację żądań kluczy co najmniej 99,9% czasu hello.
* Dla odniesieniu do indeksatora zapewniamy pomyślną realizację żądań zadań indeksatora przetwarzanych z zastrzeżone kodowanie jednostki 99,9% czasu hello.

Aby uzyskać więcej informacji, zobacz temat [Umowy dotyczące poziomu usług platformy Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [Avaiability](scenarios-and-availability.md#availability) sekcji.

## <a name="support"></a>Pomoc techniczna

[Pomoc techniczna platformy Azure](https://azure.microsoft.com/support/options/) zapewnia opcje wsparcia technicznego dla platformy Azure, w tym dla usługi Media Services.

## <a name="provide-feedback"></a>Przekazywanie opinii

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
