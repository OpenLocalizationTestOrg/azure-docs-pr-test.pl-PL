---
title: "Zarządzanie aaaDevice z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Omówienie zarządzania urządzeniami w usłudze Azure IoT Hub: cykl życia urządzenia w przedsiębiorstwie i wzorce zarządzania urządzeniami, takie jak ponowne uruchamianie, resetowanie do ustawień fabrycznych, aktualizacja oprogramowania układowego, konfiguracja, bliźniacze reprezentacje urządzeń, zapytania, zadania."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Omówienie zarządzania urządzeniami za pomocą usługi IoT Hub
## <a name="introduction"></a>Wprowadzenie
Centrum IoT Azure udostępnia funkcje hello i modelu rozszerzeń, które włączają urządzenia i rozwiązania do zarządzania urządzeniami niezawodne toobuild deweloperzy wewnętrznej. Urządzenia z zakresu od ograniczonego czujników i mikrokontrolerów jednozadaniowe, toopowerful bram, które trasy komunikacji dla grup urządzeń.  Ponadto hello przypadków użycia i wymagania dotyczące operatorów IoT różnią się znacznie w branży.  Niezależnie od zmian zarządzanie urządzeniami za pomocą Centrum IoT zapewnia możliwości hello, wzorców i kod biblioteki toocater tooa różnorodnych urządzeń i użytkowników końcowych.

Kluczową kwestią tworzenia rozwiązania IoT pomyślne przedsiębiorstwa jest tooprovide strategię jak operatorów obsługuje hello bieżące zarządzanie ich kolekcji urządzeń. Operatory IoT wymagają proste i niezawodne narzędzia i aplikacje, które umożliwia im toofocus na powitania więcej strategicznych aspektów swoich zadań. Ten artykuł zawiera:

* Krótkie omówienie zarządzania toodevice podejście Azure IoT Hub.
* Opis typowych zasad dotyczących zarządzania urządzeniami.
* Opis hello cykl życia urządzenia.
* Przegląd typowych wzorców zarządzania urządzeniami.

## <a name="device-management-principles"></a>Zasady zarządzania urządzeniami
IoT łączy się z nim unikatowy zestaw wyzwania zarządzania urządzeniami i każde rozwiązanie z klasy korporacyjnej muszą spełnić hello następujące zasady:

![Ilustracja dotycząca zasad zarządzania urządzeniami][img-dm_principles]

* **Skalowanie i automatyzacji**: rozwiązania IoT wymagają proste narzędzia, które Automatyzacja rutynowych zadań i włączenia stosunkowo mały operacji personelu toomanage milionów urządzeń. Codziennych, Operatorzy mogą pojawić się operacje urządzenia toohandle zdalnie, w zbiorczego, i tooonly otrzymywać alerty o problemach wymagających ich uwagi bezpośredniego.
* **Przejrzystości i zgodności**: hello ekosystemu urządzenia jest bardzo różnorodnych. Narzędzia do zarządzania muszą być dopasowane tooaccommodate wieloma klas urządzeń, platform i protokołów. Operatory musi być w stanie toosupport wiele typów urządzeń z hello najbardziej ograniczonego osadzonych mikroukłady jednego procesu, toopowerful i komputerów w pełni funkcjonalne.
* **Uwzględnianie kontekstu**: środowiska IoT są dynamiczne i nieustannie się zmieniają. Najważniejszą kwestią jest niezawodność usługi. Operacje zarządzania urządzeniami musi uwzględniać następujące czynniki tooensure hello konta tej obsługi przestoje nie mają wpływ na operacje biznesowe krytyczne lub tworzenie niebezpiecznych warunków:
    * Okna obsługi w umowie SLA
    * Stany sieci i zasilania
    * Warunki użycia
    * Geolokalizacja urządzenia
