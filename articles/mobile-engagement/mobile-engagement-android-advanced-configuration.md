---
title: Konfiguracja aaaAdvanced zestawem Azure Mobile Engagement Android SDK
description: W tym artykule opisano hello zaawansowane opcje konfiguracji, w tym hello manifestu systemu Android z zestawem Azure Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Konfiguracja zaawansowana dla zestawem Azure Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

W tej procedurze opisano sposób tooconfigure różnych opcji konfiguracji dla usługi Azure Mobile Engagement aplikacji systemu Android.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Wymagania dotyczące uprawnień
Niektóre opcje muszą mieć określone uprawnienia, które są wymienione wszystkie tutaj odwołania i wiersza w określonej funkcji hello. Dodaj te uprawnienia toohello AndroidManifest.xml projektu bezpośrednio przed lub po hello `<application>` tagu.

kod uprawnień Hello musi toolook, takich jak hello poniższe polecenie, gdzie Wypełnij hello odpowiednich uprawnień z poniższą tabelą hello.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Uprawnienie | Gdy jest używany |
| --- | --- |
| INTERNET |Wymagany. Na podstawowym raportowaniem |
| ACCESS_NETWORK_STATE |Wymagany. Na podstawowym raportowaniem |
| RECEIVE_BOOT_COMPLETED |Wymagany. tooshow się Centrum powiadomień powitania po ponownym uruchomieniu urządzenia |
| WAKE_LOCK |Zalecane. Umożliwia zbieranie danych przy użyciu sieci Wi-Fi lub gdy ekran jest wyłączony |
| WŁĄCZ WIBRACJĘ |Opcjonalny. Włącza wibrację po otrzymaniu powiadomienia |
| DOWNLOAD_WITHOUT_NOTIFICATION |Opcjonalny. Włącza powiadomień systemu Android duży obraz. |
| WRITE_EXTERNAL_STORAGE |Opcjonalny. Włącza powiadomień systemu Android duży obraz. |
| ACCESS_COARSE_LOCATION |Opcjonalny. Włącza raportowanie lokalizacji w czasie rzeczywistym |
| ACCESS_FINE_LOCATION |Opcjonalny. Włącza raportowanie oparte na GPS lokalizacji |

Począwszy od systemu Android M [niektóre uprawnienia są zarządzane w czasie wykonywania](mobile-engagement-android-location-reporting.md#android-m-permissions).

Jeśli korzystasz już z ``ACCESS_FINE_LOCATION``, nie potrzebujesz tooalso, a następnie użyć ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Opcje konfiguracji manifestu systemu android
### <a name="crash-report"></a>Raport o awarii
Raporty awarii toodisable, Dodaj ten kod między hello `<application>` i `</application>` tagów:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Próg serii
Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym. Jeśli dzienniki raportu Twojej aplikacji różnią się często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (nazywanych "Tryb szybki"). toodo tak, Dodaj ten kod między hello `<application>` i `</application>` tagów:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Tryb serii nieco zwiększa hello czas pracy baterii, ale ma wpływ na powitania monitora usługi Engagement: wszystkie czas trwania sesji i zadań są zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna). Próg z serii powinna być dłuższa niż 30000 (30s).

### <a name="session-timeout"></a>Limit czasu sesji
 Działanie może być zakończona przez naciśnięcie przycisku hello **Home** lub **ponownie** klucza przez ustawienie hello phone bezczynności lub przejście do innej aplikacji. Domyślnie jest zakończenie sesji dziesięć sekund po zakończeniu hello jego ostatniej aktywności. Pozwala to uniknąć podziału sesji każdego użytkownika w czasie hello opuszcza i zwraca aplikacji toohello szybkie, które mogą wystąpić podczas użytkownika hello przejmuje obrazu sprawdza powiadomienia itp. Ten parametr może być toomodify. toodo tak, Dodaj ten kod między hello `<application>` i `</application>` tagów:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Wyłączanie dziennika raportowania
### <a name="using-a-method-call"></a>Przy użyciu wywołania metody
Jeśli chcesz toostop zaangażowania wysyłania dzienników, można wywołać:

    EngagementAgent.getInstance(context).setEnabled(false);

To wywołanie jest trwały: używa plików udostępnionych preferencji.

Jeśli zaangażowania jest aktywny, gdy wywołanie tej funkcji, może zająć jedną minutę na powitania toostop usługi. Jednak nie będzie uruchomić usługi hello na wszystkich hello następnym uruchomieniu aplikacji hello.

Możesz włączyć ponownie raportowania przez wywołanie metody hello sam działać z dziennika `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integracja z własną`PreferenceActivity`
Zamiast wywoływania tej funkcji, to ustawienie można również zintegrować bezpośrednio w istniejącą `PreferenceActivity`.

Toouse zaangażowania preferencje plików (w trybie żądaną hello) można skonfigurować w hello `AndroidManifest.xml` pliku z `application meta-data`:

* Witaj `engagement:agent:settings:name` klucz to nazwa hello toodefine używanych plików udostępnionych preferencji hello.
* Witaj `engagement:agent:settings:mode` klucza jest tryb hello toodefine używanych plików udostępnionych preferencji hello. Użyj hello sam tryb jako w Twojej `PreferenceActivity`. Tryb Hello muszą być przekazywane w postaci liczby: Jeśli korzystasz z kombinacją flag stałej w kodzie, sprawdź wartość całkowita hello.

Zaangażowania zawsze używa hello `engagement:key` logiczna klucz w pliku preferencji hello zarządzania to ustawienie.

Witaj następujący przykład `AndroidManifest.xml` pokazuje hello wartości domyślne:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

Następnie można dodać `CheckBoxPreference` w układzie preferencji, takich jak hello jednym następującego:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
