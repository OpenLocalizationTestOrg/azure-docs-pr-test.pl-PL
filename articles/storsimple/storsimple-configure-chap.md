---
title: "aaaConfigure protokołu CHAP dla urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello protokół uwierzytelniania typu Challenge Handshake (CHAP) na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>Konfigurowanie protokołu CHAP dla urządzenia StorSimple
W tym samouczku wyjaśniono, jak tooconfigure protokołu CHAP dla urządzenia StorSimple. procedury Hello szczegółowo opisane w tym artykule dotyczą serii 8000 tooStorSimple, a także urządzenia StorSimple 1200.

Protokół uwierzytelniania typu Challenge Handshake oznacza protokołu CHAP. Jest schemat uwierzytelniania używany przez serwery toovalidate hello tożsamości klientów zdalnych. Weryfikacja Hello jest oparta na wspólne hasło lub klucz tajny. Protokół CHAP, może być jednokierunkowe (jednokierunkowe) lub wzajemne (dwukierunkowe). Jednokierunkowe CHAP jest w przypadku docelowej hello uwierzytelnia inicjatora. Wzajemne lub wstecznego protokołu CHAP, na powitania drugiej strony, wymaga, aby docelowy hello uwierzytelniania inicjatora hello i następnie inicjatora hello uwierzytelniania hello docelowej. Inicjator może być realizowane bez uwierzytelnienia docelowego. Jednak docelowym może być realizowane tylko wtedy, gdy uwierzytelnianie inicjatora również jest zaimplementowana. 

Najlepszym rozwiązaniem zaleca się użycie zabezpieczeń iSCSI tooenhance protokołu CHAP.

> [!NOTE]
> Należy pamiętać, że protokół IPSEC nie jest obecnie obsługiwane urządzenia StorSimple.
> 
> 

można skonfigurować ustawienia protokołu CHAP Hello na urządzeniu StorSimple hello w hello następujące sposoby:

* Uwierzytelnianie jednokierunkowe lub jednokierunkowe
* Dwukierunkowy lub uwierzytelniania wzajemnego lub wstecznego

W każdym z tych przypadków portal hello hello urządzeń i oprogramowania inicjatora iSCSI serwera hello musi toobe skonfigurowany. Witaj szczegółowe informacje na temat tej konfiguracji zostały opisane w hello samouczka.

## <a name="unidirectional-or-one-way-authentication"></a>Uwierzytelnianie jednokierunkowe lub jednokierunkowe
W jednokierunkowe uwierzytelniania docelowy hello uwierzytelnia hello inicjatora. To uwierzytelnianie wymaga skonfigurowania ustawień inicjatora protokołu CHAP hello na powitania urządzenia StorSimple i hello oprogramowaniem iSCSI Initiator na hoście hello. Witaj szczegółowe procedury dotyczące urządzenia StorSimple i hosta systemu Windows są opisane w dalszej części.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure Twojego urządzenia pod kątem uwierzytelniania jednokierunkowe
1. W hello klasycznego portalu Azure na powitania **urządzeń** kliknij przycisk hello **Konfiguruj** kartę.
   
    ![Inicjatora protokołu CHAP](./media/storsimple-configure-chap/IC740943.png)
2. Przewiń w dół na tej stronie, a w hello **inicjatora protokołu CHAP** sekcji:
   
   1. Podaj nazwę użytkownika dla użytkownika inicjatora protokołu CHAP.
   2. Podaj hasło dla użytkownika inicjatora protokołu CHAP.
      
    > [!IMPORTANT]
    > Nazwa użytkownika protokołu CHAP Hello musi zawierać mniej niż 233 znaków. Hasło protokołu CHAP Hello musi należeć do zakresu od 12 do 16 znaków. Wystąpił błąd uwierzytelniania na hoście Windows hello spowoduje dłużej nazwa użytkownika lub hasło.
   
   3. Potwierdź hasło hello.
