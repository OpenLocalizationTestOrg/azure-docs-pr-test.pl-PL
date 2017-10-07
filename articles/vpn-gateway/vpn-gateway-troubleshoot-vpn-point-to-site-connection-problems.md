---
title: "problemy z połączeniem aaaTroubleshoot Azure punkt lokacja | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot problemów połączenie punkt lokacja."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Rozwiązywanie problemów: Problemów Azure połączenie punkt lokacja

W tym artykule wymieniono typowe problemy połączenie punkt lokacja, które mogą wystąpić. Omówiono w nim również możliwe przyczyny i potencjalne rozwiązania tych problemów.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Błąd klienta sieci VPN: nie można odnaleźć certyfikatu

### <a name="symptom"></a>Objaw

Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:

**Nie można odnaleźć certyfikatu, który może zostać użyty z protokołem uwierzytelniania rozszerzonego. (Błąd 798)**

### <a name="cause"></a>Przyczyna

Ten problem występuje, jeśli brakuje certyfikat klienta na powitania **Certyfikaty — bieżący User\Personal\Certificates**.

### <a name="solution"></a>Rozwiązanie

Upewnij się, że ten certyfikat klienta hello jest zainstalowane na powitania po lokalizację magazynu certyfikatów hello (Certmgr.msc):
 
**Certyfikaty — bieżący User\Personal\Certificates**

