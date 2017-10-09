---
title: "aaaSet się serwera proxy sieci web dla urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse środowiska Windows PowerShell dla StorSimple tooconfigure sieci web ustawienia serwera proxy dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Skonfiguruj serwer proxy sieci web dla urządzenia StorSimple

## <a name="overview"></a>Omówienie

Ten przewodnik opisuje sposób toouse środowiska Windows PowerShell dla StorSimple tooconfigure i widoku sieci web ustawienia serwera proxy dla urządzenia StorSimple. ustawienia serwera proxy sieci web Hello są używane przez urządzenia StorSimple hello podczas komunikowania się z chmurą hello. Serwer proxy sieci web jest używana tooadd kolejna warstwa zabezpieczeń, filtrowanie zawartości pamięci podręcznej tooease wymaganiach odnośnie do przepustowości lub nawet pomocy analizy.

wskazówki dotyczące Hello w tym samouczku dotyczy tylko tooStorSimple 8000 fizycznych urządzeń z serii. Konfiguracja serwera proxy sieci Web nie jest obsługiwana na powitania urządzenia chmury StorSimple (urządzenia 8010 i 8020).

Serwer proxy sieci Web jest _opcjonalne_ konfiguracji dla urządzenia StorSimple. Możesz skonfigurować serwer proxy sieci web tylko przy użyciu programu Windows PowerShell dla urządzenia StorSimple. Konfiguracja Hello jest procesem dwuetapowym w następujący sposób:

1. Skonfiguruj ustawienia serwera proxy sieci web za pomocą Kreatora instalacji hello lub środowiska Windows PowerShell dla StorSimple polecenia cmdlet.
2. Następnie włącz hello skonfigurowane ustawienia serwera proxy sieci web za pomocą środowiska Windows PowerShell dla StorSimple poleceń cmdlet.

Po zakończeniu konfiguracji serwera proxy sieci web hello można wyświetlić ustawienia serwera proxy sieci web hello skonfigurowany zarówno usługi Microsoft Azure StorSimple Menedżer urządzeń hello i hello środowiska Windows PowerShell dla urządzenia StorSimple.

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Skonfiguruj serwer proxy sieci web przy użyciu Kreatora instalacji i poleceń cmdlet.
* Włącz serwer proxy sieci web przy użyciu poleceń cmdlet.
* Wyświetl ustawienia serwera proxy sieci web w hello portalu Azure.
* Rozwiązywanie błędów podczas konfigurowania serwera proxy sieci web.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Skonfiguruj serwer proxy sieci web za pomocą środowiska Windows PowerShell dla urządzenia StorSimple

Można użyć jednej z następujących ustawień serwera proxy sieci web tooconfigure hello:

* Ustawienia kreatora tooguide użytkownika przez kroki konfiguracji hello.
* Polecenia cmdlet programu Windows PowerShell dla StorSimple.

Każda z tych metod jest omówiona w hello następujące sekcje.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Skonfiguruj serwer proxy sieci web za pomocą Kreatora instalacji hello

Użyj hello tooguide Kreatora instalacji, który prowadzi użytkownika przez proces hello konfiguracji serwera proxy sieci web. Wykonaj hello następującego serwera proxy sieci web tooconfigure kroki na urządzeniu.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>Serwer proxy sieci web tooconfigure za pomocą Kreatora instalacji hello

1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu** i podaj hello **hasło administratora urządzenia**. Typ hello następujące polecenie toostart sesję kreatora instalacji:
   
    `Invoke-HcsSetupWizard`