* **Usługi ról wiele**: Obsługa hello unikatowy przepływów pracy i procesy ról operacji IoT odgrywa kluczową rolę. Operatorzy Hello harmonijnego współpracy z hello, ponieważ istnieją ograniczenia wewnętrznego działów IT.  Należy również znajduje się zrównoważony sposób toosurface czasu rzeczywistego urządzenia operacji informacji toosupervisors i innych firm ról zarządzania.

## <a name="device-lifecycle"></a>Cykl życia urządzenia
Istnieje zestaw etapy zarządzania ogólne urządzenia, które są typowe projektami IoT enterprise tooall. Azure IoT istnieją pięć etapów hello cykl życia urządzenia:

![Witaj pięć etapy cyklu życia urządzenia Azure IoT: Planowanie, obsługi administracyjnej, konfigurowanie, monitorowanie i wycofać][img-device_lifecycle]

W ramach każdej z tych pięć etapów spełnić kilka wymagań operator urządzenia, które powinny być spełnione tooprovide kompletnego rozwiązania:

* **Planowanie**: Włącz operatory toocreate schemat metadanych urządzenia, który umożliwia im tooeasily i dokładnie zapytanie dla i grupę urządzeń dla operacji zarządzania zbiorczego. Można użyć hello urządzenia dwie toostore te metadane urządzenia w formie hello tagów i właściwości.
  
    *Dalsze informacje*: [Rozpoczynanie pracy z urządzenia twins][lnk-twins-getstarted], [zrozumieć urządzenia twins][lnk-twins-devguide], [jak właściwości dwie urządzenia toouse][lnk-twin-properties].
* **Zainicjuj obsługę**: bezpiecznie udostępnić nowych urządzeń tooIoT koncentratora i Włącz operatory tooimmediately odnajdywanie możliwości urządzenia.  Użyj hello Centrum IoT tożsamość rejestru toocreate elastyczne urządzenia tożsamości i poświadczenia i wykonać tę operację w trybie zbiorczym przy użyciu zadania. Kompilacja tooreport urządzeń, ich możliwości i warunki za pośrednictwem właściwości urządzenia w Witaj dwie urządzenia.
  
    *Dalsze informacje*: [Zarządzanie tożsamościami urządzenia][lnk-identity-registry], [zbiorcze Zarządzanie tożsamościami urządzenia][lnk-bulk-identity], [Jak urządzenie toouse dwie właściwości][lnk-twin-properties].
* **Skonfiguruj**: ułatwienia zbiorczego zmian konfiguracji i oprogramowanie układowe aktualizuje toodevices, zachowując dane o kondycji i zabezpieczeń. Wykonaj te operacje zarządzania urządzeniami zbiorczo, używając odpowiednich właściwości lub bezpośrednich metod i zadań emisji.
  
    *Dalsze informacje*: [metody bezpośredniego][lnk-c2d-methods], [wywołana metoda bezpośrednio na urządzeniu][lnk-methods-devguide], [jak właściwości dwie urządzenia toouse][lnk-twin-properties], [emisji zadania i harmonogramu][lnk-jobs], [Planowanie zadań na wielu urządzeniach] [lnk-jobs-devguide].
* **Monitor**: monitorowanie kondycji kolekcji ogólnej urządzenia, stan hello trwających operacji i tooissues operatory alertów, które mogą wymagać ich uwagi.  Zastosuj hello urządzenia dwie tooallow urządzeń tooreport czasu rzeczywistego warunki działania i stan operacji aktualizacji. Zaawansowane pulpit nawigacyjny kompilacji raporty tego powierzchni hello większości problemów z bezpośrednim przy użyciu urządzenia dwie zapytań.
  
    *Dalsze informacje*: [jak urządzenie toouse dwie właściwości][lnk-twin-properties], [Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ lnk-query-language].
