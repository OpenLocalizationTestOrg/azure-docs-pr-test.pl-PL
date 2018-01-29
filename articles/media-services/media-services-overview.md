---
title: "Omówienie usługi Azure Media Services | Microsoft Docs"
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
ms.date: 10/24/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 4cec6db8b05fa0023cc0166726159b1ec2de8edb
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="azure-media-services-overview"></a>Omówienie usługi Azure Media Services 

Microsoft Azure Media Services to oparta na chmurze rozszerzona platforma, która umożliwia deweloperom tworzenie skalowalnych aplikacji do dostarczania multimediów i zarządzania nimi. Usługi Media Services są oparte na interfejsach API REST, które umożliwiają bezpieczne przekazywanie, przechowywanie, kodowanie i tworzenie pakietów zawartości wideo lub audio na potrzeby transmisji strumieniowej na żądanie i na żywo do różnych klientów (np. odbiorników TV, komputerów i urządzeń przenośnych).

Korzystając wyłącznie z usługi Media Services, można tworzyć kompleksowe przepływy pracy. W przypadku niektórych części przepływu pracy można użyć składników innych firm. Na przykład kodowanie można wykonać przy użyciu kodera innego producenta. Natomiast przekazywanie, zabezpieczanie, tworzenie pakietów i dostarczanie można realizować za pomocą usługi Media Services.

Możliwe jest przesyłanie strumieniowe zawartości na żywo lub dostarczanie zawartości na żądanie. Temat zawiera także linki do innych powiązanych tematów.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
Ścieżki szkoleniowe dotyczące usługi AMS można zobaczyć tutaj:

* [Przepływ pracy transmisji strumieniowej na żywo usługi AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Przepływ pracy transmisji strumieniowej na żądanie usługi AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Wymagania wstępne

Do rozpoczęcia korzystania z usługi Azure Media Services potrzebne są:

* Konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com).
* Konto usługi Azure Media Services. Aby uzyskać więcej informacji, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).
* (Opcjonalnie) Konfigurowanie środowiska deweloperskiego. Wybierz platformę .NET lub interfejs API REST dla środowiska deweloperskiego. Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie środowiska](media-services-dotnet-how-to-use.md).

    Dowiedz się także, jak [programowo ustanawiać połączenie z interfejsem API usługi AMS](media-services-use-aad-auth-to-access-ams-api.md).
* Punkt końcowy przesyłania strumieniowego (standardowy lub Premium) w stanie uruchomionym.  Aby uzyskać więcej informacji, zobacz [Zarządzanie punktami końcowymi przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md)

## <a name="sdks-and-tools"></a>Zestawy SDK i narzędzia

W celu tworzenia rozwiązań Media Services można użyć następujących elementów:

* [Interfejs API REST usługi Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Jeden z dostępnych zestawów SDK klienta:
    * [Zestaw SDK usługi Azure Media Services dla platformy .NET](https://github.com/Azure/azure-sdk-for-media-services)
    * [Zestaw Azure SDK dla języka Java](https://github.com/Azure/azure-sdk-for-java)
    * [Zestaw Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)
    * [Azure Media Services dla środowiska Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Jest to wersja zestawu Node.js SDK firmy innej niż Microsoft. Jest ona opracowywana przez społeczność i aktualnie nie obsługuje 100% interfejsów API usług AMS.)
* Istniejące narzędzia:
    * [Azure Portal](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) to aplikacja Winforms/C# dla systemu Windows)

> [!NOTE]
> Aby uzyskać najnowszą wersję zestawu SDK języka Java i zacząć programować w języku Java, zobacz [Rozpoczynanie korzystania z zestawu SDK klienta Java dla usług Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> Aby pobrać najnowszy zestaw SDK języka PHP dla usługi Media Services, poszukaj wersji 0.5.7 pakietu Microsoft/WindowAzure w [repozytorium Packagist](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="code-samples"></a>Przykłady kodu

Wiele przykładów kodu możesz znaleźć w galerii **Przykłady kodu platformy Azure**: [Przykłady kodu usługi Azure Media Services](https://azure.microsoft.com/resources/samples/?service=media-services&sort=0).

## <a name="concepts"></a>Pojęcia

Pojęcia związane z usługą Azure Media Services zostały przedstawione w temacie [Pojęcia](media-services-concepts.md).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Obsługiwane scenariusze i dostępność usługi Media Services w centrach danych

Aby uzyskać szczegółowe informacje, zobacz temat [Scenariusze oraz dostępność funkcji i usług AMS w centrach danych](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Umowa dotycząca poziomu usług (SLA)

* W przypadku usługi Media Services Encoding gwarantujemy dostępność transakcji interfejsu API REST na poziomie 99,9%.
* W zakresie przesyłania strumieniowego zapewniamy pomyślną obsługę żądań z gwarancją dostępności na poziomie 99,9% dla istniejącej zawartości multimedialnej w przypadku zakupu standardowego punktu końcowego przesyłania strumieniowego lub punktu końcowego przesyłania strumieniowego Premium.
* W odniesieniu do kanałów na żywo gwarantujemy, że uruchomione kanały będą utrzymywać łączność zewnętrzną przez co najmniej 99,9% czasu.
* W usłudze Content Protection gwarantujemy pomyślną realizację żądań kluczy przez co najmniej 99,9% czasu.
* Dla odniesieniu do indeksatora zapewniamy pomyślną realizację żądań zadań indeksatora przetwarzanych przez jednostkę zarezerwowaną do celów związanych z kodowaniem przez 99,9% czasu.

Aby uzyskać więcej informacji, zobacz temat [Umowy dotyczące poziomu usług platformy Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Aby uzyskać informacje na temat dostępności w centrach danych, zobacz sekcję [Dostępność](scenarios-and-availability.md#availability).

## <a name="support"></a>Pomoc techniczna

[Pomoc techniczna platformy Azure](https://azure.microsoft.com/support/options/) zapewnia opcje wsparcia technicznego dla platformy Azure, w tym dla usługi Media Services.

## <a name="provide-feedback"></a>Przekazywanie opinii

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
