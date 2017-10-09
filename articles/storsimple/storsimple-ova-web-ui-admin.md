---
title: "web tablicy wirtualnego aaaStorSimple interfejsu użytkownika administracji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooperform urządzenie podstawowe zadania za pomocą hello interfejsu użytkownika sieci web tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Użyj tooadminister interfejsu użytkownika sieci Web hello tablica wirtualnego StorSimple
![przepływ procesu instalacji](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Omówienie
Witaj w tym artykule samouczkach toohello Microsoft Azure StorSimple wirtualnego tablicy (znanej także jako hello lokalnej urządzenia wirtualnego StorSimple) uruchomionej wersji ogólnodostępnej (GA) marca 2016 r. W tym artykule opisano niektóre hello złożonych przepływów pracy i zadania zarządzania, które mogą być wykonywane na powitania tablicy wirtualnego StorSimple. Możesz zarządzać hello tablicę wirtualnego StorSimple przy użyciu usługi Menedżer StorSimple hello interfejsu użytkownika (portal hello tooas określonego interfejsu użytkownika) i hello lokalnego interfejsu użytkownika sieci web dla hello urządzenia. Ten artykuł skupia się na powitania zadania czy można wykonać przy użyciu interfejsu użytkownika sieci web hello.

Ten artykuł zawiera następujące samouczki hello:

* Pobierz klucz szyfrowania danych usługi hello
* Rozwiąż problemy z błędami ustawień interfejsu użytkownika sieci web
* Generowanie pakietu dziennika
* Zamknięcie lub ponowne uruchomienie urządzenia

## <a name="get-hello-service-data-encryption-key"></a>Pobierz klucz szyfrowania danych usługi hello
Klucz szyfrowania danych usługi jest generowany podczas rejestrowania pierwszego urządzenia z hello usługi Menedżer StorSimple. Ten klucz jest wymagany z hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple.

Jeśli użytkownik ma Zagubione klucz szyfrowania danych usługi i musi tooretrieve, wykonaj następujące hello zarejestrowane kroki lokalne powitania interfejsu użytkownika urządzenia hello sieci web przy użyciu usługi.

#### <a name="tooget-hello-service-data-encryption-key"></a>klucz szyfrowania danych usługi hello tooget
1. Połączenie lokalne toohello interfejsu użytkownika sieci web. Przejdź za**konfiguracji** > **ustawienia chmury**.
2. U dołu hello hello strony, kliknij przycisk **klucza szyfrowania danych usługi Get**. Zostanie wyświetlony klucz. Skopiuj i Zapisz ten klucz.
   
    ![Pobierz klucz szyfrowania danych usługi 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Rozwiąż problemy z błędami ustawień interfejsu użytkownika sieci web
W niektórych przypadkach po skonfigurowaniu urządzenia hello za pośrednictwem sieci web lokalne powitania interfejsu użytkownika, możesz napotkać błędy. toodiagnose i rozwiązywanie tych problemów, można uruchomić testów diagnostycznych hello.

#### <a name="toorun-hello-diagnostic-tests"></a>testów diagnostycznych hello toorun
1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**Rozwiązywanie problemów** > **testów diagnostycznych**.
   
    ![Uruchom funkcję diagnostyki 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. U dołu hello hello strony, kliknij przycisk **uruchamiania testów diagnostycznych**. Spowoduje to zainicjowanie toodiagnose testy możliwe problemy z sieci, urządzenia, serwer proxy sieci web, czas lub ustawienia chmury. Czy urządzenie hello jest uruchomione testy, otrzymasz powiadomienie.
3. Po zakończeniu testów hello, hello wyniki będą wyświetlane. Witaj poniższy przykład przedstawia hello wyniki testów diagnostycznych. Należy pamiętać, że nie skonfigurowano ustawień serwera proxy sieci web hello na tym urządzeniu i w związku z tym testu serwera proxy sieci web hello nie zostało uruchomione. Witaj wszystkich innych testach dla ustawień sieci, serwer DNS i ustawienia czasu zostały pomyślnie.
   
    ![Uruchom funkcję diagnostyki 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Generowanie pakietu dziennika
Pakiet dziennika obejmuje wszystkie dzienniki odpowiednich hello, które mogą pomóc Support firmy Microsoft o wszelkich rozwiązywania problemów z urządzeniami. W tej wersji pakietu dziennika można wygenerować za pomocą lokalne powitania interfejsu użytkownika sieci web.

#### <a name="toogenerate-hello-log-package"></a>toogenerate hello dziennika pakietu
1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**Rozwiązywanie problemów** > **dzienniki systemu**.
   
    ![Generowanie pakietu dziennika 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. U dołu hello hello strony, kliknij przycisk **Utwórz pakiet dziennika**. Zostanie utworzony pakiet hello dzienniki systemu. To może potrwać kilka minut.
   
    ![Generowanie pakietu dziennika 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Po pomyślnym utworzeniu pakietu hello i hello strona będzie aktualizowana tooindicate hello godzina i Data utworzenia pakietu hello, otrzymasz powiadomienie.
   
    ![Generowanie pakietu dziennika 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. Kliknij przycisk **pakiet dziennika**. Pakiet ZIP zostanie pobrana w tym systemie.
   
    ![Generowanie pakietu dziennika 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. Można rozpakować hello dziennika pobranego pakietu i wyświetlać plikach dziennika systemowego hello.

## <a name="shut-down-and-restart-your-device"></a>Zamykanie i ponowne uruchomienie urządzenia
Możesz zamknąć lub ponownie uruchomić urządzenie wirtualne za pomocą lokalne powitania interfejsu użytkownika sieci web. Zalecamy, aby przed ponownego uruchomienia, wykonać hello woluminy lub udziały w tryb offline na hoście hello i następnie hello urządzenia. Pozwoli to zminimalizować możliwości uszkodzenie danych. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut wyłączenia urządzenia wirtualnego
1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **ustawienia zasilania**.
2. U dołu hello hello strony, kliknij przycisk **zamknięcia**.
   
    ![zamknięcie urządzenia 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Zostanie wyświetlone ostrzeżenie, informujący, że wyłączenie urządzenia hello przerywa żadnych we/wy, które były w toku, co spowoduje Przestój. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![Ostrzeżenie zamknięcia urządzenia](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Dowiesz się, że ten shutdown hello została zainicjowana.
   
    ![Rozpoczęto zamknięcia urządzenia](./media/storsimple-ova-web-ui-admin/image38.png)
   
    Witaj urządzenia zostanie teraz zamknięty. Jeśli urządzenie ma toostart należy toodo, który za pomocą hello Menedżera funkcji Hyper-V.

#### <a name="toorestart-your-virtual-device"></a>toorestart urządzenia wirtualnego
1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **ustawienia zasilania**.
2. U dołu hello hello strony, kliknij przycisk **ponownego uruchomienia**.
   
    ![ponowne uruchomienie urządzenia](./media/storsimple-ova-web-ui-admin/image36.png)
3. Zostanie wyświetlone ostrzeżenie, informujący, że ponownie uruchomić urządzenie hello przerywa żadnych IOs, które były w toku, co spowoduje Przestój. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![Ostrzeżenie o ponownym uruchomieniu](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Użytkownik będzie powiadamiany, że ponowne hello została zainicjowana.
   
    ![zainicjowano ponowne uruchomienie](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Podczas ponownego uruchomienia hello jest w toku, utracisz hello połączenia toohello interfejsu użytkownika. Ponowne uruchomienie hello można monitorować okresowo odświeżając hello interfejsu użytkownika. Alternatywnie można monitorować stan ponowne uruchomienie urządzenia hello za pomocą Menedżera funkcji Hyper-V hello.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[Użyj hello toomanage usługi Menedżer StorSimple, urządzenie](storsimple-virtual-array-manager-service-administration.md).