* **Wycofywanie**: Zamień lub zlikwidować urządzenia po awarii, Uaktualnij cykl, lub na końcu hello okres istnienia hello usługi.  Użyj informacje o urządzeniu toomaintain hello urządzenia dwie, jeśli urządzenie fizyczne hello jest zastąpienia lub archiwizowane, jeśli wycofana. Użyj hello rejestru tożsamości Centrum IoT bezpiecznie cofnięcia tożsamości urządzenia i poświadczeń.
  
    *Dalsze informacje*: [jak urządzenie toouse dwie właściwości][lnk-twin-properties], [Zarządzanie tożsamościami urządzenia][lnk-identity-registry].

## <a name="device-management-patterns"></a>Wzorce zarządzania urządzeniami
Centrum IoT umożliwia powitania po zestaw wzorców zarządzania urządzeniami.  Hello [samouczki zarządzania urządzeniami] [ lnk-get-started] przedstawia bardziej szczegółowo sposób tooextend toofit te wzorce dokładne scenariusz i jak nowe wzorce toodesign oparte na tych podstawowych szablonów.

* **Ponowny rozruch** -hello zaplecza aplikacji informuje hello urządzenia za pomocą metody bezpośredniego czy zainicjował ponowne uruchomienie komputera.  Witaj Witaj używa urządzenie zgłosiło ono właściwości tooupdate hello ponowny rozruch stanu hello urządzenia.
  
    ![Ilustracja dotycząca wzorca ponownego uruchamiania zarządzania urządzeniami][img-reboot_pattern]
* **Resetowanie do ustawień fabrycznych** -hello zaplecza aplikacji informuje hello urządzenia za pomocą metody bezpośredniego czy zainicjował resetowania do ustawień fabrycznych.  Witaj urządzenie używa Witaj zgłosił, że właściwości tooupdate hello fabryki zresetowania stanu hello urządzenia.
  
    ![Ilustracja dotycząca wzorca resetowania urządzenia do ustawień fabrycznych zarządzania urządzeniami][img-facreset_pattern]
* **Konfiguracja** -hello zaplecza aplikacji przy użyciu oprogramowania tooconfigure właściwości hello potrzeby uruchamiania na urządzeniu hello.  Witaj Witaj używa urządzenia zgłosiła stan konfiguracji tooupdate właściwości hello urządzenia.
  
    ![Ilustracja dotycząca wzorca konfiguracji zarządzania urządzeniami][img-config_pattern]
* **Aktualizacja oprogramowania układowego** -hello zaplecza aplikacji informuje hello urządzenia za pomocą metody bezpośredniego czy zainicjował aktualizacji oprogramowania.  urządzenie Hello inicjuje obraz wieloetapowego procesu toodownload hello oprogramowania układowego Zastosuj hello oprogramowania układowego obrazu, a na koniec ponownie toohello usługi IoT Hub.  W trakcie procesu wieloetapowego hello hello urządzenie używa hello zgłosił właściwości tooupdate hello postęp i stan hello urządzenia.
  
    ![Ilustracja dotycząca wzorca aktualizacji oprogramowania układowego zarządzania urządzeniami][img-fwupdate_pattern]
* **Raportowanie postęp i stan** -zaplecza rozwiązania hello obsługuje kwerendy dwie urządzenia, na zbiór urządzeń, tooreport na powitania stan i postęp działań uruchamianych na urządzeniach hello.
  
    ![Ilustracja dotycząca postępu i stanu raportowania zarządzania urządzeniami][img-report_progress_pattern]

## <a name="next-steps"></a>Następne kroki
możliwości Hello, wzorców i biblioteki kodu, dostępnych w Centrum IoT do zarządzania urządzeniami, Włącz toocreate IoT aplikacje, które spełniają wymagania operator IoT przedsiębiorstwa w ramach każdego etapu cyklu życia urządzenia.

toocontinue poznawania hello funkcje zarządzania urządzeniami w Centrum IoT, zobacz hello [wprowadzenie do zarządzania urządzeniami] [ lnk-get-started] samouczka.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
