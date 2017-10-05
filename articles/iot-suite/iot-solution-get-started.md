---
title: "Przykład MyDriving Azure IoT: Szybki start | Dokumentacja firmy Microsoft"
description: "Zacznij korzystać z aplikacji, która jest kompleksowe pokaz zaprojektować IoT system przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
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
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a>System MyDriving IoT: Szybki start
MyDriving to system, który demonstruje projekt i implementację typowe [Internetu rzeczy](iot-suite-overview.md) rozwiązania (IoT), który zbiera dane telemetryczne z urządzeń, przetwarzania danych w chmurze i stosuje machine learning w celu zapewnienia adaptacyjnego odpowiedzi. Pokazu rejestruje dane o Twojej rund samochodu na podstawie danych z telefonu komórkowego i karty, która zbiera informacje z systemu kontroli samochód. Używa tych danych do przekazywania opinii własnego stylu jazdy w odróżnieniu od innych użytkowników.

Rzeczywistego celu MyDriving jest ułatwiających rozpoczęcie pracy podczas tworzenia rozwiązania IoT. Jednak przed, pomożemy Ci korzystanie z MyDriving aplikacja--członkiem naszego zespołu użytkownika testu. Zapewnia to środowisko aplikacji i systemu za nią klientów, przed delve do architektury. On również przedstawiono HockeyApp, chłodnych sposób zarządzania alfa i beta dystrybucji aplikacji użytkowników testowych.

## <a name="use-the-mobile-experience"></a>Użyj korzystanie z urządzeń przenośnych
Jeśli masz urządzenia z systemem Android, iOS i Windows 10, mogą korzystać z aplikacji MyDriving.

### <a name="android-and-windows-10-mobile-installation"></a>Android i Windows 10 Mobile instalacji
Na urządzeniu:

1. Zezwalaj na projektowanie aplikacji:
   
   * System android: W **ustawienia** > **zabezpieczeń**, Zezwalaj na aplikacje z **nieznane źródła**.
   * Systemie Windows 10: **ustawienia** > **aktualizacje** > **dla deweloperów**ustaw **tryb dewelopera**.
