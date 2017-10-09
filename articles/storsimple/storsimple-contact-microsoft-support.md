---
title: aaaLog biletu pomocy technicznej dla serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak żądania toocreate pomocy technicznej i rozpocząć sesję pomocy technicznej na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Skontaktuj się z pomocą techniczną firmy Microsoft dla Twojego urządzenia StorSimple
Jeśli wystąpią problemy z rozwiązania Microsoft Azure StorSimple można utworzyć żądania obsługi technicznej. W ramach sesji online ze specjalistą pomocy technicznej możesz także toostart sesję pomocy technicznej na urządzeniu StorSimple. W tym artykule przedstawiono:

* Jak toocreate obsługi żądania.
* Jak toostart sesję pomocy technicznej w hello interfejsu programu Windows PowerShell urządzenia StorSimple.

Przejrzyj hello [StorSimple 8000 serii Obsługa SLA oraz informacje](https://msdn.microsoft.com/library/mt433077.aspx) przed utworzeniem żądania pomocy technicznej.

## <a name="create-a-support-request"></a>Utwórz żądanie obsługi
Wykonaj hello następujące kroki toocreate żądania pomocy technicznej:

#### <a name="toocreate-a-support-request"></a>toocreate żądania obsługi
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), w hello prawym górnym rogu kliknij nazwę konta, a następnie kliknij przycisk **skontaktuj się z pomocą techniczną firmy Microsoft**.
   
    ![MS skontaktuj się z pomocą techniczną przez ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Będzie przekierowany toohello nowego portalu Azure (portal.azure.com). Kliknij przycisk hello **nowy obsługuje żądania** kafelka.
   
    ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Po prawej stronie powitania ekranie powitania, hello **nowy obsługuje żądania** pojawi się okienko. 
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. W hello **podstawy** okno dialogowe, pełną hello następujące:                                
   
   1. Z hello **wydawania typu** listy rozwijanej wybierz **techniczne**.
   2. Wybierz **subskrypcji** z listy rozwijanej hello.
   3. Z hello **usługi** listy rozwijanej wybierz **StorSimple**. 
   4. Wybierz **plan pomocy technicznej** z listy rozwijanej hello. Należy tooenable plan płatnej pomocy technicznej, pomocy technicznej.
4. Kliknij przycisk **Dalej**. Witaj **Problem** zostanie wyświetlone okno dialogowe.
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. W hello **Problem** okno dialogowe, pełną hello następujące:
   
   1. Wybierz **ważność** poziomu z listy rozwijanej hello.
   2. Wybierz **typ problemu** z listy rozwijanej hello.
   3. Wybierz **kategorii** z listy rozwijanej hello. 
   4. W hello **szczegóły** polu Zwięźle opisz swój problem.
   5. W hello **okresie** należy wskazać hello datę, godzinę i strefę czasową, która odpowiada toohello ostatniego wystąpienia problemu.
   6. W obszarze **przekazywania pliku**, kliknij przycisk hello folderu ikona toobrowse tooyour pomocy technicznej pakietu.
   7. Wybierz hello **udostępnianie informacji diagnostycznych** pole wyboru.
6. Kliknij przycisk **Dalej**. Witaj **informacje kontaktowe** zostanie wyświetlone okno dialogowe.
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Wprowadź swoje informacje kontaktowe i wybierz metodę kontaktu (telefonu lub poczty e-mail). 
8. Wybierz hello **Zapisz zmiany dotyczące kontaktu dla przyszłych żądań obsługi** pole wyboru.
9. Kliknij przycisk **Utwórz**.

Gdy prześlesz żądanie z pracownikiem pomocy technicznej skontaktuje się z Tobą jak najszybciej tooproceed w żądaniu.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Rozpocznij sesję pomocy technicznej w programie Windows PowerShell dla urządzenia StorSimple
tootroubleshoot wszelkie problemy, które mogą wystąpić z urządzeniem StorSimple hello, konieczne będzie tooengage z zespołem Microsoft Support hello. Microsoft Support może być konieczne toouse toolog sesji pomocy technicznej, na urządzeniu tooyour. 

Wykonaj następujące hello kroki toostart sesję pomocy technicznej:

#### <a name="toostart-a-support-session"></a>toostart sesję pomocy technicznej
1. Urządzenie hello dostępu bezpośrednio za pomocą konsoli szeregowej hello lub za pośrednictwem sesji telnet z komputera zdalnego. toodo, wykonaj kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. W sesji hello, który zostanie otwarty, naciśnij klawisz hello **Enter** tooget klucza wiersza polecenia.
3. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.
4. W wierszu hello wpisz hello następującego hasła: 
   
    `Password1`
5. W wierszu hello wpisz hello następujące polecenie:
   
    `Enable-HcsSupportAccess`
6. Tooyou zostanie wyświetlone zaszyfrowanego ciągu. Skopiuj ten ciąg do edytora tekstu, takiego jak Notatnik.
7. Zapisz ten ciąg i wysyłać je w tooMicrosoft wiadomości e-mail pomocy technicznej. 

> [!IMPORTANT]
> Dostęp do pomocy technicznej można wyłączyć, uruchamiając `Disable-HcsSupportAccess`. urządzenia StorSimple Hello będzie również próbują uzyskać dostęp do pomocy technicznej toodisable, 8 godzin po hello sesji zostało zainicjowane. Jest najlepszym toochange praktyki urządzenia StorSimple poświadczenia po zainicjowaniu sesji pomocy technicznej.
> 
> 

