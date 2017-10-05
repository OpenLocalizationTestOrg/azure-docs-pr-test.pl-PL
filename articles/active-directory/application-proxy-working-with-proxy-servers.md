---
title: "Praca z istniejącym lokalnych serwerów proxy i Azure AD | Dokumentacja firmy Microsoft"
description: "Uwzględniono również sposób pracy z istniejących serwerów proxy lokalnymi."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Praca z istniejącym lokalnych serwerów proxy

W tym artykule opisano sposób konfigurowania serwera Proxy aplikacji usługi Azure Active Directory (Azure AD) łączniki do pracy z serwerami serwera proxy ruchu wychodzącego. Przewodnik jest przeznaczony dla klientów z sieci środowiskach z istniejących serwerów proxy.

Rozpoczniemy analizując te scenariusze wdrażania głównego:
* Skonfiguruj konektory w celu obejścia proxy ruchu wychodzącego sieci lokalnej.
* Skonfiguruj konektory w celu użycia serwera proxy ruchu wychodzącego do serwera Proxy aplikacji usługi Azure AD.

Aby uzyskać więcej informacji na temat działania łączników, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).

## <a name="configure-the-outbound-proxy"></a>Konfigurowanie serwera proxy ruchu wychodzącego

Jeśli w środowisku serwera proxy ruchu wychodzącego, użyj konta z odpowiednimi uprawnieniami do konfigurowania serwera proxy ruchu wychodzącego. Ponieważ Instalator jest uruchamiany w kontekście użytkownika, który jest podczas instalacji, konfiguracji można sprawdzić za pomocą Microsoft Edge lub innej przeglądarki internetowej.

Aby skonfigurować ustawienia serwera proxy w programie Microsoft Edge:

1. Przejdź do **ustawienia** > **widoku Zaawansowane ustawienia** > **Otwórz ustawienia serwera Proxy** > **instalacji ręcznej serwera Proxy**.
2. Ustaw **Użyj serwera proxy** do **na**, wybierz pozycję **nie używaj serwera proxy dla adresów lokalnych (sieć intranet)** pole wyboru, a następnie zmień adres i port, aby odzwierciedlić serwera proxy w lokalnych.
3. Wypełnij ustawienia serwera proxy niezbędne.

   ![Okno dialogowe ustawień serwera proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Obejście proxy ruchu wychodzącego

Łączniki mają podstawowych składników systemu operacyjnego, które żądania wychodzącego. Te składniki automatycznie podejmować próby zlokalizowania serwera proxy w sieci. Korzystają autowykrywania serwera Proxy sieci Web (WPAD), jeśli jest włączona w środowisku.

Składniki systemu operacyjnego podejmować próby zlokalizowania serwera proxy przeprowadzając wyszukiwania DNS dla wpad.domainsuffix. Jeśli to rozwiązuje w systemie DNS do adresu IP dla wpad.dat następnie jest przeprowadzane żądania HTTP. To żądanie staje się skrypt konfiguracji serwera proxy w danym środowisku. Łącznik korzysta ten skrypt, aby wybrać serwer proxy ruchu wychodzącego. Jednak ruch łącznika może nadal nie powiodło się, ze względu na dodatkowe ustawienia konfiguracji potrzebne na serwerze proxy.

Można skonfigurować łącznik, aby pominąć lokalnego serwera proxy do zapewnienia korzysta z bezpośredniego łączności usług Azure. Zalecamy takie podejście (Jeśli zasady sieci umożliwia on), ponieważ oznacza, że masz mniej jedną konfigurację do obsługi.

Aby wyłączyć użycia serwera proxy ruchu wychodzącego dla łącznika, przeprowadź edycję pliku C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config i Dodaj *system.net* sekcji pokazano w tym przykładowym kodzie:

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
Aby upewnić się, że aktualizator łącznika usługi również pomija serwera proxy, należy wprowadzić zmianę podobne do pliku ApplicationProxyConnectorUpdaterService.exe.config znajdującym się w aktualizator łącznika serwera Proxy aplikacji usługi AAD C:\Program Files\Microsoft.

Należy pamiętać o wykonaniu kopii oryginalnych plików, w razie potrzeby można przywrócić w plikach .config domyślne.

## <a name="use-the-outbound-proxy-server"></a>Użyj serwera proxy ruchu wychodzącego

Niektóre środowiska wymagają cały ruch wychodzący do go za pośrednictwem serwera proxy ruchu wychodzącego, bez wyjątku. W związku z tym pomijanie serwera proxy nie jest opcją.

Możesz skonfigurować ruchu łącznika do go za pośrednictwem serwera proxy ruchu wychodzącego, jak pokazano na poniższym diagramie:

 ![Konfigurowanie łącznika ruchu można przejść za pośrednictwem serwera proxy ruchu wychodzącego do serwera Proxy aplikacji usługi Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

W wyniku o tylko ruchu wychodzącego, nie istnieje potrzeba aby skonfigurować dostęp przychodzących na zaporach.

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a>Krok 1: Konfigurowanie łącznika i powiązane usługi, aby przejść za pośrednictwem serwera proxy ruchu wychodzącego

Objętych wcześniej, jeśli WPAD jest włączona w środowisku i prawidłowo skonfigurowany, łącznik automatycznie odnajdzie serwera proxy ruchu wychodzącego i spróbować go użyć. Można jednak jawnie skonfigurować łącznik, aby go za pośrednictwem serwera proxy ruchu wychodzącego.

Aby to zrobić, Edytuj plik C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config i Dodaj *system.net* sekcji pokazano w tym przykładowym kodzie. Zmień *proxyserver:8080* w celu uwzględnienia nazwę lokalnego serwera proxy serwera lub adres IP i portu nasłuchiwania na.

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

Skonfiguruj usługę aktualizator łącznika, aby serwer proxy jest używany przez wprowadzenie zmiany podobną do następującej lokalizacji C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy łącznika Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a>Krok 2: Konfigurowanie serwera proxy zezwalająca na ruch z łącznika i powiązane usługi przepływają przez

Istnieją cztery aspektów, które należy wziąć pod uwagę w przypadku serwera proxy ruchu wychodzącego:
* Reguły ruchu wychodzącego serwera proxy
* Uwierzytelnianie serwera proxy
* Porty serwera proxy
* Inspekcja protokołu SSL

#### <a name="proxy-outbound-rules"></a>Reguły ruchu wychodzącego serwera proxy
Zezwalaj na dostęp do następujących punktów końcowych do łącznika usługi:

* *. msappproxy.net
* *. servicebus.windows.net

Początkowe rejestracyjny można zezwolić na dostęp do następujących punktów końcowych:

* login.windows.net
* Login.microsoftonline.com

Jeśli nie umożliwiają nawiązywanie połączeń przez nazwę FQDN, a zamiast tego określ zakresy adresów IP, korzystać z tych opcji:

* Zezwalaj na dostęp ruchu wychodzącego łącznika do wszystkich miejsc docelowych.
* Zezwalaj na dostęp ruchu wychodzącego łącznika do [zakresy IP centrum danych Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Wyzwanie z listy zakresów IP centrum danych Azure jest, że jest aktualizowana co tydzień. Należy umieścić procesu w celu zapewnienia odpowiednio aktualizowany reguł dostępu.

#### <a name="proxy-authentication"></a>Uwierzytelnianie serwera proxy

Uwierzytelnianie serwera proxy nie jest obecnie obsługiwane. Nasze zalecenie, bieżący jest zezwala na dostęp anonimowy łącznika do Internetu miejsc docelowych.

#### <a name="proxy-ports"></a>Porty serwera proxy

Łącznik sprawia, że oparte na protokole SSL połączeń wychodzących przy użyciu metody CONNECT. Ta metoda powoduje ustawienie zasadniczo tunelu za pośrednictwem serwera proxy ruchu wychodzącego. Konfiguracja serwera proxy, aby umożliwić tunelowania na porty 443 i 80.

>[!NOTE]
>Po uruchomieniu usługi Service Bus przy użyciu protokołu HTTPS używa portu 443. Domyślnie usługi Service Bus podejmuje próbę bezpośredniego połączenia TCP i powraca do HTTPS tylko wtedy, gdy bezpośrednie połączenie między zakończy się niepowodzeniem.

Aby upewnić się, że ruch usługi Service Bus jest również przesyłany za pośrednictwem serwera proxy ruchu wychodzącego, upewnij się, że łącznik nie może nawiązać bezpośrednie usług platformy Azure dla porty 9350, 9352 i 5671.

#### <a name="ssl-inspection"></a>Inspekcja protokołu SSL
Nie należy używać protokołu SSL inspekcji dla ruchu łącznika, ponieważ powoduje problemy w przypadku ruchu łącznika.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Rozwiązywanie problemów z łącznika serwera proxy problemów i problemy z połączeniem usługi
Teraz powinien być widoczny cały ruch przepływających przez serwer proxy. Jeśli masz problemy powinny pomóc następujące informacje dotyczące rozwiązywania problemów.

Najlepszym sposobem na identyfikowanie i rozwiązywanie problemów z łącznością łącznika jest przechwytywanie sieci na usługę łącznika podczas uruchamiania usługi łącznika. To stanowić nie lada wyzwanie, więc Przyjrzyjmy się szybkie porady dotyczące przechwytywania i filtrowania śladów sieciowych.

Można użyć narzędzia monitorowania wybranych przez użytkownika. Do celów tego artykułu użyliśmy Microsoft Network Monitor 3.4. Możesz [Pobierz go z Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

Przykłady i filtry, których używamy w poniższych sekcjach są specyficzne dla monitora sieci, ale zasady mogą być stosowane do dowolnego narzędzia do analizy.

### <a name="take-a-capture-by-using-network-monitor"></a>Przechwytywanie za pomocą Monitora sieci

Aby uruchomić przechwytywania:

1. Otwórz program Network Monitor i kliknij przycisk **nowe przechwycenia**.
2. Kliknij przycisk **Start** przycisku.

   ![Okno Monitora sieci](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Po ukończeniu przechwytywania, kliknij przycisk **zatrzymać** przycisk, aby ją zakończyć.

### <a name="take-a-capture-of-connector-traffic"></a>Przechwytywanie ruchu łącznika

Do rozwiązywania problemów początkowej, wykonaj następujące czynności:

1. Z services.msc należy zatrzymać usługę łącznika serwera Proxy aplikacji w usłudze Azure AD.
2. Uruchom przechwytywania ruchu sieciowego.
3. Uruchom usługę łącznika serwera Proxy aplikacji w usłudze Azure AD.
4. Zatrzymaj przechwytywania ruchu sieciowego.

   ![Usługa Azure łącznika serwera Proxy aplikacji usługi AD w celu aplikację services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a>Przyjrzyj się z serwerem proxy żądania z łącznika

Skoro masz przechwytywania ruchu sieciowego, możesz go filtrować. Klucz do analizowania śledzenia jest zrozumienie sposobu filtru przechwytywania.

Jeden filtr następująco (gdzie 8080 jest port usługi serwera proxy):

**(protokół http. Żądanie lub http. Odpowiedź) i tcp.port==8080**

Po wprowadzeniu tego filtru w **filtru wyświetlania** i zaznacz **Zastosuj**, filtruje przechwycony ruch na podstawie filtru.

Poprzednie filtru zawiera po prostu żądań i odpowiedzi HTTP z port serwera proxy. Do uruchomienia łącznika, gdy łącznik jest skonfigurowany do używania serwera proxy filtr będzie Pokaż mniej więcej tak:

 ![Przykład listy filtrowane żądań i odpowiedzi HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Teraz w szczególności szukasz żądania połączenia, które Pokaż komunikacji z serwerem proxy. Na sukces otrzymasz odpowiedź HTTP OK (200).

Jeśli widzisz innych kodów odpowiedzi, na przykład 407 lub 502, serwer proxy jest wymaganie uwierzytelniania lub nie zezwala na ruch innego powodu. W tym momencie Uwzględnij się z zespołem pomocy technicznej serwera proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Zidentyfikuj nieudanych prób połączenia TCP

Typowy scenariusz, który może Cię zainteresować jest łącznik próbuje nawiązać połączenie bezpośrednio, ale występuje błąd.

Inny filtr Monitor sieci, która pomaga łatwo zidentyfikować ten problem jest:

**Właściwość. TCPSynRetransmit**

Pakiet SYN jest pierwszy pakiet wysyłany do nawiązywania połączeń TCP. Jeśli ten pakiet nie zwraca odpowiedź, SYN jest podjęta ponownie. Można użyć poprzedniego filtru, aby wyświetlić wszystkie syn ponownie przesłane. Następnie można sprawdzić, czy te syn odpowiadają żadnych ruch związany z usługą łącznika.

W poniższym przykładzie przedstawiono portu usługi Service Bus 9352 próba połączenia nie powiodło się:

 ![Przykład odpowiedzi próby połączenia nie powiodło się](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Jeśli zostanie wyświetlony ekran podobny do poprzedniej odpowiedzi łącznika próbuje komunikują się bezpośrednio z usługi Azure Service Bus. Jeśli łącznik, aby nawiązywać połączenia bezpośrednio z usług Azure, ta odpowiedź jest jednoznacznie zidentyfikować, że masz problem sieci i zapory.

>[!NOTE]
>Jeśli są skonfigurowane do korzystania z serwera proxy, tej odpowiedzi może oznaczać, że usługi Service Bus próbuje bezpośrednie połączenie TCP przed przełączeniem do próba połączenia za pośrednictwem protokołu HTTPS.
>

Analiza śledzenia sieci nie jest dostępne dla wszystkich użytkowników. Jednak jest przydatnym narzędziem, aby uzyskać szybki dowiedzieć się, co dzieje się z sieci.

Jeśli nadal mieć trudności z problemów z łącznością łącznika, Utwórz bilet z naszym zespołem pomocy technicznej. Zespół może pomóc dalszego rozwiązywania problemów.

Aby uzyskać informacje o rozwiązywaniu problemów z łącznika serwera Proxy aplikacji, zobacz [Rozwiązywanie problemów z serwera Proxy aplikacji](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Następne kroki

[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)<br>
[Jak zainstalować łącznik serwera Proxy aplikacji Azure AD w trybie dyskretnym](active-directory-application-proxy-silent-installation.md)