2. Dołącz nasz zespół beta testu przez zarejestrowanie u lub zalogowanie się do, [HockeyApp](https://rink.hockeyapp.net). Platforma HockeyApp ułatwia dystrybucję Wczesne wersje aplikacji użytkowników testowych.
   
   Jeśli używasz systemu Windows 10, użyj przeglądarki Edge.
   
   Gdyby uczestnika Build 2016, zaloguj się przy użyciu tego samego e-mail konta Microsoft zarejestrowana konferencji za pomocą jednego z przycisków firmy Microsoft. Użytkownik już jest zalogowany z HockeyApp.
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
3. Pobierz i zainstaluj aplikację w tym miejscu:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Istnieją dwa elementy. Zainstaluj certyfikat w **zaufane osoby**. Następnie zainstaluj aplikację.

*Uruchamianie aplikacji w systemie Windows 10 Mobile problemy?* Twój telefon może być aktualizacja lub dwóch za. Upewnij się, że masz najnowsze aktualizacje, lub zainstalować:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Instalacja systemu iOS
Jeśli Twoja Build 2016, Pobierz aplikację członkiem naszego zespołu testowego na platformę HockeyApp:

1. Na urządzeniu z systemem iOS, zaloguj się do [HockeyApp](https://rink.hockeyapp.net).
   Użyj jednej z Microsoft logowania przycisków i zaloguj się przy użyciu tego samego e-mail konta Microsoft, który został zarejestrowany z konferencji. (Nie używaj pola wiadomości e-mail i hasło).
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
2. Na pulpicie nawigacyjnym aplikacji HockeyApp MyDriving wybierz i pobierz go.
3. Autoryzowanie wydanie beta z HockeyApp:
   
   a. Przejdź do **ustawienia** > **ogólne** > **profilów i zarządzania urządzeniami.**
   
   b. Zaufania **Bit Stadium GmbH** certyfikatu.

Jeśli nim nie zajmiesz Build 2016, możesz skompilować i wdrożyć aplikację samodzielnie:

1. Pobierz kod [z usługi GitHub].
2. Tworzenie i wdrażanie przez [za pomocą platformy Xamarin].

Znajdź więcej szczegółów w [MyDriving podręcznik](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Pobierz adaptera diagnostycznego (opcjonalnie)
Jest to element, który sprawia, że to rzeczywiste systemu Internetu rzeczy! Możesz użyć aplikacji bez ani jednego, ale jest więcej fun z czegoś, a nie są kosztowne.

Lokalnego Diagnostyka jest funkcją samochód używającej garaż dostrajanie samochód i diagnozowanie nieparzysta szumów i świateł ostrzeżenie. O ile samochód jest doskonałym antyków, znajdziesz gniazda gdzieś w podręcznego, zwykle za niestabilnością adresu w ramach pulpitu nawigacyjnego. Prawy łącznik możesz pobrać metryki wydajności przez aparat i niektórych dostosować. Łącznik diagnostycznego można zakupić tanio z zwykle miejsca. Łączy za pomocą urządzenia Bluetooth lub Wi-Fi do aplikacji w telefonie.

W takim przypadku zamierzamy samochód nawiązać połączenia z chmurą. Bezpośrednie połączenie z diagnostycznego jest na Twój telefon, ale aplikacji działa jako przekaźnik. Telemetrii samochód są wysyłane bezpośrednio do Centrum MyDriving IoT, gdzie są przetwarzane do logowania użytkownika rund drogowej i oceny własnego stylu jazdy.

Aby podłączyć urządzenia diagnostycznego:

1. Sprawdź, czy samochód ma gniazda diagnostycznego.
2. Uzyskaj adaptera diagnostycznego:
   
   * Jeśli używasz programu Android i Windows phone, potrzebna jest karta II diagnostycznego z obsługą funkcji Bluetooth. My używamy [narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX].
   * Jeśli używasz telefonu z systemem iOS, należy adaptera diagnostycznego włączone Wi-Fi. My używamy [MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera].
3. Postępuj zgodnie z instrukcjami dostarczonymi z kartą diagnostycznego w celu połączenia jej na Twój telefon. Należy pamiętać, że:
   
   * Karta Bluetooth muszą łączyć się z telefonu, na **ustawienia** strony.
   * Karty sieci Wi-Fi musi mieć adres w 192.168.xxx.xxx zakresu.
4. Jeśli masz kilka samochodów, możesz uzyskać osobnej karty dla każdego (maksymalnie trzy).

Jeśli nie masz adaptera diagnostycznego aplikacja nadal będzie wysyłać dane lokalizacji i szybkość z odbiornika GPS telefonu do wewnętrznej i zapyta, czy chcesz symulować diagnostycznego.

Można dowiedzieć się więcej o jak aplikacja korzysta z danych z karty diagnostycznego i opcje tworzenia urządzenia diagnostycznego w sekcji 2.1 "Urządzenia IoT,", w [MyDriving podręcznik](http://aka.ms/mydrivingdocs).

## <a name="use-the-app"></a>Za pomocą aplikacji
Uruchom aplikację. Brak początkowej szybkiego startu, aby zademonstrować sposób jej działania.

### <a name="track-your-trips"></a>Śledzenie sieci rund
Naciśnij przycisk rekordu (big czerwone kółko w dolnej części ekranu) można uruchomić podróży i ponownie naciśnij, aby zakończyć.

![Ilustracja przycisku rekordu podczas podróży śledzenia](./media/iot-solution-get-started/image2.png)

Podczas każdego uruchomienia podróży, jeśli istnieje nie jest diagnostycznego urządzeniem, użytkownik zostanie zapytany Jeśli chcesz użyć symulatora.

Na koniec podróży naciśnij przycisk Zatrzymaj, a uzyskać podsumowanie.

![Przykład podróży podsumowania](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Zapoznaj się z podróży
![Przykład ostatnich podróży](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Przejrzyj profilu
![Przykład profilu zwiększają stylu](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Wyślij nam swoją opinię testu
Ponieważ systemy IoT utworzyliśmy MyDriving ułatwiające Rozpocznij pracę chcemy pewnością poznać Twoją opinię o tym, jak działa. Daj nam znać, jeśli:

* Wystąpiły problemy lub wyzwania.
* Brak punktu rozszerzenia, że będą bardziej odpowiednie do realizowanego scenariusza.
* Możesz znaleźć bardziej wydajny sposób wykonywania określonych potrzeb.
* Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.

W ramach MyDriving aplikacji, można użyć wbudowany mechanizm opinii HockeyApp: w systemach iOS i Android, wystarczy podać telefon potrząsania powoduje lub użyj **opinii** polecenia menu. Zrzut ekranu, to dołączą automatycznie tak, aby firma Microsoft wie, co jest mowa o. A w przypadku awarii (Crash) wszelkie niefortunne HockeyApp zbiera dzienniki awarii, aby poinstruować nas o nich. Możesz też udzielić informacje zwrotne przez [portalu HockeyApp].

Można również pliku [problem w usłudze GitHub], lub zostaw komentarz poniżej (en-us edition).

Czekamy na przesłuchanie od Ciebie!

## <a name="next-steps"></a>Następne kroki
* Eksploruj [MyDriving podręcznik](http://aka.ms/mydrivingdocs) zrozumieć, jak wprowadzeniu zaprojektowany i zbudowany całego systemu MyDriving.
* [Tworzenie i wdrażanie własnego systemu](iot-solution-build-system.md) za pomocą skryptów naszej usługi Azure Resource Manager. [MyDriving podręcznik](http://aka.ms/mydrivingdocs) prowadzi użytkownika przez obszary, w których należy podjąć najbardziej dostosowania.

[z usługi GitHub]: https://github.com/Azure-Samples/MyDriving
[za pomocą platformy Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX]: http://www.amazon.com/gp/product/B005NLQAHS
[MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[portalu HockeyApp]: https://rink.hockeyapp.org
[problem w usłudze GitHub]: https://github.com/Azure-Samples/MyDriving/issues