2. Hello jest użycie hello Kreator w czasie rejestracji urządzenia po raz pierwszy, należy najpierw tooconfigure wszystkie ustawienia sieciowe hello wymagane aż do konfiguracji serwera proxy sieci web hello. Jeśli urządzenie jest już zarejestrowany, Zaakceptuj wszystkie ustawienia sieciowe skonfigurowane hello aż do konfiguracji serwera proxy sieci web hello. W Kreatorze instalacji hello, gdy zostanie wyświetlony monit o tooconfigure ustawienia serwera proxy w sieci web, wpisz **tak**.
3. Dla hello **adres URL serwera Proxy sieci Web**, określ adres IP hello lub hello w pełni kwalifikowaną nazwę domeny (FQDN) z sieci web serwera i hello TCP numer portu serwera proxy czy chcesz toouse Twojego urządzenia podczas komunikacji z chmurą hello. Witaj Użyj następującego formatu:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Domyślnie jest określony numer portu TCP 8080.
4. Wybierz typ uwierzytelniania hello jako **NTLM**, **podstawowe**, lub **Brak**. Podstawowa jest hello najmniej bezpiecznego uwierzytelniania dla konfiguracji serwera proxy hello. NT LAN Manager (NTLM) to protokół uwierzytelniania wysokiego poziomu zabezpieczeń i złożone korzystającym z systemu obsługi wiadomości trzystopniowo, (czasami cztery Jeśli wymagane jest dodatkowe integralności) tooauthenticate użytkownika. Witaj domyślne uwierzytelnianie to NTLM. Aby uzyskać więcej informacji, zobacz [podstawowe](http://hc.apache.org/httpclient-3.x/authentication.html) i [uwierzytelniania NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **W hello usługi Menedżer urządzeń StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. Dla hello monitorowania toowork wykresy, potrzebujesz tooensure uwierzytelniania ustawiono tooNONE.**
  
5. Włączenie uwierzytelniania hello podać **nazwa użytkownika serwera Proxy sieci Web** i **hasło serwera Proxy sieci Web**. Należy również tooconfirm hello hasła.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device1](./media/storsimple-configure-web-proxy/IC751830.png)

W przypadku rejestracji urządzenia na powitania po raz pierwszy, kontynuuj hello rejestracji. Jeśli urządzenie zostało już zarejestrowane, Kreator hello zamknięte. Witaj skonfigurowane ustawienia są zapisywane.

Serwer proxy sieci Web jest teraz włączony. Można pominąć hello [włączyć serwer proxy sieci web](#enable-web-proxy) kroku i przejść bezpośrednio za[wyświetlić ustawienia serwera proxy sieci web w portalu Azure hello](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Skonfiguruj serwer proxy sieci web za pomocą środowiska Windows PowerShell dla StorSimple poleceń cmdlet

Ustawienia serwera proxy sieci web alternatywny sposób tooconfigure odbywa się za pośrednictwem hello środowiska Windows PowerShell dla StorSimple poleceń cmdlet. Wykonaj hello następującego serwera proxy sieci web tooconfigure czynności.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>Serwer proxy sieci web tooconfigure za pomocą poleceń cmdlet
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Wprowadź i Potwierdź hasło powitania po wyświetleniu monitu.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device3](./media/storsimple-configure-web-proxy/IC751831.png)

Serwer proxy sieci web Hello jest teraz skonfigurowane i musi toobe włączone.

## <a name="enable-web-proxy"></a>Włącz serwer proxy sieci web

Serwer proxy sieci Web jest domyślnie wyłączona. Po skonfigurowaniu ustawień serwera proxy sieci web hello na urządzeniu StorSimple, użyj hello środowiska Windows PowerShell dla ustawień serwera proxy sieci web hello tooenable StorSimple.

> [!NOTE]
> **Ten krok nie jest wymagane, jeśli używasz serwera proxy sieci web tooconfigure hello ustawienia kreatora. Serwer proxy sieci Web automatycznie jest domyślnie włączona po sesji kreatora instalacji.**


Wykonaj następujące kroki w programie Windows PowerShell dla serwera proxy sieci web tooenable StorSimple na urządzeniu hello:

