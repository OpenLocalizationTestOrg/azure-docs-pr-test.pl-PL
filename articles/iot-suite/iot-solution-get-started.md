---
title: "Przykład MyDriving Azure IoT: Szybki start | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do aplikacji, która jest kompleksowe pokaz tooarchitect system IoT przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>System MyDriving IoT: Szybki start
MyDriving to system, który demonstruje hello projekt i implementację typowe [Internetu rzeczy](iot-suite-overview.md) rozwiązania (IoT), który zbiera dane telemetryczne z urządzeń, przetwarzania danych w chmurze hello i stosuje uczenia maszynowego tooprovide adaptacyjną odpowiedzi. Pokaz Hello rejestruje dane o Twojej rund samochodu przy użyciu danych z telefonu komórkowego i karty, która zbiera informacje z systemu kontroli samochód. Tej opinii tooprovide danych używa własnego stylu pobudzenie porównanie tooother użytkowników.

Witaj rzeczywistego celu MyDriving jest tooget uruchomienia podczas tworzenia rozwiązania IoT. Jednak przed, pomożemy Ci korzystanie z hello MyDriving aplikacja--członkiem naszego zespołu użytkownika testu. Zapewnia to środowisko aplikacji hello i systemie hello za nią klientów, przed delve w architekturze hello. On również przedstawiono tooHockeyApp, chłodnych sposób zarządzania hello alfa i beta dystrybucje użytkowników tootest aplikacji.

## <a name="use-hello-mobile-experience"></a>Użyj hello korzystanie z urządzeń przenośnych
Możesz użyć aplikacji MyDriving hello, jeśli masz urządzenia z systemem Android, iOS i Windows 10.

### <a name="android-and-windows-10-mobile-installation"></a>Android i Windows 10 Mobile instalacji
Na urządzeniu:

1. Zezwalaj na projektowanie aplikacji:
   
   * System android: W **ustawienia** > **zabezpieczeń**, Zezwalaj na aplikacje z **nieznane źródła**.
   * Systemie Windows 10: **ustawienia** > **aktualizacje** > **dla deweloperów**ustaw **tryb dewelopera**.
