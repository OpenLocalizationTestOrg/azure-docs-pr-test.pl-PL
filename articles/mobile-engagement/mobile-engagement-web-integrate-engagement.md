---
title: "zestaw SDK usługi Mobile Engagement w sieci Web integracji aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj najnowsze aktualizacje i procedury dotyczące hello zestaw SDK usługi Azure Mobile Engagement w sieci Web"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Integrowanie usługi Azure Mobile Engagement w aplikacji sieci web
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Witaj procedur w tym artykule opisano hello najprostszy sposób tooactivate hello analizy i monitorowania funkcji w usłudze Azure Mobile Engagement w aplikacji sieci web.

Wykonaj wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i technicals hello kroki tooactivate hello dziennika raportów, które są potrzebne toocompute. Statystyki zależne od aplikacji, takich jak zdarzenia, błędy i zadań należy ręcznie uaktywnić raporty dziennika przy użyciu interfejsu API usługi Azure Mobile Engagement hello. Aby uzyskać więcej informacji, Dowiedz się [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Wprowadzenie
[Pobierz zestaw SDK usługi Azure Mobile Engagement Web hello](http://aka.ms/P7b453).
Hello przenośnych zaangażowania zestawu SDK sieci Web jest dostarczana jako pojedynczy plik JavaScript, azure-engagement.js, których tooinclude na każdej stronie Twojej witryny lub aplikacji sieci web.

> [!IMPORTANT]
> Przed uruchomieniem tego skryptu, należy uruchomić skrypt lub zapisu tooconfigure Mobile Engagement dla aplikacji fragment kodu.
> 
> 

## <a name="browser-compatibility"></a>Zgodność przeglądarek
Hello zestaw SDK usługi Mobile Engagement w sieci Web używa natywnego JSON, kodowania i dekodowania dodatkowo żądania AJAX toocross domeny (polegania na powitania specyfikacji W3C CORS). Jest on zgodny z hello następujące przeglądarki:

* Przeglądarka Microsoft Edge 12 +
* Program Internet Explorer 10 +
* Firefox 3.5 +
* Chrome 4 +
* Safari 6 +
* Opera 12 +

## <a name="configure-mobile-engagement"></a>Konfigurowanie usługi Mobile Engagement
Napisać skrypt, który tworzy globalnym `azureEngagement` obiektu JavaScript, tak jak hello poniższy przykład. Ponieważ witryna może być wielokrotność stron, w tym przykładzie założono, że ten skrypt znajduje się na każdej stronie. W tym przykładzie nosi nazwę obiektu JavaScript hello `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Witaj `connectionString` wartość aplikacji zostanie wyświetlony w hello portalu Azure.

> [!NOTE]
> `appVersionName`i `appVersionCode` są opcjonalne. Jednak zaleca się je skonfigurować tak, aby analiza może przetworzyć informacji o wersji.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Uwzględnić skrypty Mobile Engagement na swoich stronach
Dodaj usługi Mobile Engagement skrypty tooyour stron w jednym z hello następujące sposoby:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Lub to:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Po załadowaniu hello skryptu zestaw SDK usługi Mobile Engagement w sieci Web tworzy hello **engagement** alias tooaccess hello interfejsów API zestawu SDK. Nie można użyć tego aliasu toodefine hello SDK konfiguracji. Ten alias jest używany jako odwołanie w niniejszej dokumentacji.

Należy pamiętać, że jeśli hello domyślny alias powoduje konflikt z innym zmiennej globalnej ze strony użytkownika, można zmienić go w konfiguracji hello następujący przed załadowaniem hello zestaw SDK usługi Mobile Engagement w sieci Web:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Podstawowym raportowaniem
Podstawowym raportowaniem w usłudze Mobile Engagement obejmuje statystyki poziomu sesji, takie jak statystyki dotyczące użytkowników, sesji, działaniami i awariami.

### <a name="session-tracking"></a>Śledzenie sesji
Sesja usługi Mobile Engagement jest podzielony na sekwencję działań, każdy identyfikowane przez nazwę.

W klasycznej witryny zaleca się zadeklarować różnych działań na każdej stronie witryny. Dla witryny sieci Web lub aplikacji sieci web w których hello nigdy nie zmienia bieżącej strony możesz tootrack hello działań na mniejszą skalę, takich jak stronie powitania.

Albo, toostart lub zmień hello bieżącego działania użytkownika, wywołania hello `engagement.agent.startActivity` funkcji. Na przykład:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Serwer usługi Mobile Engagement Hello kończy się automatycznie otwartych sesji w ciągu trzech minut po zamknięciu strony aplikacji hello.

Alternatywnie można zakończyć sesję ręcznie przez wywołanie metody `engagement.agent.endActivity`. To ustawienie hello bieżącego użytkownika działania too'Idle. "  Sesja Hello zakończy później 10 sekund, chyba że nowy wywołanie za`engagement.agent.startActivity` wznawia hello sesji.

Witaj 10-sekundowe opóźnienie można skonfigurować w obiekcie globalnej hello, w następujący sposób:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Nie można użyć `engagement.agent.endActivity` w hello `onunload` wywołania zwrotnego, ponieważ na tym etapie nie można wprowadzić wywołania AJAX.
> 
> 

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie Jeśli chcesz tooreport zdarzenia specyficzne dla aplikacji, błędy i zadań, należy hello toouse Mobile Engagement z interfejsu API. Dostęp hello Mobile Engagement API za pośrednictwem hello `engagement.agent` obiektu.

Możesz uzyskać dostęp do wszystkich hello zaawansowane funkcje w usłudze Mobile Engagement w hello Mobile Engagement z interfejsu API. Witaj interfejsu API została szczegółowo opisana w artykule hello [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Dostosowywanie hello adresy URL używany dla wywołań AJAX
Adresy URL można dostosować ten hello używanych przez zestaw SDK usługi Mobile Engagement w sieci Web. Na przykład może zastąpić konfiguracji hello tooredefine hello URL dziennika (hello SDK punktu końcowego logowania), podobnie do następującej:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Jeśli adres URL funkcji zwraca ciąg, który rozpoczyna się od `/`, `//`, `http://`, lub `https://`, hello domyślny schemat nie jest używany. Domyślnie program hello `https://` schemat jest używany dla tych adresów URL. Jeśli chcesz toocustomize hello domyślny schemat, Zastąp hello konfiguracji, takich jak to:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
