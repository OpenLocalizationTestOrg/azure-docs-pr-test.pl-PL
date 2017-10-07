---
title: "aaaSet się serwera proxy sieci web dla urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse środowiska Windows PowerShell dla StorSimple tooconfigure sieci web ustawienia serwera proxy dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Skonfiguruj serwer proxy sieci web dla urządzenia StorSimple
## <a name="overview"></a>Omówienie
Ten przewodnik opisuje sposób toouse środowiska Windows PowerShell dla StorSimple tooconfigure i widoku sieci web ustawienia serwera proxy dla urządzenia StorSimple. ustawienia serwera proxy sieci web Hello są używane przez urządzenia StorSimple hello podczas komunikowania się z chmurą hello. Serwer proxy sieci web jest używana tooadd kolejna warstwa zabezpieczeń, filtrowanie zawartości pamięci podręcznej tooease wymaganiach odnośnie do przepustowości lub nawet pomocy analizy.

Serwer proxy sieci Web jest opcjonalnym dla urządzenia StorSimple. Możesz skonfigurować serwer proxy sieci web tylko przy użyciu programu Windows PowerShell dla urządzenia StorSimple. Konfiguracja Hello jest procesem dwuetapowym w następujący sposób:

1. Skonfiguruj ustawienia serwera proxy sieci web za pomocą Kreatora instalacji hello lub środowiska Windows PowerShell dla StorSimple polecenia cmdlet.
2. Następnie włącz hello skonfigurowane ustawienia serwera proxy sieci web za pomocą środowiska Windows PowerShell dla StorSimple poleceń cmdlet.

Po zakończeniu konfiguracji serwera proxy sieci web hello można wyświetlić ustawienia serwera proxy sieci web hello skonfigurowane w hello usługi Microsoft Azure StorSimple Manager i hello środowiska Windows PowerShell dla urządzenia StorSimple. 

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Skonfiguruj serwer proxy sieci web przy użyciu Kreatora instalacji i poleceń cmdlet
* Włącz serwer proxy sieci web za pomocą poleceń cmdlet
* Wyświetl ustawienia serwera proxy sieci web w hello klasycznego portalu Azure
* Rozwiązywanie błędów podczas konfigurowania serwera proxy sieci web

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Skonfiguruj serwer proxy sieci web za pomocą środowiska Windows PowerShell dla urządzenia StorSimple
Można użyć jednej z następujących ustawień serwera proxy sieci web tooconfigure hello:

* Ustawienia kreatora tooguide użytkownika przez kroki konfiguracji hello.
* Polecenia cmdlet programu Windows PowerShell dla StorSimple.

Każda z tych metod jest omówiona w hello następujące sekcje.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Skonfiguruj serwer proxy sieci web za pomocą Kreatora instalacji hello
Hello tooguide Kreatora instalacji, który prowadzi użytkownika przez proces hello służy do konfiguracji serwera proxy sieci web. Wykonaj hello następującego serwera proxy sieci web tooconfigure kroki na urządzeniu.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>Serwer proxy sieci web tooconfigure za pomocą Kreatora instalacji hello
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu** i podaj hello **hasło administratora urządzenia**. Typ hello następujące polecenie toostart sesję kreatora instalacji:
   
    `Invoke-HcsSetupWizard`
