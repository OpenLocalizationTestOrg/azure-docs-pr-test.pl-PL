---
title: "problemy z aaaTroubleshoot brama zarządzania danymi | Dokumentacja firmy Microsoft"
description: "Zawiera porady tootroubleshoot problemów powiązanych tooData brama zarządzania."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Rozwiązywanie problemów z używaniem bramy zarządzania danymi
Ten artykuł zawiera informacje na temat rozwiązywania problemów przy użyciu bramy zarządzania danymi.

> [!NOTE]
> Zobacz hello [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać szczegółowe informacje o hello bramy. Zobacz hello [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu przewodnik przenoszenia danych z tooMicrosoft bazy danych programu SQL Server lokalnego magazynu obiektów Blob platformy Azure przy użyciu bramy hello.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Nie powiodło się tooinstall lub zarejestruj bramę
### <a name="1-problem"></a>1. Problem
Widzisz ten komunikat o błędzie podczas instalowania i rejestrowanie bramy, w szczególności podczas pobierania pliku instalacyjnego hello bramy.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Przyczyna
Hello maszyny, na którym próbujesz tooinstall hello bramy nie powiodło się toodownload hello najnowszej bramy plik instalacyjny z Centrum pobierania hello powodu tooa problem z siecią.

#### <a name="resolution"></a>Rozwiązanie
Sprawdź toosee ustawienia z zapory serwera proxy serwera czy ustawienia hello blokują hello połączenia sieciowego z hello komputera toohello [Centrum pobierania](https://download.microsoft.com/)i zaktualizuj ustawienia hello odpowiednio.

Alternatywnie można pobrać plik instalacyjny hello hello najnowszą bramę z hello [Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=39717) na innych komputerach, które mogą uzyskiwać dostęp do Centrum pobierania hello. Mogą być następnie brama toohello pliku Instalatora hello kopiowania komputera-hosta i uruchomić go ręcznie bramy hello tooinstall i aktualizacji.

### <a name="2-problem"></a>2. Problem
Ten błąd jest widoczny podczas tooinstall bramy w przypadku próby klikając **Zainstaluj bezpośrednio na tym komputerze** w hello portalu Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Przyczyna
Brama jest już zainstalowana na komputerze hello.

#### <a name="resolution"></a>Rozwiązanie
Odinstaluj istniejącą bramę hello na maszynie hello, a następnie kliknij przycisk hello **Zainstaluj bezpośrednio na tym komputerze** połączyć ponownie.

### <a name="3-problem"></a>3. Problem
Ten błąd może być widoczna podczas rejestrowania nowej bramy.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Przyczyna
Można napotkać tego komunikatu dla jednego z hello z następujących powodów:

* format Hello hello klucz bramy jest nieprawidłowy.
* klucz bramy Hello została unieważniona.
* wygenerowano ponownie klucz bramy Hello hello portalu.  

#### <a name="resolution"></a>Rozwiązanie
Sprawdź, czy używasz hello klucz prawo bramy z portalu hello. W razie potrzeby ponownie wygenerować klucz i użyj hello klucza tooregister hello bramy.

### <a name="4-problem"></a>4. Problem
Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Zawartość i format klucza jest nieprawidłowy](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Przyczyna
Witaj zawartości lub format hello klucz bramy wejściowy jest nieprawidłowy. Jednego z powodów hello może być to, że tylko część klucza hello został skopiowany z portalu hello lub jest używany nieprawidłowy klucz.

#### <a name="resolution"></a>Rozwiązanie
Wygeneruj klucz bramy w portalu hello i użyj hello kopiowania przycisk toocopy hello cały klucz. Następnie wklej go w tej bramy hello tooregister okna.

### <a name="5-problem"></a>5. Problem
Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Klucz bramy jest nieprawidłowy lub pusty](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Przyczyna
wygenerowano ponownie klucz bramy Hello lub hello bramy został usunięty w hello portalu Azure. Możliwe również, czy hello konfiguracji bramy zarządzania danymi nie jest najnowszą.

#### <a name="resolution"></a>Rozwiązanie
Sprawdź hello konfiguracji bramy zarządzania danymi jest najnowsza wersja hello, możesz znaleźć najnowszej wersji hello na powitania Microsoft [Centrum pobierania](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Jeśli Instalator jest bieżący / najnowsze i brama nadal istnieje w portalu, ponownie wygenerować klucz bramy hello w hello portalu Azure, użyj hello kopiowania przycisk toocopy hello cały klucz i wklej go w tej bramy hello tooregister okna. W przeciwnym razie ponownie hello bramy i zacząć od nowa.

### <a name="6-problem"></a>6. Problem
Może pojawić się następujący komunikat o błędzie, jeśli rejestrujesz bramy hello.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Klucz bramy jest nieprawidłowy lub pusty](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Przyczyna
Ten błąd może się zdarzyć, ponieważ usunięto bramę hello lub ponownie wygenerować klucz bramy skojarzone hello.

#### <a name="resolution"></a>Rozwiązanie
Usunięcie bramy hello ponownie utworzyć bramę hello hello portalu, kliknij przycisk **zarejestrować**, skopiuj klucz hello z portalu hello, wklej go, a następnie spróbuj tooregister hello bramy.

Jeśli brama hello nadal istnieje, ale ponownego wygenerowania klucza jego, użyj hello nowego klucza tooregister hello bramy. Jeśli nie masz klucza hello, należy ponownie wygenerować klucz hello ponownie z portalu hello.

### <a name="7-problem"></a>7. Problem
W przypadku rejestrowania bramy, może być konieczne tooenter ścieżkę i hasło certyfikatu.

![Określ certyfikat](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Przyczyna
Brama Hello została zarejestrowana na innych komputerach przed. Podczas rejestracji początkowej hello bramy certyfikat szyfrowania został skojarzony z hello bramy. certyfikat Hello można własnym generowanych przez bramę hello lub podane przez użytkownika hello.  Ten certyfikat jest poświadczeń używanych tooencrypt hello magazynu danych (połączonej usługi).  

![Eksportowanie certyfikatu](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Gdy Przywracanie hello bramy na inny komputer hosta, Kreator rejestracji hello zapyta, dla tego certyfikatu toodecrypt poświadczeń wcześniej zaszyfrowanych z tym certyfikatem.  Bez tego certyfikatu nie może odszyfrować poświadczeń hello hello nowej bramy i wykonania działania kolejnych kopii skojarzone z tym nową bramę zakończy się niepowodzeniem.  

#### <a name="resolution"></a>Rozwiązanie
Jeśli certyfikat poświadczeń hello zostały wyeksportowane z oryginalnego komputera bramy hello przy użyciu hello **wyeksportować** przycisk na powitania **ustawienia** karcie w danych Menedżera konfiguracji bramy zarządzania, należy użyć hello certyfikat w tym miejscu.

Nie można pominąć ten etap, podczas przywracania bramy. Jeśli brakuje certyfikatu hello toodelete hello bramy z portalu hello i ponownie Tworzenie nowej bramy.  Ponadto należy zaktualizować wszystkie połączone usługi, które są powiązane toohello bramy przez ponownego wprowadzania poświadczeń.

### <a name="8-problem"></a>8. Problem
Może pojawić się następujący komunikat o błędzie hello.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Przyczyna
Ten błąd wystąpi, gdy brama jest w środowisku, które wymaga tooaccess serwera proxy HTTP zasobów internetowych, lub serwer proxy uwierzytelniania hasła jest zmieniany, ale nie jest odpowiednio aktualizowany w bramy.

#### <a name="resolution"></a>Rozwiązanie
Postępuj zgodnie z instrukcjami hello hello [zagadnienia dotyczące serwera Proxy](#proxy-server-considerations) sekcji tego artykułu, a następnie skonfiguruj ustawienia serwera proxy z danych Menedżera konfiguracji bramy zarządzania.

## <a name="gateway-is-online-with-limited-functionality"></a>Brama jest w trybie online z ograniczoną funkcjonalnością
### <a name="1-problem"></a>1. Problem
Możesz wyświetlić stan hello hello bramy jako online z ograniczoną funkcjonalnością.

#### <a name="cause"></a>Przyczyna
Wyświetlany stan hello hello brama jest w trybie online z ograniczoną funkcjonalność dla jednego z hello z następujących powodów:

* Brama nie może połączyć toocloud usługi za pomocą usługi Azure Service Bus.
* Usługi w chmurze nie można połączyć toogateway za pośrednictwem usługi Service Bus.

Gdy brama hello jest dostępna z ograniczoną funkcjonalnością, może być możliwe toouse hello kreatora kopiowania fabryki danych toocreate danych potoki kopiowania tooor danych z lokalnych magazynów danych. Jako rozwiązanie alternatywne można Edytor fabryki danych w portalu hello, Visual Studio lub Azure PowerShell.

#### <a name="resolution"></a>Rozwiązanie
Rozwiązanie tego problemu (online z ograniczoną funkcjonalnością) jest oparty na czy hello bramy nie można połączyć z usługą w chmurze toohello lub hello inny sposób. Witaj następujące sekcje zawierają te rozwiązania.

### <a name="2-problem"></a>2. Problem
Zostanie wyświetlony następujący błąd hello.

`Error: Gateway cannot connect toocloud service through service bus`

![Brama nie może połączyć toocloud usługi](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Przyczyna
Brama nie może połączyć toohello usługi w chmurze za pośrednictwem usługi Service Bus.

#### <a name="resolution"></a>Rozwiązanie
Wykonaj te kroki tooget hello bramy powrotem w tryb online:

1. Zezwalaj na adres IP reguły wychodzące na komputerze bramy hello i hello firmowej zapory. Można znaleźć adres IP z dziennika zdarzeń systemu Windows hello (identyfikator == 401): próba została wprowadzona tooaccess gniazda w sposób zabroniony przez jego uprawnienia dostępu XX. XX. XX. XX:9350.
* Skonfiguruj ustawienia serwera proxy na powitania bramy. Zobacz hello [zagadnienia dotyczące serwera Proxy](#proxy-server-considerations) sekcji, aby uzyskać szczegółowe informacje.
* Włącz portów wychodzących 5671 i 9350-9354 na obu hello zapory systemu Windows na komputerze bramy hello i hello firmowej zapory. Zobacz hello [portów i zapory](#ports-and-firewall) sekcji, aby uzyskać szczegółowe informacje. Ten krok jest opcjonalny, ale firma Microsoft zaleca ze względów wydajności.

### <a name="3-problem"></a>3. Problem
Zostanie wyświetlony następujący błąd hello.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Przyczyna
Błąd przejściowy w łączności sieciowej.

#### <a name="resolution"></a>Rozwiązanie
Wykonaj te kroki tooget hello bramy powrotem w tryb online:

1. Zaczekaj kilka minut, łączności hello zostaną automatycznie odzyskane po hello błąd został usunięty.
* Jeśli hello błąd będzie się powtarzać, uruchom ponownie usługę bramy hello.

## <a name="failed-tooauthor-linked-service"></a>Nie powiodło się tooauthor połączone usługi
### <a name="problem"></a>Problem
Ten błąd może być widoczna podczas spróbuj toouse Menedżera poświadczeń w hello tooinput portalu poświadczeń dla nowej usługi połączonej lub zaktualizować poświadczenia istniejącą połączoną usługę.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Gdy zostanie wyświetlony ten błąd, strony ustawień hello z danych Menedżera konfiguracji bramy zarządzania może wyglądać powitania po zrzut ekranu.

![Nie można nawiązać połączenia bazy danych](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Przyczyna
certyfikat SSL Hello mógł utracić na komputerze bramy hello. komputer z bramą Hello nie można załadować hello certyfikat obecnie używany do szyfrowania SSL. Może być również wyświetlany jest komunikat o błędzie w dzienniku zdarzeń hello, który jest podobne toohello następującą wiadomości.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Rozwiązanie
Wykonaj te kroki toosolve hello problemu:

1. Uruchom Menedżera konfiguracji bramy zarządzania danymi.
2. Przełącz toohello **ustawienia** kartę.  
3. Kliknij przycisk hello **zmiany** certyfikat SSL hello toochange przycisku.

   ![Zmień przycisk certyfikat](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Wybierz nowy certyfikat jako hello certyfikatu SSL. Możesz użyć dowolnego certyfikatu SSL, który jest generowany przez użytkownika lub każdej organizacji.

   ![Określ certyfikat](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Aktywność kopiowania nie powiedzie się.
### <a name="problem"></a>Problem
Można zauważyć powitania po awarii "UserErrorFailedToConnectToSqlserver", po skonfigurowaniu potoku w portalu hello.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Przyczyna
Może to mieć kilka przyczyn, i środki zaradcze różni odpowiednio.

#### <a name="resolution"></a>Rozwiązanie
Zezwolenie na połączenia wychodzące TCP za pośrednictwem portu TCP/1433 na powitania po stronie klienta bramy zarządzania danymi przed połączeniem tooan bazy danych SQL.

Jeśli hello docelowa baza danych jest bazą danych Azure SQL, sprawdzanie programu SQL Server ustawień zapory dla platformy Azure oraz.

Zobacz powitania po sekcji tootest hello połączenia toohello na lokalnym magazynem danych.

## <a name="data-store-connection-or-driver-related-errors"></a>Połączenia magazynu danych lub błędy związane z sterownika
Jeśli widzisz dane przechowywane połączenia lub błędy związane z sterowników, wykonaj hello następujące kroki:

1. Uruchom Menedżera konfiguracji bramy zarządzania danymi na maszynie bramy hello.
2. Przełącz toohello **diagnostyki** kartę.
3. W **Testuj połączenie**, Dodaj grupę hello bramę.
4. Kliknij przycisk **testu** toosee, jeśli można połączyć toohello lokalnego źródła danych na maszynie bramy hello przy użyciu hello informacje o połączeniu oraz poświadczenia. Jeśli połączenie testowe hello nadal kończy się niepowodzeniem po zainstalowaniu sterownika, ponowne uruchomienie hello bramy dla niego toopick się hello najnowsze zmiany.

![Testuj połączenie na karcie diagnostyki](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Dzienniki bramy
### <a name="send-gateway-logs-toomicrosoft"></a>Wyślij tooMicrosoft dzienniki bramy
Gdy skontaktować się z Microsoft Support tooget pomoc dotyczącą rozwiązywania problemów bramy, użytkownik może zostać poproszony tooshare dzienniki bramy. Hello wersji z hello bramy można udostępniać dzienniki wymagane bramy z dwóch kliknięcia przycisków w danych Menedżera konfiguracji bramy zarządzania.    

1. Przełącz toohello **diagnostyki** kartę w danych Menedżera konfiguracji bramy zarządzania.

    ![Karta zarządzania diagnostyki bramy danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Kliknij przycisk **Wyślij dzienniki** hello toosee następujące okno dialogowe.

    ![Dzienniki zarządzania bramy wysyłanie danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Opcjonalnie) Kliknij przycisk **Sprawdź dzienniki** tooreview dzienniki w Podglądzie zdarzeń hello.
4. (Opcjonalnie) Kliknij przycisk **prywatności** zasady zachowania poufności informacji usług tooreview firmy Microsoft w sieci web.
5. Po zakończeniu są o tooupload, kliknij przycisk **Wyślij dzienniki** tooactually przesyłania dzienników hello z hello ostatnich siedmiu dni tooMicrosoft do rozwiązywania problemów. Powinien zostać wyświetlony stan hello operacji wysyłania dzienników hello pokazane na powitania po zrzut ekranu.

    ![Dane zarządzania bramy wysyłania dzienników stanu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Po zakończeniu operacji hello wyświetlone okno dialogowe pokazane na powitania po zrzut ekranu.

    ![Dane zarządzania bramy wysyłania dzienników stanu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Zapisz hello **identyfikator raportu** i udostępniać je Support firmy Microsoft. Identyfikator raportu Hello jest używany toolocate hello bramy dzienniki przekazane do rozwiązywania problemów.  Identyfikator raportu Hello jest także zapisane w Podglądzie zdarzeń hello.  Można go znaleźć, sprawdzając identyfikator zdarzenia hello "25" i sprawdź hello daty i godziny.

    ![Dane zarządzania bramy wysyłania dzienników identyfikator raportu](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Dzienniki bramy archiwum na komputerze hosta bramy
Istnieją sytuacje, w którym masz problemy bramy i dzienniki bramy nie mogą współużytkować bezpośrednio:

* Ręcznie zainstaluj hello bramy i zarejestruj bramę hello.
* Możesz spróbować tooregister hello bramy za pomocą ponownie wygenerowanego klucza w danych Menedżera konfiguracji bramy zarządzania.
* Spróbuj dzienniki toosend i nie może zostać połączona usługa hosta bramy hello.

W tych sytuacjach można zapisać dzienniki bramy jako plik zip i udostępnić go w przypadku skontaktuj się z pomocą techniczną firmy Microsoft. Na przykład jeśli wystąpi błąd podczas rejestrowania bramy hello jako pokazano hello następującego zrzutu ekranu.   

![Błąd zarządzania rejestracji bramy danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Kliknij przycisk hello **archiwum dzienniki bramy** połączyć tooarchive i zapisać dzienników, a następnie udostępnić plik zip hello pomocy technicznej firmy Microsoft.

![Dzienniki zarządzania bramy archiwum danych](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Zlokalizuj dzienniki bramy
Bramy szczegółowe informacje można znaleźć w dzienniku zdarzeń systemu Windows hello.

1. Uruchom system Windows **Podgląd zdarzeń**.
2. Zlokalizuj dzienniki w hello **Dzienniki aplikacji i usług** > **brama zarządzania danymi** folderu.

 Przy rozwiązywaniu problemów związanych z bramą, wyszukaj poziom zdarzenia błędów w Podglądzie zdarzeń hello.

![Brama zarządzania danymi dzienniki w Podglądzie zdarzeń](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
