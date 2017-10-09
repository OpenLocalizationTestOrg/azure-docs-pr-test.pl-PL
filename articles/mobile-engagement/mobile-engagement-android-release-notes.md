---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Informacje o wersji

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Usuń awarii rzadko może się zdarzyć podczas wywoływania metody `EngagementAgentUtils.isInDedicatedEngagementProcess`, która jest już używana przez hello `EngagementApplication` klasy.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Obsługa 8 systemu android (poprzednie wersje powitalne zestawu SDK nie będą działać na 8 dla systemu Android).
* Nie więcej zależności biblioteki pomocy technicznej.
* Usuń `EngagementFragmentActivity` klasy.
* Z powodu zbyt[limity wykonywania tła](https://developer.android.com/preview/features/background.html) na 8 dla systemu Android, dzienniki w tle mogą zostać opóźnione aż hello użytkownik wchodzi w interakcję z urządzeniem hello, będzie to mieć wpływ na Push kampanii **dostarczone** i **Powiadomienie systemowe wyświetlane** statystyki opóźnieniu, jeśli został uśpiony hello urządzenia (hello powiadomienia będą nadal wyświetlane, będzie pierścienia i Włącz wibrację w czasie rzeczywistym bez problemów).
* Z powodu zbyt[ograniczenia lokalizacji tła](https://developer.android.com/preview/features/background-location-limits.html), hello czasu rzeczywistego lokalizacji w tle nie zostanie zaktualizowany często na 8 dla systemu Android.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* Napraw powiadomień w aplikacji koloru tekstu na toobe Android 7 hello takie same jak starsze wersje systemu Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Więcej blokady sieci Wi-Fi.
* Usuń zakleszczenie podczas wywoływania metody getDeviceId przed init (wprowadzona w 4.2.0 błędów).

## <a name="422-05172016"></a>4.2.2 (05/17/2016)
* Ulepszenia.

## <a name="421-05102016"></a>4.2.1 (05/10/2016)
* Zabezpieczenia: Wyłącz dostęp do pliku lokalnego widoku sieci web.
* Security: usunąć `EngagementPreferenceActivity` klasy, która rozszerza przestarzałe i niezabezpieczone `PreferenceActivity` klasy.
* Zabezpieczenia: reach działania są teraz udokumentowane toouse `exported="false"`, ta flaga umożliwia również w poprzednich wersjach zestawu SDK.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Witaj zestawu SDK jest teraz licencją MIT.
* Pozwala na stosowanie identyfikator urządzeń niestandardowych w czasie inicjowania zestawu SDK.

## <a name="415-02012016"></a>4.1.5 (02/01/2016)
* Ulepszenia.

## <a name="414-01262016"></a>4.1.4 (01/26/2016)
* Ulepszenia.

## <a name="413-1292015"></a>4.1.3 (12/9/2015)
* Ulepszenia.

## <a name="412-11252015"></a>4.1.2 (11/25/2015)
* Ulepszenia.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* Ulepszenia.

## <a name="410-08252015"></a>4.1.0 (08/25/2015)
* Obsługa nowego modelu uprawnień dla systemu Android M.
* Można teraz skonfigurować funkcje lokalizacji w czasie wykonywania, zamiast `AndroidManifest.xml`.
* Naprawa błędów uprawnienie: Jeśli używasz `ACCESS_FINE_LOCATION`, następnie `ACCESS_COARSE_LOCATION` nie jest już potrzebne.
* Ulepszenia.

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* Wewnętrzny protokołu zmienia toomake analytics i bardziej niezawodny wypychania.
* Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych powitania dla dowolnego typu wypychania kampanii.
* Usuń powiadomień szerszej: były wyświetlane tylko 10s po przekazywanej.
* Naprawa błędów w widoku sieci web: kliknięcie łącza również wykonywania hello będzie domyślny adres URL akcji.
* Usuń rzadkich awarii powiązane toolocal zarządzania magazynem.
* Napraw zarządzania ciągu konfiguracji dynamicznej.
* Zaktualizuj umowy licencyjnej.

## <a name="300-02172015"></a>3.0.0 (02/17/2015)
* Początkowa wersja usługi Azure Mobile Engagement
* Konfiguracja appId zastępuje konfigurację ciągu połączenia.
* Usunięte toosend interfejsu API i odbieranie komunikatów XMPP dowolnego z dowolnego XMPP jednostek.
* Usunięte toosend interfejsu API i odbierania wiadomości między urządzeniami.
* Ulepszenia zabezpieczeń.
* Śledzenie Google Play i SmartAd usunięte.