2. Jeśli jest to hello czy użyto Kreatora instalacji hello w czasie rejestracji urządzenia po raz pierwszy, konieczne będzie tooconfigure wszystkie ustawienia sieciowe hello wymagane aż do konfiguracji serwera proxy sieci web hello. Jeśli urządzenie jest już zarejestrowany, aż do konfiguracji serwera proxy sieci web hello można zaakceptować wszystkie hello skonfigurowane ustawienia sieci. W Kreatorze instalacji hello, gdy zostanie wyświetlony monit o tooconfigure ustawienia serwera proxy w sieci web, wpisz **tak**.
3. Dla hello **adres URL serwera Proxy sieci Web**, określ adres IP hello lub hello w pełni kwalifikowaną nazwę domeny (FQDN) z sieci web serwera i hello TCP numer portu serwera proxy czy chcesz toouse Twojego urządzenia podczas komunikacji z chmurą hello. Witaj Użyj następującego formatu:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Domyślnie jest określony numer portu TCP 8080.
4. Wybierz typ uwierzytelniania hello jako **NTLM**, **podstawowe**, lub **Brak**. Podstawowa jest hello najmniej bezpiecznego uwierzytelniania dla konfiguracji serwera proxy hello. NT LAN Manager (NTLM) to protokół uwierzytelniania wysokiego poziomu zabezpieczeń i złożone korzystającym z systemu obsługi wiadomości trzystopniowo, (czasami cztery Jeśli wymagane jest dodatkowe integralności) tooauthenticate użytkownika. Witaj domyślne uwierzytelnianie to NTLM. Aby uzyskać więcej informacji, zobacz [podstawowe](http://hc.apache.org/httpclient-3.x/authentication.html) i [uwierzytelniania NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **W hello usługi Menedżer StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. Dla hello monitorowania toowork wykresy, konieczne będzie tooensure uwierzytelniania ustawiono tooNONE.**
   > 
   > 
5. Jeśli używasz uwierzytelniania, podaj **nazwa użytkownika serwera Proxy sieci Web** i **hasło serwera Proxy sieci Web**. Należy również tooconfirm hello hasła.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device1](./media/storsimple-configure-web-proxy/IC751830.png)

W przypadku rejestracji urządzenia na powitania po raz pierwszy, kontynuuj hello rejestracji. Jeśli urządzenie zostało już zarejestrowane, hello Kreator zakończy pracę. Witaj skonfigurowane ustawienia zostaną zapisane.

Serwer proxy sieci Web zostanie również być włączone. Można pominąć hello [włączyć serwer proxy sieci web](#enable-web-proxy) kroku i przejść bezpośrednio za[wyświetlić ustawienia serwera proxy sieci web w hello klasycznego portalu Azure](#view-web-proxy-settings-in-the-azure-classic-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Skonfiguruj serwer proxy sieci web za pomocą środowiska Windows PowerShell dla StorSimple poleceń cmdlet
Ustawienia serwera proxy sieci web alternatywny sposób tooconfigure odbywa się za pośrednictwem hello środowiska Windows PowerShell dla StorSimple poleceń cmdlet. Wykonaj hello następującego serwera proxy sieci web tooconfigure czynności.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>Serwer proxy sieci web tooconfigure za pomocą poleceń cmdlet
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Wprowadź i Potwierdź hasło powitania po wyświetleniu monitu, jak pokazano poniżej.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device3](./media/storsimple-configure-web-proxy/IC751831.png)

Serwer proxy sieci web Hello jest teraz skonfigurowane i musi toobe włączone.

## <a name="enable-web-proxy"></a>Włącz serwer proxy sieci web
Serwer proxy sieci Web jest domyślnie wyłączona. Po skonfigurowaniu ustawień serwera proxy sieci web hello na urządzeniu StorSimple, należy toouse hello środowiska Windows PowerShell dla ustawień serwera proxy sieci web hello tooenable StorSimple.

> [!NOTE]
> **Ten krok nie będzie wymagane, jeśli używasz serwera proxy sieci web tooconfigure hello ustawienia kreatora. Serwer proxy sieci Web automatycznie jest domyślnie włączona po sesji kreatora instalacji.**
> 
> 

Wykonaj następujące kroki w programie Windows PowerShell dla serwera proxy sieci web tooenable StorSimple na urządzeniu hello:

