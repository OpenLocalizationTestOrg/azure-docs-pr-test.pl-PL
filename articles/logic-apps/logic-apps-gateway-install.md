---
title: "Brama danych lokalnych aaaInstall — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Aby uzyskać dostęp do źródła danych na lokalnym, instalowanie bramy danych lokalnych hello transferu danych szybki i szyfrowania między źródłami danych lokalnie i logic apps"
keywords: "dostęp do danych lokalnych, transfer danych, szyfrowania, źródła danych"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Instalowanie bramy danych lokalne powitania dla usługi Azure Logic Apps

Aplikacje logiki uzyskania dostępu do źródeł danych lokalnie, należy zainstalować i skonfigurować bramę danych lokalne powitania. Witaj bramy działa jako mostka zapewnia transfer danych szybki i szyfrowania między systemami lokalnymi i aplikacje logiki. Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus. Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta. Dowiedz się więcej o [działanie bramy danych hello](#gateway-cloud-service).

Brama Hello obsługuje źródeł danych toothese połączeń lokalnie:

*   BizTalk Server 2016
*   DB2  
*   System plików
*   Informix
*   MQ
*   MySQL
*   Baza danych Oracle
*   PostgreSQL
*   Serwer aplikacji SAP 
*   Serwer komunikatów SAP
*   Sharepoint
*   Oprogramowanie SQL Server
*   Teradata

Te kroki pokazują, jak toofirst hello instalacji lokalnej bramy danych przed [skonfigurować połączenie między bramą hello i aplikacje logiki](./logic-apps-gateway-connection.md). Aby uzyskać więcej informacji o obsługiwanych łączników, zobacz [łączniki dla usługi Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list). 

Informacje o sposobie toouse hello bramy z innymi usługami zobacz następujące artykuły:

*   [Microsoft Power BI lokalnej bramy danych](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure bramy danych lokalnych usług Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Brama danych lokalnych Flow firmy Microsoft](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Brama danych lokalnych PowerApps firmy Microsoft](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Wymagania

**Co najmniej**:

* .NET 4.5 framework
* 64-bitowej wersji systemu Windows 7 lub Windows Server 2008 R2 (lub nowszy)

**Zalecane**:

* 8 rdzeni procesora CPU
* 8 GB pamięci
* 64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)

**Ważne uwagi dotyczące**:

* Instalowanie bramy danych lokalne powitania tylko na komputerze lokalnym.
Witaj bramy nie można zainstalować na kontrolerze domeny.

   > [!TIP]
   > Nie masz tooinstall hello bramy na powitania tego samego komputera jako źródła danych. Opóźnienie toominimize, możesz zainstalować bramę hello jak jako źródło danych możliwe tooyour lub na powitania sam komputera, przy założeniu, że użytkownik ma uprawnienia.

* Nie należy instalować na komputerze, który zostanie wyłączony, toosleep czy też nie połączyć toohello Internet, ponieważ hello bramy nie można uruchomić w tych warunkach hello bramy. Ponadto w sieci bezprzewodowej może pogorszyć wydajność bramy.

* Podczas instalacji, należy się zalogować przy użyciu [konto służbowe](https://docs.microsoft.com/azure/active-directory/sign-up-organization) zarządzanym przez usługę Azure Active Directory (Azure AD), nie konta Microsoft. 

  Masz toouse hello służbowe lub szkolne, konto później w hello Azure portal podczas tworzenia i skojarzyć z instalacją bramy zasobów bramy. Podczas tworzenia połączenia hello między logiki aplikacji i hello lokalnego źródła danych, następnie wybierz tego zasobu bramy. [Dlaczego należy używać Praca usługi Azure AD lub konta służbowego?](#why-azure-work-school-account)

  > [!TIP]
  > Jeśli konta dla oferty usługi Office 365, a nie dostarczył rzeczywiste służbowego adresu e-mail, adresu logowania może wyglądać jeff@contoso.onmicrosoft.com. 

* Jeśli masz istniejącą bramę skonfigurowanego z Instalatorem, która jest starsza niż wersja 14.16.6317.4, nie można zmienić lokalizacji bramy sieci przez uruchomione hello najnowszą wersję Instalatora. Jednak można użyć hello najnowsze Instalator tooset się nową bramę z lokalizacją hello, który chcesz zamiast tego.
  
  Jeśli Instalator bramy, która jest starsza niż wersja 14.16.6317.4, ale nie zostały zainstalowane bramy można jeszcze miejsca, pobranie i użycie hello najnowszą wersję Instalatora.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Instalowanie bramy danych hello

1.  [Pobierz i uruchom Instalatora bramy hello na komputerze lokalnym](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Przeczytaj i zaakceptuj postanowienia hello instrukcji użycia i ochrony prywatności.

3. Określ ścieżkę hello na komputerze lokalnym, w którym ma tooinstall hello bramy.

4. Po wyświetleniu monitu zaloguj się przy użyciu konta służbowego, nie konta Microsoft Azure pracy.

   ![Zaloguj się przy użyciu pracy Azure lub konta służbowego](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Zarejestruj teraz zainstalowana brama hello [usługi bramy w chmurze](#gateway-cloud-service). Wybierz **zarejestrować nową bramę na tym komputerze**.

   usługi w chmurze bramy Hello są szyfrowane i przechowywane poświadczenia źródła danych, a szczegóły bramy. 
   Usługa Hello również kieruje zapytań i ich wyników między aplikację logiki, brama danych lokalne powitania i źródła danych lokalnie.

6. Podaj nazwę dla tej instalacji bramy. Twórz klucza odzyskiwania, a następnie potwierdź klucz odzyskiwania. 

   > [!IMPORTANT] 
   > Klucz odzyskiwania musi zawierać co najmniej osiem znaków. Upewnij się, zapisywanie i hello klucz należy przechowywać w bezpiecznym miejscu. Należy również ten klucz należy toomigrate, przywracania, lub Przejmij istniejącą bramę.

   1. Wybierz toochange hello domyślnego regionu hello usługi bramy w chmurze i używanych w danej instalacji bramy usługi Azure Service Bus **Region zmiany**.

      ![Zmiana regionu](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      Witaj domyślnego regionu jest hello regionu skojarzonego z dzierżawą usługi Azure AD.

   2. Otwórz hello na powitania następne okienko **wybierz Region** zbyt wybierz inny region.

      ![Wybierz inny region](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Na przykład użytkownik może wybrać hello tym samym regionie co aplikację logiki lub hello wybierz region najbliższy tooyour lokalne na dane źródło, aby ograniczyć czas oczekiwania. Bramy aplikacji logiki i zasobów mogą mieć różnych lokalizacjach.

      > [!IMPORTANT]
      > Ten region nie można zmienić po zakończeniu instalacji. Ten region również określa i ogranicza lokalizacji hello umożliwiającego utworzenie hello zasobów platformy Azure dla bramy. Dlatego podczas tworzenia zasobu bramy na platformie Azure, upewnij się, czy lokalizacja zasobu hello zgodna hello regionie, który został wybrany podczas instalacji bramy.
      > 
      > Jeśli chcesz toouse inny region bramy później, należy skonfigurować nową bramę.

   3. Gdy wszystko jest gotowe, wybierz pozycję **gotowe**.

7. Teraz, można więc, wykonaj następujące kroki w portalu Azure hello [tworzenie zasobów platformy Azure dla bramy](../logic-apps/logic-apps-gateway-connection.md). 

Dowiedz się więcej o [działanie bramy danych hello](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Migracja, Przywróć lub Przejmij na istniejącą bramę

tooperform te zadania, musi mieć hello klucza odzyskiwania, który został określony podczas hello brama została zainstalowana.

1. Z menu Start komputera, wybierz **bramy danych lokalnych**.

2. Po hello Instalator zostanie otwarta, zaloguj się przy użyciu hello sam Azure pracy lub konta służbowego, który był wcześniej używany tooinstall hello bramy.

3. Wybierz **migracji, Przywróć lub Przejmij istniejącą bramę**.

4. Podaj nazwę i odzyskiwania klucz hello bramy hello, który ma być toomigrate, przywracania lub podejmij za pośrednictwem.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Ponownie uruchom bramę hello

Witaj bramy działa jako usługa systemu Windows. Podobnie jak inne usługi systemu Windows należy uruchomić i zatrzymać usługi hello na wiele sposobów. Można na przykład, otwórz wiersz polecenia z podwyższonym poziomem uprawnień na komputerze hello gdzie hello brama jest uruchomiona i uruchom obu tych poleceń:

* toostop hello usługi, uruchom to polecenie:
  
    `net stop PBIEgwService`

* toostart hello usługi, uruchom to polecenie:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Konto usługi systemu Windows

Brama danych lokalne powitania skonfigurowano toouse `NT SERVICE\PBIEgwService` dla systemu Windows hello usługi poświadczeń logowania. Domyślnie hello bramy ma prawo "Zaloguj jako usługa" hello maszyny hello zainstalowanym hello bramy.

> [!NOTE]
> Konto usługi Windows Hello różni się od hello konto używane do łączenia tooon lokalnych źródeł danych oraz hello Azure pracy lub konto służbowe używane toosign w usługach toocloud.

## <a name="configure-a-firewall-or-proxy"></a>Konfigurowanie zapory lub serwera proxy

Brama Hello tworzy połączeń wychodzących za [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). informacje o serwerze proxy tooprovide bramy, zobacz [Skonfiguruj ustawienia serwera proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck czy zapory lub serwera proxy, może zablokować połączenia, upewnij się, czy komputer faktycznie można łączyć z toohello internet i hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). Uruchom to polecenie z wiersza polecenia programu PowerShell:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> To polecenie tylko testy, łączności sieciowej i toohello łączność usługi Azure Service Bus. Dzięki hello polecenia nie ma niczego toodo hello bramy lub hello bramy usługi w chmurze są szyfrowane i przechowywane poświadczenia i szczegóły bramy. 
>
> Ponadto to polecenie jest tylko dostępne w systemie Windows Server 2012 R2 lub nowszy oraz Windows 8.1 lub nowszy. We wcześniejszych wersjach systemu operacyjnego, można użyć programu Telnet zbyt przetestować połączenia. Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Wyniki powinny wyglądać podobny przykład toothis:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Jeśli **TcpTestSucceeded** nie ustawiono zbyt**True**, może zostać zablokowany przez zaporę. Jeśli toobe kompleksowe, należy zastąpić hello **ComputerName** i **portu** wartości z wartościami hello wymienione w obszarze [skonfigurować porty](#configure-ports) w tym temacie.

Hello Zapora może również blokować połączeń, że powitalne Azure Service Bus udostępnia toohello centrach danych platformy Azure. W przypadku tego scenariusza należy zatwierdzić (odblokuj) hello wszystkie adresy IP dla tych centrach danych w danym regionie. Dla tych adresów IP [get hello Azure listy adresów IP w tym miejscu](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Skonfiguruj porty

Brama Hello tworzy połączeń wychodzących za[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) i komunikuje się portów wychodzących: TCP 443 (ustawienie domyślne), 5671, 5672, 9350 za pośrednictwem 9354. Witaj bramy nie wymaga portów przychodzących. Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| NAZWY DOMEN | PORTY WYJŚCIOWE | OPIS |
| --- | --- | --- |
| *. analysis.windows.net | 443 | HTTPS | 
| *. login.windows.net | 443 | HTTPS | 
| *. servicebus.windows.net | 5671-5672 | Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP) | 
| *. servicebus.windows.net | 443, 9350-9354 | Obiekty nasłuchujące na przekaźnik magistrali usług za pośrednictwem protokołu TCP (wymaga 443 dla tokenu przejęcie kontroli dostępu) | 
| *. frontend.clouddatahub.net | 443 | HTTPS | 
| *. core.windows.net | 443 | HTTPS | 
| Login.microsoftonline.com | 443 | HTTPS | 
| *. msftncsi.com | 443 | Połączenie z Internetem tootest należy użyć, gdy brama hello jest nieosiągalny za hello usługi Power BI. | 

Jeśli zamiast domeny hello tooapprove adresów IP, możesz pobrać i użyć hello [Microsoft Azure Datacenter IP zakresów listy](https://www.microsoft.com/download/details.aspx?id=41653). W niektórych przypadkach hello Azure Service Bus połączenia są nawiązywane z adresu IP, a nie w pełni kwalifikowanych nazw domen.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Jak działa hello bramę danych?

Brama danych Hello umożliwia szybkie i bezpieczne komunikację między aplikację logiki, hello usługi bramy w chmurze i lokalne źródła danych. 

![Diagram-for-on-premises-Data-Gateway-Flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Dlatego po hello użytkownika w chmurze hello współdziała z elementem, który został podłączony tooyour lokalnego źródła danych:

1. Hello usługi bramy w chmurze tworzy zapytanie, wraz z hello zaszyfrowane poświadczenia dla źródła danych hello i wysyła hello zapytania toohello kolejki hello tooprocess bramy.

2. Witaj usługi bramy w chmurze analizuje zapytania hello i wypchnięcia toohello żądania hello Azure Service Bus.

3. Brama danych lokalne powitania sonduje hello Azure Service Bus dla żądań oczekujących.

4. bramy Hello pobiera hello zapytania, odszyfrowuje hello poświadczeń i łączy toohello źródła danych z tych poświadczeń.

5. Brama Hello wysyła źródła danych toohello hello kwerendy do wykonania.

6. wyniki Hello są wysyłane z hello źródła danych, brama toohello Wstecz i toohello usługi bramy w chmurze. Witaj usługi bramy w chmurze używa hello wyników.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Często zadawane pytania

### <a name="general"></a>Ogólne

**Q**: należy bramy dla źródeł danych w chmurze hello, np. SQL Azure? <br/>
**A**: nie. Brama łączy lokalnych tooon tylko źródła danych.

**Q**: hello bramy ma zainstalowane na powitania sam komputer jako źródło danych hello toobe? <br/>
**A**: nie. Brama Hello łączy toohello źródła danych przy użyciu informacji o połączeniu hello dostarczony. Jako aplikacja klienta, w tym sensie, należy wziąć pod uwagę hello bramy. Witaj bramy wystarczy hello możliwości tooconnect toohello nazwy serwera podany.

<a name="why-azure-work-school-account"></a>

**Q**: Dlaczego należy I Użyj Azure pracy lub szkołą toosign konta w? <br/>
**A**: można używać Praca Azure lub tylko konta służbowego, po zainstalowaniu bramy danych lokalne powitania. Twoje konto logowania są przechowywane w dzierżawie, który jest zarządzany przez usługę Azure Active Directory (Azure AD). Zazwyczaj główna nazwa użytkownika konta usługi Azure AD (UPN) jest zgodna hello adres e-mail.

**Q**: moich poświadczeń przechowywania? <br/>
**A**: poświadczenia powitania dla źródła danych są szyfrowane i przechowywane hello bramy w usłudze w chmurze. poświadczenia Hello są odszyfrowywane w bramy danych lokalne powitania.

**Q**: istnieją wszelkie wymagania dotyczące przepustowości sieci? <br/>
**A**: zaleca się, że połączenie sieciowe ma dobrej przepływności. Każde środowisko jest inne, a hello ilość danych wysyłanych dotyczy hello wyników. Przy użyciu usługi ExpressRoute może pomóc tooguarantee poziomu przepływności między lokalnymi i hello centrach danych platformy Azure.
Możesz użyć hello narzędzia innej firmy Azure szybkości testowanie aplikacji toohelp miernika przepustowość sieci.

**Q**: co to jest hello opóźnienie dla źródła danych tooa zapytania uruchomionego z bramy hello? Co to jest architektura najlepsze hello? <br/>
**A**: tooreduce opóźnienia sieci, zainstaluj hello bramy jako źródło danych zamknij toohello, jak to możliwe. Po zainstalowaniu bramy hello w źródle danych rzeczywistych hello, to zbliżeniowe minimalizuje opóźnienia hello wprowadzone. Rozważ zbyt hello centrów danych. Na przykład jeśli usługa używa hello datacenter zachodnie stany USA, a masz programu SQL Server w maszynie Wirtualnej platformy Azure, maszyny Wirtualnej Azure należy w hello zachodnie stany USA zbyt. Ta bliskości zmniejsza opóźnienia i pozwala uniknąć opłaty za wyjście na powitania maszyny Wirtualnej platformy Azure.

**Q**: w jaki sposób wyniki wysyłane wstecz toohello chmury? <br/>
**A**: wyniki są wysyłane za pośrednictwem hello Azure Service Bus.

**Q**: czy istnieją bramy toohello wszystkie połączenia przychodzące z chmury hello? <br/>
**A**: nie. Brama Hello używa połączenia wychodzące tooAzure usługi Service Bus.

**Q**: co zrobić, jeśli zablokowanie połączeń wychodzących? Czego potrzebuję tooopen? <br/>
**A**: Zobacz hello portów i hostów, które hello używa bramy.

**Q**: rzeczywiste usługi Windows hello tzw?<br/>
**A**: W usługach, bramy hello jest nazywany Usługa bramy Power BI Enterprise.

**Q**: można hello usługa systemu Windows bramy uruchomione przy użyciu konta usługi Azure Active Directory? <br/>
**A**: nie. Usługa Windows Hello muszą mieć prawidłowe konto systemu Windows. Domyślnie usługa hello jest uruchamiana z hello SID usługi NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Wysoka dostępność i odzyskiwanie po awarii

**Q**: jakie opcje są dostępne dla odzyskiwania po awarii? <br/>
**A**: możesz użyć toorestore klucza odzyskiwania hello lub przenieść bramy. Po zainstalowaniu bramy hello Określ hello klucza odzyskiwania.

**Q**: co to jest korzyść hello hello klucza odzyskiwania? <br/>
**A**: hello klucza odzyskiwania zawiera toomigrate sposób lub odzyskiwanie po awarii ustawienia bramy.

**Q**: czy jest planowane umożliwiających realizację scenariuszy wysokiej dostępności z bramą hello? <br/>
**A**: te scenariusze są na powitania plan, ale nie mamy jeszcze osi czasu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Q**: jak zobaczyć, jakie zapytania są wysyłane toohello lokalnego źródła danych? <br/>
**A**: można włączyć funkcja śledzenia zapytań, w tym hello zapytań, które są wysyłane. Należy pamiętać, zapytania toochange Śledzenie wstecz toohello oryginalnej wartości po zakończeniu rozwiązywania problemów. Jeśli pozostanie włączona funkcja śledzenia zapytań tworzy większe dzienniki.

Można też przyjrzeć się narzędzia, które ma źródła danych śledzenia zapytań. Na przykład można użyć zdarzeń rozszerzonych lub profilera SQL dla programu SQL Server i usług Analysis Services.

**Q**: gdzie są dzienniki bramy hello? <br/>
**A**: Zobacz narzędzia w dalszej części tego tematu.

### <a name="update-toohello-latest-version"></a>Aktualizacja toohello najnowszej wersji

Wiele problemów można powierzchni, gdy wersja bramy hello staje się nieaktualne. Dobrym rozwiązaniem ogólne upewnij się, że używasz najnowszej wersji powitania. Witaj bramy nie były aktualizowane przez miesiąc lub dłużej, może zaleca się zainstalowanie najnowszej wersji bramy hello hello i zobacz, czy można odtworzyć problem hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Błąd: Nie tooadd toogroup użytkownika. (Użytkownicy dzienników wydajności PBIEgwService-2147463168)

Być może ten błąd przy próbie tooinstall hello bramy na kontrolerze domeny, który nie jest obsługiwany. Upewnij się, wdrożenie bramy hello na komputerze, który nie jest kontrolerem domeny.

## <a name="tools"></a>Narzędzia

### <a name="collect-logs-from-hello-gateway-configurer"></a>Zbieranie dzienników z hello configurer bramy

Można zbierać dzienniki kilka hello bramy. Zawsze uruchamiaj z dziennikami Witaj!

#### <a name="installer-logs"></a>Dzienniki Instalatora

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Dzienniki konfiguracji

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Dzienniki usługi bramy przedsiębiorstwa

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Dzienniki zdarzeń

Możesz znaleźć hello dzienniki bramy zarządzania danymi i PowerBIGateway w obszarze **Dzienniki aplikacji i usług**.

### <a name="fiddler-trace"></a>Śledzenie fiddler

[Fiddler](http://www.telerik.com/fiddler) to bezpłatne narzędzie ze strony firmy Telerik, który monitoruje ruch HTTP. Ten ruch z usługi Power BI z komputera klienta hello hello jest widoczny. Ta usługa mogą być wyświetlane błędy oraz inne powiązane informacje.

## <a name="next-steps"></a>Następne kroki
    
* [Połączenie lokalne tooon dane z aplikacji logiki](../logic-apps/logic-apps-gateway-connection.md)
* [Funkcje integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Łączniki dla usługi Azure Logic Apps](../connectors/apis-list.md)