3. Kliknij pozycję **Zapisz**. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **OK** toosave hello zmiany.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>tooconfigure jednokierunkowe uwierzytelniania w systemie Windows hello serwerze hosta
1. Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.
2. W hello **właściwości inicjatora iSCSI** okna, wykonaj następujące kroki hello:
   
   1. Kliknij przycisk hello **odnajdywania** kartę.
      
       ![Właściwości inicjatora iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. Kliknij przycisk **odnajdź Portal**.
3. W hello **odnajdowanie portalu obiektu docelowego** okno dialogowe:
   
   1. Określ adres IP hello urządzenia.
   2. Kliknij przycisk **zaawansowane**.
      
       ![Odnajdowanie portalu obiektu docelowego](./media/storsimple-configure-chap/IC740945.png)
4. W hello **Zaawansowane ustawienia** okno dialogowe:
   
   1. Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.
   2. W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.
   3. W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.
   4. Kliknij przycisk **OK**.
      
       ![Zaawansowane ustawienia ogólne](./media/storsimple-configure-chap/IC740946.png)
5. Na powitania **celów** kartę hello **właściwości inicjatora iSCSI** okna, stan urządzenia hello powinny się wyświetlać jako **połączony**. Jeśli używasz urządzenia StorSimple 1200 następnie każdy wolumin zostanie zainstalowany jako obiektu docelowego iSCSI w sposób przedstawiony poniżej. W związku z tym kroki 3 i 4 należy powtórzyć dla każdego woluminu toobe.
   
    ![Woluminów zainstalowanych jako osobne cele](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Jeśli zmienisz nazwę iSCSI hello hello nową nazwę będzie służyć do nowej sesji iSCSI. Nowe ustawienia nie są ponownie używane istniejące sesje aż do wylogowywania i logowania.
   > 
   > 

Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Dwukierunkowy lub wzajemnego uwierzytelniania
W uwierzytelnianiu dwukierunkowego docelowy hello umożliwiają uwierzytelnienie inicjatora hello a następnie inicjatora hello hello docelowej. Wymaga to hello tooconfigure hello CHAP inicjatora ustawień, a także hello odwrócić ustawień protokołu CHAP na powitania urządzeniami i oprogramowaniem iSCSI Initiator na hoście hello. Witaj poniższe procedury opisują hello kroki tooconfigure wzajemnego uwierzytelniania na powitania urządzeniu i na hoście Windows hello.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure Twojego urządzenia pod kątem wzajemnego uwierzytelniania
1. W hello klasycznego portalu Azure na powitania **urządzeń** kliknij przycisk hello **Konfiguruj** kartę.
   
    ![Obiektu docelowego protokołu CHAP](./media/storsimple-configure-chap/IC740948.png)
2. Przewiń w dół na tej stronie, a w hello **docelowego protokołu CHAP** sekcji:
   
   1. Podaj **nazwy użytkownika** dla danego urządzenia.
   2. Podaj **wstecznego protokołu CHAP hasła** dla danego urządzenia.
   3. Potwierdź hasło hello.
3. W hello **inicjatora protokołu CHAP** sekcji:
   
   1. Podaj **nazwy użytkownika** dla danego urządzenia.
   2. Podaj **hasło** dla danego urządzenia.
   3. Potwierdź hasło hello.
4. Kliknij pozycję **Zapisz**. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **OK** toosave hello zmiany.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>tooconfigure dwukierunkowego uwierzytelniania w systemie Windows hello serwerze hosta
1. Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.
2. W hello **właściwości inicjatora iSCSI** okna, kliknij przycisk hello **konfiguracji** kartę.
3. Kliknij przycisk **protokołu CHAP**.
4. W hello **wzajemnego protokołu CHAP klucz tajny inicjatora iSCSI** okno dialogowe:
   
   1. Typ hello **wstecznego protokołu CHAP hasła** skonfigurowanego w hello klasycznego portalu Azure.
   2. Kliknij przycisk **OK**.
      
       ![wzajemne tajny protokołu CHAP inicjatora iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. Kliknij przycisk hello **cele** kartę.
6. Kliknij przycisk hello **Connect** przycisku. 
7. W hello **połączyć tooTarget** okno dialogowe, kliknij przycisk **zaawansowane**.
8. W hello **właściwości zaawansowane** okno dialogowe:
   
   1. Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.
   2. W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.
   3. W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.
   4. Wybierz hello **wykonaj wzajemnego uwierzytelniania** pole wyboru.
      
       ![Ustawienia zaawansowane wzajemnego uwierzytelniania.](./media/storsimple-configure-chap/IC740950.png)
   5. Kliknij przycisk **OK** toocomplete hello CHAP konfiguracji

Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).

## <a name="additional-considerations"></a>Dodatkowe zagadnienia
Witaj **szybkie połączenie** funkcja nie obsługuje połączeń, które mają włączony protokół CHAP. Po włączeniu protokołu CHAP, upewnij się, że używasz hello **Connect** przycisku, który jest dostępny na powitania **cele** kartę tooconnect tooa docelowej.

![Połącz tootarget](./media/storsimple-configure-chap/IC740947.png)

W hello **połączyć tooTarget** dialogowe hello przedstawioną, wybierz pozycję **Dodawanie połączenia tej toohello lista ulubionych elementów docelowych** pole wyboru. Dzięki temu, że przy każdym uruchomieniu komputera hello podejmowana jest próba toorestore hello połączenia toohello ulubionych obiektów docelowych iSCSI.

## <a name="errors-during-configuration"></a>Błędy podczas konfiguracji
Jeśli konfiguracja protokołu CHAP jest niepoprawny, a następnie są prawdopodobnie toosee **niepowodzenie uwierzytelniania** komunikat o błędzie.

## <a name="verification-of-chap-configuration"></a>Weryfikacja konfiguracji protokołu CHAP
Aby sprawdzić, czy, wykonując następujące kroki hello jest używany protokół CHAP.

#### <a name="tooverify-your-chap-configuration"></a>tooverify konfiguracji protokołu CHAP
1. Kliknij przycisk **Ulubione obiekty docelowe**.
2. Wybierz cel hello, dla której jest włączone uwierzytelnianie.
3. Kliknij przycisk **szczegóły**.
   
    ![Inicjator właściwości ulubionych obiektów docelowych iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. W hello **ulubionych szczegóły docelowej** okno dialogowe, wpisu notatki hello w hello **uwierzytelniania** pola. Jeśli konfiguracja hello zakończyło się pomyślnie, powinien powiedzieć **protokołu CHAP**.
   
    ![Szczegóły ulubiony obiekt docelowy](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-security.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