#### <a name="tooenable-web-proxy"></a>Serwer proxy sieci web tooenable
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Enable-HcsWebProxy`
   
    Konfiguracja serwera proxy sieci web hello ma teraz włączone na urządzeniu StorSimple.
   
    ![Skonfiguruj serwer Proxy sieci Web na StorSimple Device4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Wyświetl ustawienia serwera proxy sieci web w hello klasycznego portalu Azure
ustawienia serwera proxy sieci web Hello są skonfigurowane za pomocą interfejsu programu Windows PowerShell hello i nie można zmienić w portalu klasycznym hello. Można jednak przeglądać te ustawienia skonfigurowane w portalu klasycznym hello. Wykonaj hello następującego serwera proxy sieci web tooview czynności.

#### <a name="tooview-web-proxy-settings"></a>ustawienia serwera proxy sieci web tooview
1. Przejdź za**usługi Menedżer StorSimple > urządzenia**. Wybierz i kliknij urządzenie, a następnie przejdź zbyt**Konfiguruj**.
2. Przewiń w dół hello **Konfiguruj** strony zbyt**ustawienia serwera proxy w sieci Web** sekcji. Można wyświetlić ustawienia serwera proxy sieci web hello skonfigurowane na urządzeniu StorSimple, jak pokazano poniżej.
   
    ![Widok serwera Proxy sieci Web w portalu zarządzania](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>Błędy podczas konfiguracji serwera proxy sieci web
Jeśli ustawienia serwera proxy sieci web hello został niepoprawnie skonfigurowana, komunikaty o błędach będzie wyświetlane toohello użytkownika w programie Windows PowerShell dla urządzenia StorSimple. Witaj w poniższej tabeli omówiono te komunikaty o błędach, ich prawdopodobne przyczyny i zalecane działania.

| Numer porządkowy. | Błąd HRESULT kodu | Możliwe przyczyny | Zalecane działanie |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Polecenie jest uruchamiane z kontrolera pasywnym hello i nie jest możliwe toocommunicate z aktywnym kontrolerze hello. |Uruchom polecenie hello na aktywnym kontrolerze hello. polecenie hello toorun z kontrolera pasywnym hello, konieczne będzie toofix hello łączności z kontrolera tooactive pasywnych. Należy tooengage Support firmy Microsoft, jeśli to połączenie zostanie przerwane. |
| 2. |0x800710dd — identyfikator operacji hello jest nieprawidłowa |Ustawienia serwera proxy nie są obsługiwane na urządzenie wirtualne StorSimple. |Ustawienia serwera proxy nie są obsługiwane na urządzenie wirtualne StorSimple. Można je skonfigurować tylko na urządzeniu fizycznym StorSimple. |
| 3. |0x80070057 — nieprawidłowy parametr |Jeden z parametrów hello podanych ustawień serwera proxy hello jest nieprawidłowy. |nie podano identyfikatora URI Hello w poprawnym formacie. Witaj Użyj następującego formatu:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706BA — serwer RPC jest niedostępny |Hello główną przyczyną jest jedną z następujących hello:</br></br>Klaster nie jest w górę.</br></br>Usługa ścieżki danych nie jest uruchomiona.</br></br>polecenie Hello z pasywnym kontrolera i nie jest możliwe toocommunicate z aktywnym kontrolerze hello. |Sprawdź komunikować tooensure Support firmy Microsoft, który hello klastra jest uruchomiony i działa usługa ścieżki danych.</br></br>Uruchom polecenie hello na aktywnym kontrolerze hello. Jeśli chcesz, aby polecenie hello toorun z kontrolera pasywnym hello, konieczne będzie tooensure hello pasywnym kontroler może komunikować się z aktywnym kontrolerze hello. Należy tooengage Support firmy Microsoft, jeśli to połączenie zostanie przerwane. |
| 5. |0x800706be - wywołanie RPC nie powiodło się |Klaster jest wyłączony. |Sprawdź komunikować tooensure Support firmy Microsoft, który hello klastra jest uruchomiony. |
| 6. |0x8007138f — nie można odnaleźć zasobu klastra |Nie znaleziono zasobu klastra usługi platformy. Może to być spowodowane hello instalacja nie jest właściwe. |Może być konieczne tooperform resetowania urządzenia do ustawień fabrycznych. Może być konieczne toocreate zasobów platformy. Dalsze czynności, skontaktuj się z Microsoft Support. |
| 7. |0x8007138c - zasób klastra nie w trybie online |Zasoby klastra platformy lub ścieżki danych nie są online. |Skontaktuj się z pomocą toohelp Microsoft Support upewnij się, zasobów usługi ścieżki danych i platforma hello są w trybie online. |

> [!NOTE]
> * Witaj powyżej listę komunikatów o błędach nie jest pełna. 
> * Ustawienia serwera proxy tooweb powiązane błędy nie pojawi się w hello klasycznego portalu Azure w usłudze Menedżer StorSimple. Jeśli wystąpi problem z serwera proxy sieci web po zakończeniu konfiguracji hello, hello urządzenia stan zmieni się zbyt**Offline** w portalu klasycznym hello. |
> 
> 

## <a name="next-steps"></a>Następne kroki
* Jeśli wystąpią problemy podczas wdrażania urządzenia lub konfigurowanie ustawień serwera proxy sieci web można znaleźć zbyt[rozwiązywania problemów z wdrożeniem urządzenia StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn jak toouse hello usługi Menedżer StorSimple, przejdź zbyt[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

