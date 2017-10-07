---
title: "aaaWork przy użyciu istniejących lokalnych serwerów proxy i Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób toowork przy użyciu istniejących lokalnych serwerów proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Praca z istniejącym lokalnych serwerów proxy

W tym artykule opisano sposób toowork łączniki serwera Proxy aplikacji usługi Azure Active Directory (Azure AD) tooconfigure z serwerów proxy ruchu wychodzącego. Przewodnik jest przeznaczony dla klientów z sieci środowiskach z istniejących serwerów proxy.

Rozpoczniemy analizując te scenariusze wdrażania głównego:
* Skonfiguruj toobypass łączniki proxy ruchu wychodzącego sieci lokalnej.
* Skonfiguruj toouse łączniki tooaccess serwera proxy ruchu wychodzącego serwera Proxy aplikacji usługi Azure AD.

Aby uzyskać więcej informacji na temat działania łączników, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Konfigurowanie serwera proxy ruchu wychodzącego hello

Jeśli masz serwera proxy ruchu wychodzącego w danym środowisku, należy użyć konta z serwera proxy ruchu wychodzącego hello tooconfigure odpowiednie uprawnienia. Ponieważ hello Instalator jest uruchamiany w kontekście hello hello użytkownika, który wykonuje hello instalacji, należy sprawdzić konfigurację hello przy użyciu Microsoft Edge lub innej przeglądarki internetowej.

tooconfigure hello ustawienia serwera proxy w programie Microsoft Edge:

