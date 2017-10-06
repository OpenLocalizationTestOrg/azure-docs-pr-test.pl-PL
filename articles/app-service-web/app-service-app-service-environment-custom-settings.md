---
title: "Ustawienia aaaCustom dla środowiska usługi App Service"
description: "Niestandardowych ustawień konfiguracji środowiska usługi App Service"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Niestandardowych ustawień konfiguracji środowiska usługi App Service
## <a name="overview"></a>Omówienie
Ponieważ środowiska usługi aplikacji są izolowane tooa jednego odbiorcy, istnieją pewne ustawienia konfiguracji, które mogą być stosowane wyłącznie tooApp środowiska usługi. Ten artykuł dokumenty hello różnych specjalnego dostosowania, które są dostępne dla środowiska usługi App Service.

Jeśli nie masz środowisko usługi aplikacji, zobacz [jak tooCreate środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md).

Dostosowywanie środowiska usługi aplikacji może przechowywać przy użyciu tablicy w hello nowe **clusterSettings** atrybutu. Ten atrybut zostanie znaleziony w słownik "Właściwości" hello hello *hostingEnvironments* jednostki usługi Azure Resource Manager.

Witaj poniższy fragment skróconej szablonu usługi Resource Manager zawiera hello **clusterSettings** atrybutu:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Witaj **clusterSettings** atrybut może być uwzględniany w Resource Manager hello tooupdate szablonu środowiska usługi aplikacji.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Użyj Eksploratora zasobów Azure tooupdate środowiska usługi aplikacji
Alternatywnie można zaktualizować hello środowiska usługi aplikacji przy użyciu [Eksploratora zasobów Azure](https://resources.azure.com).  

1. W Eksploratorze zasobów Przejdź węzła toohello dla środowiska usługi aplikacji hello (**subskrypcje** > **resourceGroups** > **dostawców**  >  **Microsoft.Web** > **hostingEnvironments**). Następnie kliknij przycisk hello określonego środowiska usługi aplikacji, które mają tooupdate.
2. W okienku po prawej stronie powitania, kliknij przycisk **odczytu/zapisu** w tooallow narzędzi u góry hello interakcyjne edycji w Eksploratorze zasobów.  
3. Kliknij przycisk hello niebieski **Edytuj** edycji szablonu usługi Resource Manager hello toomake przycisku.
4. Przewiń w dół toohello hello prawego okienka. Witaj **clusterSettings** atrybut jest bardzo dole hello, gdzie można wprowadzić lub zaktualizować jej wartość.
5. Typ (lub kopiowania i wklejania) hello tablicę wartości konfiguracji w hello **clusterSettings** atrybutu.  
6. Kliknij zielony hello **PUT** przycisku, który ma znajdujący się u góry hello hello prawym okienku toocommit hello zmiany toohello środowiska usługi aplikacji.

Jednak wprowadzane zmiany hello trwa około 30 minut pomnożona przez hello liczba przedniego kończy się hello środowiska usługi aplikacji hello zmiany tootake efektu.
Na przykład jeśli środowiska usługi aplikacji ma cztery zakończenia frontonu, potrwa około dwie godziny dla toofinish aktualizacji konfiguracji hello. Gdy jest Trwa wprowadzanie zmian w konfiguracji hello, nie ma innych operacji skalowania lub operacje zmiany konfiguracji może mieć miejsce w hello środowiska usługi aplikacji.

## <a name="disable-tls-10"></a>Wyłączenie protokołu TLS 1.0
Cyklicznego zapytania od klientów, szczególnie w przypadku klientów, którzy mają do czynienia z zgodności PCI inspekcji, jest sposób tooexplicitly wyłączenie protokołu TLS 1.0 dla swoich aplikacji.

Protokołu TLS 1.0, można wyłączyć za pomocą następujących hello **clusterSettings** wpis:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Zmień kolejność użycia mechanizmów szyfrowania TLS
Następne pytanie od klientów jest Jeśli modyfikują hello lista szyfrów wynegocjowanym przez ich serwer i można to osiągnąć, modyfikując hello **clusterSettings** jak pokazano poniżej. Witaj listę dostępnych mechanizmach szyfrowania można pobrać z [ten artykuł w witrynie MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Jeśli niepoprawne wartości są ustawiane dla hello mechanizmów szyfrowania, który SChannel nie może zrozumieć, wszystkie server tooyour komunikację TLS może przestaną działać. W takim przypadku należy tooremove hello *FrontEndSSLCipherSuiteOrder* wpisu z **clusterSettings** i przesyłanie hello zaktualizowane Menedżera zasobów szablonu toorevert wstecz toohello domyślne szyfrowania Ustawienia pakietu.  Użyj tej funkcji należy z rozwagą.
> 
> 

## <a name="get-started"></a>Rozpoczęcie pracy
Witryna szablon Menedżera zasobów Azure szybkiego startu Hello zawiera szablonu z hello podstawową definicję dla [tworzenie środowiska usługi aplikacji](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