Aby uzyskać więcej informacji o sposobie tooinstall hello certyfikatu klienta, zobacz [Generowanie i eksportowania certyfikatów połączeń punkt lokacja](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Po zaimportowaniu certyfikatu klienta hello nie zaznaczaj hello **Włącz silną ochronę klucza prywatnego** opcji.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Błąd klienta sieci VPN: Odebrano wiadomość hello jest nieoczekiwany lub nieprawidłowo sformatowany

### <a name="symptom"></a>Objaw

Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:

**Odebrano wiadomość Hello jest nieoczekiwany lub nieprawidłowo sformatowany. (Błąd 0x80090326)**

### <a name="cause"></a>Przyczyna

Ten problem występuje, gdy klucz publiczny certyfikatu głównego hello nie zostało załadowane do hello bramy sieci VPN platformy Azure. Może również wystąpić, jeśli klucz hello jest uszkodzony lub wygasł.

### <a name="solution"></a>Rozwiązanie

tooresolve ten problem, sprawdź status hello hello głównego certyfikatu w hello toosee portalu Azure, czy został on odwołany. Jeśli nie został odwołany, spróbuj certyfikatu głównego hello toodelete i reupload. Aby uzyskać więcej informacji, zobacz [tworzenia certyfikatów](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Błąd klienta sieci VPN: łańcuch certyfikatów przetworzona, ale została przerwana 

### <a name="symptom"></a>Objaw 

Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:

**Łańcuch certyfikatów przetworzona, ale została przerwana w certyfikacie głównym, który nie jest zaufany przez dostawcę zaufania hello.**

### <a name="solution"></a>Rozwiązanie

1. Upewnij się, że hello następujące certyfikaty są w poprawnej lokalizacji hello:

    | Certyfikat | Lokalizacja |
    | ------------- | ------------- |
    | AzureClient.pfx  | Bieżący User\Personal\Certificates |
    | Azuregateway -*GUID*. cloudapp.net  | Bieżący User\Trusted główne urzędy certyfikacji|
    | AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer    | Lokalny komputer lokalny\Zaufane główne urzędy certyfikacji|

2. Jeśli certyfikaty hello znajdują się już w lokalizacji hello, spróbuj toodelete hello certyfikatów, a następnie zainstaluj je ponownie. Witaj  **azuregateway -*GUID*. cloudapp.net** certyfikat znajduje się w pakietu konfiguracji klienta VPN hello, który został pobrany z portalu Azure hello. Można użyć pliku archivers tooextract hello pliki z pakietu hello.

## <a name="file-download-error-target-uri-is-not-specified"></a>Błąd pobierania pliku: nie określono docelowego identyfikatora URI

### <a name="symptom"></a>Objaw

Pojawi się następujący komunikat o błędzie hello:

**Wystąpił błąd podczas pobierania pliku. Nie określono docelowego identyfikatora URI.**

### <a name="cause"></a>Przyczyna 

Ten problem występuje z powodu typu niepoprawne bramy. 

### <a name="solution"></a>Rozwiązanie

Witaj typu bramy sieci VPN musi być **VPN**, i hello typ sieci VPN musi być **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Błąd klienta sieci VPN: sieci VPN platformy Azure niestandardowego skryptu nie powiodło się 

### <a name="symptom"></a>Objaw

Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:

**Skryptu niestandardowego (tooupdate Twojego routingu tabeli) nie powiodło się. (Błąd 8007026f)**

### <a name="cause"></a>Przyczyna

Ten problem może wystąpić, jeśli próbujesz połączenia sieci VPN punktu lokacji hello tooopen przy użyciu skrótu.

### <a name="solution"></a>Rozwiązanie 

Otwórz hello pakietu sieci VPN bezpośrednio, zamiast z hello skrótów.

## <a name="cannot-install-hello-vpn-client"></a>Nie można zainstalować powitania klienta sieci VPN

### <a name="cause"></a>Przyczyna 

Dodatkowy certyfikat jest brama sieci VPN hello tootrust wymagane dla sieci wirtualnej. certyfikat Hello jest uwzględniany w pakietu konfiguracji klienta VPN hello, które są generowane na podstawie hello portalu Azure.

### <a name="solution"></a>Rozwiązanie

Wyodrębnienie pakietu konfiguracji klienta VPN hello i Znajdź plik cer hello. Witaj tooinstall certyfikatów, wykonaj następujące kroki:

1. Otwórz mmc.exe.
2. Dodaj hello **certyfikaty** przystawki.
3. Wybierz hello **komputera** konta na komputerze lokalnym hello.
4. Kliknij prawym przyciskiem myszy hello **zaufane główne urzędy certyfikacji** węzła. Kliknij przycisk **wszystkie zadania** > **importu**, a plik .cer toohello przeglądania wyodrębniony z pakietu konfiguracji klienta VPN hello.
5. Uruchom ponownie komputer hello. 
6. Spróbuj tooinstall hello obsługi klienta VPN.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Błąd portalu Azure: nie powiodło się bramy sieci VPN hello toosave i hello dane są nieprawidłowe

### <a name="symptom"></a>Objaw

Podczas próby zmiany hello toosave dla bramy sieci VPN hello w portalu Azure hello pojawi się następujący komunikat o błędzie hello:

**Brama sieci wirtualnej nie powiodło się toosave &lt;* nazwa bramy*&gt;. Dane certyfikatu &lt; *certyfikatu identyfikator* &gt; jest invalid.* *

### <a name="cause"></a>Przyczyna 

Ten problem może wystąpić, jeśli hello główny klucz publiczny certyfikatu, który został przekazany zawiera nieprawidłowy znak, takich jak miejsce.

### <a name="solution"></a>Rozwiązanie

Upewnij się, że hello dane w certyfikacie hello nie zawiera nieprawidłowe znaki, takie jak podziały wiersza (znaki powrotu karetki). Witaj całą wartość powinna być jeden długi wiersz. powitania po tekst jest przykładem hello certyfikatu:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Błąd portalu Azure: nie powiodło się bramy sieci VPN hello toosave i hello Nazwa zasobu jest nieprawidłowy

### <a name="symptom"></a>Objaw

Podczas próby zmiany hello toosave dla bramy sieci VPN hello w portalu Azure hello pojawi się następujący komunikat o błędzie hello: 

**Brama sieci wirtualnej nie powiodło się toosave &lt;* nazwa bramy*&gt;. Nazwa zasobu &lt; *nazwę certyfikatu, spróbuj tooupload* &gt; jest nieprawidłowa **.

### <a name="cause"></a>Przyczyna

Ten problem występuje, ponieważ nazwa hello hello certyfikatu zawiera nieprawidłowy znak, takich jak miejsce. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Błąd portalu Azure: 503 błąd pobierania pliku pakietu sieci VPN

### <a name="symptom"></a>Objaw

Podczas próby pakietu klienta VPN toodownload hello w konfiguracji pojawi się następujący komunikat o błędzie hello:

**Toodownload hello pliku nie powiodło się. Szczegóły błędu: błąd 503. Witaj serwer jest zajęty.**
 
### <a name="solution"></a>Rozwiązanie

Przyczyną tego błędu może być tymczasowy problem z siecią. Spróbuj pakietu VPN hello toodownload ponownie za kilka minut.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Uaktualnianie programu Azure bramy sieci VPN: tooconnect są P2S wszystkich klientów

### <a name="cause"></a>Przyczyna

Jeśli certyfikat hello jest więcej niż 50% przez jego okres istnienia certyfikatu hello jest przerzuceniem.

### <a name="solution"></a>Rozwiązanie

tooresolve ten problem, Utwórz i ponowne rozdzielanie nowych klientów sieci VPN toohello certyfikatów. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Zbyt wielu klientów sieci VPN na raz podłączone

Dla każdej bramy sieci VPN hello maksymalną liczbę dozwolonych połączeń to 128. Całkowita liczba podłączonych klientów w portalu Azure hello hello jest widoczny.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Sieć VPN punkt lokacja niepoprawnie dodaje trasę dla tabeli tras toohello 10.0.0.0/8

### <a name="symptom"></a>Objaw

Podczas wybierania hello połączenia sieci VPN na powitania klienta punkt lokacja powitania klienta sieci VPN należy dodać trasę kierunku hello sieci wirtualnej platformy Azure. Usługa Pomocnika IP Hello należy dodać trasę dla podsieci hello hello klientów sieci VPN. 

Hello zakresu klienta sieci VPN należy tooa mniejsze podsieci 10.0.0.0/8, takich jak 10.0.12.0/24. Zamiast trasę 10.0.12.0/24 trasę dla 10.0.0.0/8 dodaniu, która ma wyższy priorytet. 

Ta trasa niepoprawne dzieli łączności z pozostałych lokalnej sieci, które mogą należeć do podsieci tooanother w zakresie 10.0.0.0/8 hello, takich jak 10.50.0.0/24, które nie mają określoną trasę zdefiniowane. 

### <a name="cause"></a>Przyczyna

To zachowanie jest celowe w przypadku klientów z systemem Windows. Gdy klient hello używa protokołu PPP IPCP hello, uzyskuje hello adres IP dla interfejsu tunelu hello z powitania serwera (hello bramy sieci VPN w tym przypadku). Jednak ze względu na ograniczenia w protokole hello powitania klienta nie ma hello maski podsieci. Ponieważ nie istnieje żadne tooget sposób, powitania klienta próbuje maski podsieci hello tooguess oparte na powitania klasy adres IP interfejsu tunelu hello. 

W związku z tym trasę dodaje oparte na powitania po mapowania statyczne 

Jeśli adres należy tooclass A--> Zastosuj /8

Jeśli adres należy tooclass--> B Zastosuj/16 do /

Jeśli adres należy tooclass C--> Zastosuj prefiksie/24

## <a name="vpn-client-cannot-access-network-file-shares"></a>Klient sieci VPN nie może uzyskać dostępu udziałów plików sieciowych

### <a name="symptom"></a>Objaw

Klient sieci VPN Hello został podłączony toohello sieci wirtualnej platformy Azure. Jednak powitania klienta nie może uzyskać dostępu do udziałów sieciowych.

### <a name="cause"></a>Przyczyna

Witaj protokołu SMB służy do dostępu do udziału plików. Po zainicjowaniu połączenia hello poświadczenia sesji hello dodaje powitania klienta sieci VPN i hello awarii. Po nawiązaniu połączenia hello powitania klienta jest wymuszone toouse hello pamięci podręcznej poświadczeń dla uwierzytelniania Kerberos. Ten proces jest inicjowany zapytania toohello Centrum dystrybucji kluczy (kontroler domeny) tooget tokenu. Ponieważ hello klient nawiąże połączenie z hello Internet, może nie być kontrolera domeny hello tooreach stanie. W związku z tym powitania klienta nie może przełączyć się z tooNTLM protokołu Kerberos. 

Hello tylko czasu klienta hello jest monitowany o poświadczenia jest, gdy ma prawidłowy certyfikat (z siecią SAN = nazwy UPN) wydanego przez toowhich domeny hello jest on dołączony. również powitania klienta musi być fizycznie podłączone toohello sieci z domeną. W takim przypadku hello klient próbuje toouse hello certyfikatów i przez nią miejsce osiągnie limit toohello kontrolera domeny. Następnie hello Centrum dystrybucji kluczy zwraca błąd "KDC_ERR_C_PRINCIPAL_UNKNOWN". powitania klienta jest wymuszone toofail tooNTLM. 

### <a name="solution"></a>Rozwiązanie

toowork wokół hello problem, wyłącz hello buforowanie poświadczeń domeny z powitania po podklucz rejestru: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Nie można odnaleźć połączenia VPN punkt lokacja hello w systemie Windows przed ponowną instalację powitania klienta sieci VPN

### <a name="symptom"></a>Objaw

Usuń połączenie VPN punkt lokacja hello i ponownie zainstalować powitania klienta sieci VPN. W takiej sytuacji nie skonfigurowano pomyślnie hello połączenia sieci VPN. Nie ma połączenie VPN hello hello **połączenia sieciowe** ustawienia systemu Windows.

### <a name="solution"></a>Rozwiązanie

tooresolve hello problem, Usuń hello starego VPN plików konfiguracji klienta z **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, a następnie ponownie uruchom Instalatora klienta VPN hello.