#### <a name="tooenable-web-proxy"></a>Serwer proxy sieci web tooenable
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Enable-HcsWebProxy`
   
    Konfiguracja serwera proxy sieci web hello ma teraz włączone na urządzeniu StorSimple.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a>Wyświetl ustawienia serwera proxy sieci web w portalu Azure hello

ustawienia serwera proxy sieci web Hello są skonfigurowane za pomocą interfejsu programu Windows PowerShell hello i nie można zmienić w portalu hello. Można jednak przeglądać te ustawienia skonfigurowane w portalu hello. Wykonaj hello następującego serwera proxy sieci web tooview czynności.

#### <a name="tooview-web-proxy-settings"></a>ustawienia serwera proxy sieci web tooview
1. Przejdź za**usługi Menedżer StorSimple urządzenia > urządzenia**. Wybierz i kliknij urządzenie, a następnie przejdź zbyt**ustawienia urządzenia > sieci**.

    ![Kliknij sieć](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. W hello **ustawień sieciowych** bloku, kliknij przycisk hello **serwer proxy sieci Web** kafelka.

    ![Kliknij serwer proxy sieci web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. W hello **serwer proxy sieci Web** bloku ustawienia serwera proxy sieci web Przejrzyj hello skonfigurowane na urządzeniu StorSimple.
   
    ![Wyświetl ustawienia serwera proxy sieci web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Błędy podczas konfiguracji serwera proxy sieci web

Jeśli ustawienia serwera proxy sieci web hello jest niepoprawnie skonfigurowana, komunikaty o błędach są wyświetlane toohello użytkownika w programie Windows PowerShell dla urządzenia StorSimple. Witaj w poniższej tabeli omówiono te komunikaty o błędach, ich prawdopodobne przyczyny i zalecane działania.

| Numer porządkowy. | Błąd HRESULT kodu | Możliwe przyczyny | Zalecane działanie |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Polecenie jest uruchamiane z kontrolera pasywnym hello i nie jest możliwe toocommunicate z aktywnym kontrolerze hello. |Uruchom polecenie hello na aktywnym kontrolerze hello. polecenie hello toorun z kontrolera pasywnym hello, musisz naprawić hello łączności z kontrolera tooactive pasywnych. Microsoft Support musi Uwzględnij, jeśli to połączenie zostanie przerwane. |
| 2. |0x800710dd — identyfikator operacji hello jest nieprawidłowa |Ustawienia serwera proxy nie są obsługiwane na urządzeniu chmury StorSimple. |Ustawienia serwera proxy nie są obsługiwane na urządzeniu chmury StorSimple. Można je skonfigurować tylko na urządzeniu fizycznym StorSimple. |
| 3. |0x80070057 — nieprawidłowy parametr |Jeden z parametrów hello podanych ustawień serwera proxy hello jest nieprawidłowy. |nie podano identyfikatora URI Hello w poprawnym formacie. Witaj Użyj następującego formatu:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706BA — serwer RPC jest niedostępny |Hello główną przyczyną jest jedną z następujących hello:</br></br>Klaster nie jest w górę. </br></br>Usługa ścieżki danych nie jest uruchomiona.</br></br>polecenie Hello z pasywnym kontrolera i nie jest możliwe toocommunicate z aktywnym kontrolerze hello. |Komunikować tooensure Support firmy Microsoft, który hello klastra jest uruchomiony i działa usługa ścieżki danych.</br></br>Uruchom polecenie hello na aktywnym kontrolerze hello. Jeśli chcesz, aby polecenie hello toorun z kontrolera pasywnym hello, musi Sprawdź, czy ten kontroler pasywnym hello może komunikować się z aktywnym kontrolerze hello. Microsoft Support musi Uwzględnij, jeśli to połączenie zostanie przerwane. |
| 5. |0x800706be - wywołanie RPC nie powiodło się |Klaster jest wyłączony. |Uwzględnij Microsoft Support tooensure, który hello klastra jest uruchomiony. |
| 6. |0x8007138f — nie można odnaleźć zasobu klastra |Nie znaleziono zasobu klastra usługi platformy. Może to być spowodowane hello instalacja nie jest właściwe. |Może być konieczne tooperform resetowania urządzenia do ustawień fabrycznych. Może być konieczne toocreate zasobów platformy. Skontaktuj się z Microsoft Support następnych kroków. |
| 7. |0x8007138c - zasób klastra nie w trybie online |Zasoby klastra platformy lub ścieżki danych nie są online. |Skontaktuj się z pomocą toohelp Microsoft Support upewnij się, zasobów usługi ścieżki danych i platforma hello są w trybie online. |

> [!NOTE]
> * Witaj powyżej listę komunikatów o błędach nie jest pełna.
> * Ustawienia serwera proxy tooweb powiązane błędy nie pojawi się w portalu Azure w usłudze Menedżer StorSimple urządzenia hello. Jeśli wystąpi problem z serwera proxy sieci web po zakończeniu konfiguracji hello, hello urządzenia stan zmieni się zbyt**Offline** w portalu klasycznym hello. |

## <a name="next-steps"></a>Następne kroki
* Jeśli wystąpią problemy podczas wdrażania urządzenia lub konfigurowanie ustawień serwera proxy sieci web można znaleźć zbyt[rozwiązywania problemów z wdrożeniem urządzenia StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn jak toouse hello usługi Menedżer StorSimple urządzeń, przejdź zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