1. Przejdź za**ustawienia** > **ustawienia zaawansowane widoku** > **Otwórz ustawienia serwera Proxy** > **ręcznego ustawienia serwera Proxy** .
2. Ustaw **Użyj serwera proxy** za**na**, wybierz pozycję hello **nie używaj powitania serwera proxy dla adresów lokalnych (sieć intranet)** pole wyboru, a następnie zmień hello adres i port tooreflect Serwer proxy lokalnego.
3. Wypełnij ustawienia serwera proxy niezbędne hello.

   ![Okno dialogowe ustawień serwera proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Obejście proxy ruchu wychodzącego

Łączniki mają podstawowych składników systemu operacyjnego, które żądania wychodzącego. Te składniki automatycznie próbę toolocate serwera proxy w sieci hello. Korzystają autowykrywania serwera Proxy sieci Web (WPAD), jeśli jest włączona w środowisku hello.

składniki systemu operacyjnego Hello próba toolocate serwer proxy przeprowadzając wyszukiwania DNS dla wpad.domainsuffix. Jeśli to rozwiązuje w systemie DNS, żądanie HTTP jest przeprowadzane toohello IP adres wpad.dat. To żądanie staje się hello skryptu konfiguracji serwera proxy w danym środowisku. Łącznik Hello korzysta z tego tooselect skryptu serwera proxy ruchu wychodzącego. Jednak ruch łącznika może nadal nie powiodło się, ze względu na ustawienia dodatkowe czynności konfiguracyjne na powitania serwera proxy.

Można skonfigurować toobypass łącznika hello tooensure serwera proxy sieci lokalnej, używa bezpośrednie połączenie toohello Azure usługi. Zalecamy takie podejście (Jeśli zasady sieci umożliwia on), ponieważ oznacza, że masz jeden mniej toomaintain konfiguracji.

toodisable użycia serwera proxy ruchu wychodzącego dla łącznika hello, Edytuj plik C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config hello i dodać hello *system.net* sekcji pokazano w tym przykładowym kodzie :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure hello aktualizator łącznika usługi będzie również pomija powitania serwera proxy, należy podobne zmiany toohello ApplicationProxyConnectorUpdaterService.exe.config plik znajdujący się w aktualizator łącznika serwera Proxy aplikacji usługi AAD C:\Program Files\Microsoft.

Należy się kopie toomake hello oryginalnych plików, w razie potrzeby toorevert toohello domyślnych .config plików.

## <a name="use-hello-outbound-proxy-server"></a>Użyj serwera proxy ruchu wychodzącego hello

Niektóre środowiska wymagają wszystkich toogo ruch wychodzący za pośrednictwem serwera proxy ruchu wychodzącego, bez wyjątku. W związku z tym pomijanie powitania serwera proxy nie jest opcją.

Można skonfigurować hello łącznika ruchu toogo za pośrednictwem serwera proxy ruchu wychodzącego hello, pokazane na powitania po diagramu:

 ![Konfigurowanie łącznika toogo ruchu za pośrednictwem serwera proxy ruchu wychodzącego tooAzure AD serwera Proxy aplikacji](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

W związku z tym o tylko ruchu wychodzącego, jest tooconfigure nie konieczności ruchu przychodzącego dostęp za pośrednictwem zapór.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Krok 1: Skonfiguruj łącznik hello i powiązanych usług toogo za pośrednictwem serwera proxy ruchu wychodzącego hello

Objętych wcześniej, jeśli WPAD jest włączona w środowisku hello i prawidłowo skonfigurowany, łącznik hello automatycznie wykryje na powitania serwera proxy ruchu wychodzącego toouse serwera, a następnie spróbuj go. Jednak jawnie skonfigurować toogo łącznika hello za pośrednictwem serwera proxy ruchu wychodzącego.

toodo tak, przeprowadź edycję pliku C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config hello i Dodaj hello *system.net* sekcji pokazano w tym przykładowym kodzie. Zmień *proxyserver:8080* tooreflect swoją nazwę serwera lokalnego serwera proxy lub adres IP i hello portu, że nasłuchuje na.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Skonfiguruj serwer proxy hello aktualizator łącznika usługi toouse hello dokonując podobne zmiany toohello w następującej lokalizacji C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy łącznika Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Krok 2: Konfigurowanie hello proxy tooallow ruch z hello łącznika i powiązane usługi tooflow za pośrednictwem

Istnieją cztery tooconsider aspekty na powitania serwera proxy ruchu wychodzącego:
* Reguły ruchu wychodzącego serwera proxy
* Uwierzytelnianie serwera proxy
* Porty serwera proxy
* Inspekcja protokołu SSL

#### <a name="proxy-outbound-rules"></a>Reguły ruchu wychodzącego serwera proxy
Zezwalaj na dostęp toohello następujące punkty końcowe dla dostępu do usługi łącznika:

* *. msappproxy.net
* *. servicebus.windows.net

Początkowa rejestracji Zezwalaj na następujące punkty końcowe toohello dostępu:

* login.windows.net
* Login.microsoftonline.com

Jeśli nie umożliwiają nawiązywanie połączeń przez nazwę FQDN, a zamiast tego muszą toospecify zakresy adresów IP, należy użyć tych opcji:

* Zezwalaj na dostęp ruchu wychodzącego łącznika hello tooall miejsc docelowych.
* Zezwalaj na powitania łącznik wychodzący dostęp za[zakresy IP centrum danych Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Hello żądania przy użyciu hello listą zakresów IP centrum danych Azure jest, że jest aktualizowana co tydzień. Należy tooput procesu w miejscu tooensure odpowiednio aktualizowany reguł dostępu.

#### <a name="proxy-authentication"></a>Uwierzytelnianie serwera proxy

Uwierzytelnianie serwera proxy nie jest obecnie obsługiwane. Nasze zalecenie, bieżący jest hello tooallow łącznika toohello anonimowy dostęp do Internetu miejsc docelowych.

#### <a name="proxy-ports"></a>Porty serwera proxy

Łącznik Hello sprawia, że oparte na protokole SSL połączeń wychodzących przy użyciu metody CONNECT hello. Ta metoda konfiguruje zasadniczo tunel powitania serwera proxy ruchu wychodzącego. Skonfiguruj tooallow serwera proxy hello tunelowania tooports 443 i 80.

>[!NOTE]
>Po uruchomieniu usługi Service Bus przy użyciu protokołu HTTPS używa portu 443. Domyślnie usługi Service Bus podejmuje próbę bezpośredniego połączenia TCP i powraca tooHTTPS tylko wtedy, gdy bezpośrednie połączenie między zakończy się niepowodzeniem.

tooensure hello ruch jest również przesyłany za pośrednictwem serwera proxy ruchu wychodzącego hello usługi Service Bus, upewnij się, że ten łącznik hello nie może połączyć się bezpośrednio z toohello usług Azure porty 9350, 9352 i 5671.

#### <a name="ssl-inspection"></a>Inspekcja protokołu SSL
Nie należy używać SSL kontroli w przypadku ruchu łącznika hello, ponieważ powoduje problemy w przypadku ruchu łącznika hello.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Rozwiązywanie problemów z łącznika serwera proxy problemów i problemy z połączeniem usługi
Teraz powinien być widoczny cały ruch przepływających przez powitania serwera proxy. Jeśli masz problemy powinny pomóc w hello następujące informacje dotyczące rozwiązywania problemów.

Witaj najlepsze sposób tooidentify i rozwiązywania problemów z łącznością łącznika tootake sieci przechwytywania usługi łącznika hello podczas uruchamiania usługi łącznika hello jest problemy. To stanowić nie lada wyzwanie, więc Przyjrzyjmy się szybkie porady dotyczące przechwytywania i filtrowania śladów sieciowych.

Możesz użyć hello monitorowania dowolnego narzędzia. Dla celów hello w tym artykule użyliśmy Microsoft Network Monitor 3.4. Możesz [Pobierz go z Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

filtry, których używamy w hello następujące sekcje zawierają informacje i przykłady Hello są określone tooNetwork Monitor, ale hello zasady mogą być zastosowane tooany narzędzie do analizy.

### <a name="take-a-capture-by-using-network-monitor"></a>Przechwytywanie za pomocą Monitora sieci

toostart przechwytywania:

1. Otwórz program Network Monitor i kliknij przycisk **nowe przechwycenia**.
2. Kliknij przycisk hello **Start** przycisku.

   ![Okno Monitora sieci](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Po ukończeniu przechwytywania, kliknij przycisk hello **zatrzymać** tooend przycisk go.

### <a name="take-a-capture-of-connector-traffic"></a>Przechwytywanie ruchu łącznika

Do rozwiązywania problemów początkowej, wykonaj hello następujące kroki:

1. Z services.msc należy zatrzymać usługę łącznika serwera Proxy aplikacji w usłudze Azure AD hello.
2. Uruchom hello przechwytywania ruchu sieciowego.
3. Uruchom usługę łącznika serwera Proxy aplikacji w usłudze Azure AD hello.
4. Zatrzymaj hello przechwytywania ruchu sieciowego.

   ![Usługa Azure łącznika serwera Proxy aplikacji usługi AD w celu aplikację services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Obejrzyj hello żądań z serwera proxy toohello łącznika hello

Skoro masz przechwytywania ruchu sieciowego, wszystko jest gotowe toofilter go. toolooking klucza Hello na powitania śledzenia jest zrozumienie, jak toofilter hello przechwytywania.

Jeden filtr następująco (gdzie 8080 jest port usługi serwera proxy hello):

**(protokół http. Żądanie lub http. Odpowiedź) i tcp.port==8080**

Po wprowadzeniu tego filtru w hello **filtru wyświetlania** i zaznacz **Zastosuj**, filtruje ruchu hello przechwycone oparte na powitania filtru.

Witaj poprzedniego filtru zawiera tylko hello żądań i odpowiedzi HTTP z hello port serwera proxy. Do uruchomienia łącznika, gdy łącznik hello jest toouse skonfigurowany serwer proxy filtr hello czy Pokaż podobny do następującego:

 ![Przykład listy filtrowane żądań i odpowiedzi HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Teraz w szczególności szukasz hello CONNECT żądań, które Pokaż komunikacji z serwerem proxy hello. Na sukces otrzymasz odpowiedź HTTP OK (200).

Jeśli widzisz innych kodów odpowiedzi, na przykład 407 lub 502 powitania serwera proxy jest wymaganie uwierzytelniania lub nie zezwala na ruch hello innego powodu. W tym momencie Uwzględnij się z zespołem pomocy technicznej serwera proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Zidentyfikuj nieudanych prób połączenia TCP

Hello innych typowy scenariusz, który może Cię zainteresować jest hello łącznika próbuje tooconnect bezpośrednio, ale występuje błąd.

Inny filtr Monitor sieci, która pomaga tooeasily zidentyfikować ten problem jest:

**Właściwość. TCPSynRetransmit**

Pakiet SYN jest pierwszy pakiet hello wysłanych tooestablish połączenie TCP. Jeśli ten pakiet nie zwraca odpowiedź, hello SYN jest podjęta ponownie. Można użyć dowolnego syn ponownie przesłane hello poprzedzających toosee filtru. Następnie można sprawdzić, czy te syn odpowiada tooany ruch związany z usługą łącznika.

Witaj poniższy przykład przedstawia próba połączenia nie powiodło się tooService magistrali port 9352:

 ![Przykład odpowiedzi próby połączenia nie powiodło się](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Jeśli zostanie wyświetlony ekran podobny do hello poprzedzających odpowiedzi łącznika hello próbuje toocommunicate bezpośrednio z hello usługi Azure Service Bus. Jeśli oczekujesz hello łącznika toomake bezpośrednich połączeń toohello Azure usługi, to odpowiedź jest jednoznacznie zidentyfikować, że masz problem sieci i zapory.

>[!NOTE]
>Jeśli jesteś toouse skonfigurowany serwer proxy tej odpowiedzi może oznaczać, że usługi Service Bus próbuje bezpośrednie połączenie TCP przed przełączeniem tooattempting połączenie za pośrednictwem protokołu HTTPS.
>

Analiza śledzenia sieci nie jest dostępne dla wszystkich użytkowników. Jednak jest przydatnym narzędziem tooget szybkie informacje o to, co dzieje się z sieci.

Jeśli będziesz kontynuować toostruggle z problemów z łącznością łącznika, Utwórz bilet z naszym zespołem pomocy technicznej. zespół Hello mogą pomóc o dodatkowe informacje o rozwiązywaniu.

Aby uzyskać informacje o rozwiązywaniu problemów z łącznika serwera Proxy aplikacji, zobacz [Rozwiązywanie problemów z serwera Proxy aplikacji](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Następne kroki

[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)<br>
[Jak toosilently zainstalować hello łącznika serwera Proxy aplikacji w usłudze Azure AD](active-directory-application-proxy-silent-installation.md)