2. Dołącz nasz zespół beta testu przez zarejestrowanie u lub zalogowanie się do, [HockeyApp](https://rink.hockeyapp.net). Platforma HockeyApp umożliwia łatwe toodistribute Wczesne wersje użytkownikom tootest aplikacji.
   
   Jeśli używasz systemu Windows 10 za pomocą przeglądarki Edge hello.
   
   Gdyby uczestnika Build 2016, zaloguj się przy użyciu hello sam e-mail konta Microsoft, zarejestrowanego konferencji hello przy użyciu jednej z hello przycisków firmy Microsoft. Użytkownik już jest zalogowany z HockeyApp.
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
3. Pobierz i zainstaluj aplikacji hello w tym miejscu:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Istnieją dwa elementy. Zainstaluj certyfikat hello w **zaufane osoby**. Następnie zainstaluj aplikację hello.

*Uruchamianie aplikacji hello w systemie Windows 10 Mobile problemy?* Twój telefon może być aktualizacja lub dwóch za. Upewnij się, otrzymasz najnowsze aktualizacje hello, lub zainstalować:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Instalacja systemu iOS
Jeśli Twoja Build 2016, należy pobrać aplikację hello członkiem naszego zespołu testowego na platformę HockeyApp:

1. Na urządzeniu z systemem iOS, zaloguj się za[HockeyApp](https://rink.hockeyapp.net).
   Użycie hello jeden hello Microsoft logowania przycisków i zaloguj się przy użyciu tego samego e-mail konta Microsoft, który został zarejestrowany z konferencji hello. (Nie używaj hello pola wiadomości e-mail i hasło).
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
2. Na pulpicie nawigacyjnym aplikacji HockeyApp hello wybierz MyDriving i pobierz go.
3. Autoryzowanie hello wydanie beta z HockeyApp:
   
   a. Przejdź za**ustawienia** > **ogólne** > **profilów i zarządzania urządzeniami.**
   
   b. Zaufania hello **Bit Stadium GmbH** certyfikatu.

Jeśli nim nie zajmiesz Build 2016, możesz skompilować i wdrożyć aplikacji hello samodzielnie:

1. Pobierz kod hello [z usługi GitHub].
2. Tworzenie i wdrażanie przez [za pomocą platformy Xamarin].

Więcej szczegółów znajduje się w hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Pobierz adaptera diagnostycznego (opcjonalnie)
To jest część hello, który sprawia, że to rzeczywiste systemu Internetu rzeczy! Możesz użyć aplikacji hello bez ani jednego, ale jest więcej fun z czegoś hello, a nie są kosztowne.

Lokalnego Diagnostyka to funkcja hello samochód hello garaż tootune używa się samochód i diagnozowanie nieparzysta szumów i świateł ostrzeżenie. O ile samochód jest doskonałym antyków, znajdziesz gniazda gdzieś w podręcznego hello, zwykle za niestabilnością adresu w obszarze hello pulpitu nawigacyjnego. Łącznik prawo hello możesz pobrać metryki wydajności hello aparatu i niektórych dostosować. Łącznik diagnostycznego można zakupić tanio z takich miejsc, zwykle hello. Łączy przy użyciu aplikacji tooan Bluetooth lub Wi-Fi na telefonie.

W takim przypadku zamierzamy tooconnect samochodu toohello chmury. bezpośrednie połączenie hello diagnostycznego Hello jest tooyour telefon, ale aplikacji działa jako przekaźnik. Dane telemetryczne samochód jest wysyłany proste toohello Centrum MyDriving IoT, w którym jest przetwarzanie toolog Twojego rund drogowej i oceny własnego stylu jazdy.

tooconnect urządzenia diagnostycznego:

1. Sprawdź, czy samochód ma gniazda diagnostycznego.
2. Uzyskaj adaptera diagnostycznego:
   
   * Jeśli używasz programu Android i Windows phone, potrzebna jest karta II diagnostycznego z obsługą funkcji Bluetooth. My używamy [narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX].
   * Jeśli używasz telefonu z systemem iOS, należy adaptera diagnostycznego włączone Wi-Fi. My używamy [MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera].
3. Wykonaj instrukcje hello dostarczanych z Twojej tooconnect adaptera diagnostycznego go tooyour telefonu. Pamiętać hello następujące czynności:
   
   * Karta Bluetooth muszą łączyć się z telefonu hello, na powitania **ustawienia** strony.
   * Karty sieci Wi-Fi musi mieć adres w hello 192.168.xxx.xxx zakresu.
4. Jeśli masz kilka samochodów, możesz uzyskać osobnej karty dla każdego (maksymalnie trzy).

Jeśli nie masz adaptera diagnostycznego aplikacji hello nadal będzie wysyłać, lokalizacji i szybkości danych z telefonu hello GPS odbiornika toohello ponownie zakończyć i zapyta, czy ma toosimulate diagnostycznego.

Znajduje się więcej o używaniu danych z karty diagnostycznego hello aplikacji hello i opcje tworzenia urządzenia diagnostycznego w sekcji 2.1 "Urządzenia IoT," w hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Użycie aplikacji hello
Uruchamiają aplikację hello. Brak początkowej toowalk szybkiego startu sposób jej działania.

### <a name="track-your-trips"></a>Śledzenie sieci rund
Wybierz hello przycisk rekordów (big czerwone kółko u dołu ekranu hello hello) toostart podróży, a następnie ponownie wybierz tooend.

![Ilustracja przycisku rekordu hello podczas podróży śledzenia](./media/iot-solution-get-started/image2.png)

Każdym uruchomieniu podróży, jeśli istnieje nie jest diagnostycznego urządzeniem, użytkownik zostanie zapytany czy ma toouse hello symulatora.

Naciśnij hello Zatrzymaj przycisku, a na końcu hello podróży, uzyskać podsumowanie.

![Przykład podróży podsumowania](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Zapoznaj się z podróży
![Przykład ostatnich podróży](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Przejrzyj profilu
![Przykład profilu zwiększają stylu](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Wyślij nam swoją opinię testu
Ponieważ utworzyliśmy Rozpocznij pracę toohelp MyDriving systemów IoT chcemy pewnością toohear od użytkownika o tym, jak działa. Daj nam znać, jeśli:

* Wystąpiły problemy lub wyzwania.
* Brak punktu rozszerzenia, że będą bardziej odpowiedni scenariusz tooyour.
* Efektywniejsze tooaccomplish sposób znaleźć określonych potrzeb.
* Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.

W ramach hello MyDriving samej aplikacji, można użyć hello wbudowany mechanizm opinii HockeyApp: w systemach iOS i Android, wystarczy podać telefon potrząsania powoduje lub użyj hello **opinii** polecenia menu. Zrzut ekranu, to dołączą automatycznie tak, aby firma Microsoft wie, co jest mowa o. Oraz w przypadku awarii (Crash) wszelkie niefortunne HockeyApp zbiera tootell dzienniki awarii hello nas o nich. Możesz też udzielić informacje zwrotne przez hello [portalu HockeyApp].

Można również pliku [problem w usłudze GitHub], lub zostaw komentarz poniżej (en-us edition).

Mamy nadzieję toohearing od Ciebie!

## <a name="next-steps"></a>Następne kroki
* Eksploruj hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs) toounderstand jak wprowadzeniu zaprojektowany i zbudowany hello całego systemu MyDriving.
* [Tworzenie i wdrażanie własnego systemu](iot-solution-build-system.md) za pomocą skryptów naszej usługi Azure Resource Manager. Witaj [MyDriving podręcznik](http://aka.ms/mydrivingdocs) prowadzi użytkownika przez obszary, w których należy podjąć hello większości dostosowań.

[z usługi GitHub]: https://github.com/Azure-Samples/MyDriving
[za pomocą platformy Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX]: http://www.amazon.com/gp/product/B005NLQAHS
[MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[portalu HockeyApp]: https://rink.hockeyapp.org
[problem w usłudze GitHub]: https://github.com/Azure-Samples/MyDriving/issues
