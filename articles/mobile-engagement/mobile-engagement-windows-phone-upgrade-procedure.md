---
title: aaaWindows procedur uaktualniania Phone Silverlight SDK
description: "Windows Phone Silverlight SDK procedur uaktualniania dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Windows Phone Silverlight SDK procedur uaktualniania
Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK. Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.

## <a name="from-200-too330"></a>Z 2.0.0 too3.3.0
### <a name="test-logs"></a>Dzienniki testów
Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane. toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>Z 1.1.1 too2.0.0
Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej. Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów
> 
> 

W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.1.1, zastosuj hello procedury

### <a name="nuget-package"></a>Pakiet Nuget
Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.

### <a name="applying-mobile-engagement"></a>Stosowanie usługi Mobile Engagement
Hello SDK używany termin hello `Engagement`. Należy tooupdate toomatch Twojego projektu tej zmiany.

Należy toouninstall bieżącego Capptain pakietu nuget. Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte. Jeśli tookeep tych plików, a następnie utworzyć ich kopię.

Po wykonaniu tej instalacji nowego pakietu nuget usługi Microsoft Azure Engagement hello w projekcie. Można go znaleźć bezpośrednio na [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Zastępuje tej akcji, wszystkich plików zasobów używanych przez usługi Engagement i dodaje nowe tooyour DLL zaangażowania hello projektu odwołań.

Masz tooclean odwołania projektu o usunięcie odwołania do biblioteki DLL Capptain. Jeśli nie wprowadzisz to, wersja hello Capptain spowoduje konflikt i nastąpi błędy.

Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania hello. Należy pamiętać, że pliku xaml, jak i cs toobe aktualizacji.

Po wykonaniu tych kroków wystarczy tooreplace stare odwołania Capptain przez hello nowych zaangażowania odwołań.

1. Wszystkie przestrzenie nazw Capptain ma toobe aktualizacji.
   
    Przed migracją:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Po zakończeniu migracji:
   
        using Microsoft.Azure.Engagement;
2. Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".
   
    Przed migracją:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Po zakończeniu migracji:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.
   
    Przed migracją:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Po zakończeniu migracji:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Dla hello innych zasobów, takich jak obrazy Capptain należy pamiętać, że również zostały toouse zmieniono nazwę "Zaangażowania".

### <a name="application-id--sdk-key"></a>Identyfikator aplikacji / klucz zestawu SDK
Zaangażowania używa parametrów połączenia. Nie masz toospecify identyfikator i klucz zestawu SDK z usługi Mobile Engagement, wystarczy toospecify ciąg połączenia. Możesz można skonfigurować go na plik EngagementConfiguration.

Konfiguracja zaangażowania Hello może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.

Edytuj toospecify tego pliku:

* Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.

Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlany w hello klasycznego portalu Azure.

### <a name="items-name-change"></a>Zmiana nazwy elementów
Wszystkie elementy o nazwie *capptain* została nazwana *engagement*. Podobnie dla *Capptain* za*Engagement*.

Przykłady często używanych elementów Capptain:

* CapptainConfiguration teraz nazwę EngagementConfiguration
* Teraz o nazwie EngagementAgent CapptainAgent
* Teraz o nazwie EngagementReach CapptainReach
* Teraz o nazwie EngagementHttpConfig CapptainHttpConfig
* Teraz o nazwie GetEngagementPageName GetCapptainPageName

Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.

