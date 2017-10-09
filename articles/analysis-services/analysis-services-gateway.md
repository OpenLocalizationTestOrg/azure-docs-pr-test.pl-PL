---
title: Brama danych lokalnych aaaOn | Dokumentacja firmy Microsoft
description: "Brama lokalnego jest konieczne, jeśli serwer usług Analysis Services na platformie Azure będą łączyć tooon lokalnych źródeł danych."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Łączenie tooon lokalnych źródeł danych z lokalnego Azure bramy danych
Brama danych lokalne powitania działa jako mostka zapewnianie bezpiecznego transferu danych między lokalnych źródeł danych i w chmurze hello serwerów usług Azure Analysis Services. W tooworking dodanie z wieloma serwerami usług Azure Analysis Services w hello tego samego regionu, hello najnowszą wersję bramy hello współdziała również z usługi Azure Logic Apps, usługi Power BI aplikacje zasilania i Flow firmy Microsoft. Można skojarzyć wielu usług w hello tym samym regionie z pojedynczą bramą. 

 Zasób bramy w hello wymaga usług Azure Analysis Services tego samego regionu. Na przykład jeśli masz serwery usług Azure Analysis Services w regionie wschodnie stany USA 2 hello należy zasobu bramy w regionie wschodnie stany USA 2 hello. Wiele serwerów w wschodnie stany USA 2 można użyć hello tą samą bramą.

Pobieranie konfiguracji z hello bramy hello po raz pierwszy jest procesem czteroczęściową:

- **Pobierz i uruchom Instalatora** -tego kroku Usługa bramy są instalowane na komputerze w organizacji.

- **Zarejestruj bramę** — w tym kroku określ nazwę i odzyskiwanie klucza bramy i wybierz region, rejestrowanie bramy z hello usługi bramy w chmurze.

- **Tworzenie zasobu bramy na platformie Azure** — w tym kroku tworzenia zasobu bramy w Twojej subskrypcji platformy Azure.

- **Połącz zasób serwerów bramy tooyour** — po utworzeniu zasobu bramy w ramach subskrypcji, możesz rozpocząć łączenia z tooit serwerów.

Po utworzeniu zasobu bramy skonfigurowane dla Twojej subskrypcji, można połączyć wiele serwerów i tooit innych usług. Tylko muszą tooinstall różnych bramy i Utwórz zasoby dodatkowe bramy, jeśli masz serwery lub innych usług w innym regionie.

Zobacz tooget pracę już teraz, [Zainstaluj i skonfiguruj bramę danych lokalnych](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Jak to działa
Brama Hello zainstalować na komputerze w organizacji działa jako usługa systemu Windows, **bramy danych lokalnych**. Ta usługa lokalna jest zarejestrowany hello usługi bramy w chmurze za pomocą usługi Azure Service Bus. Następnie można utworzyć zasobu bramy usługi bramy w chmurze dla subskrypcji platformy Azure. Twoje Azure Analysis Services, serwery są następnie połączony tooyour zasobów bramy. Gdy modele tooyour tooconnect potrzeby z serwera lokalnego źródła danych do zapytań lub przetwarzania zapytań i danych przepływu traverses hello bramy zasób usługi Azure Service Bus hello Usługa bramy lokalnej lokalnymi danymi i źródeł danych. 

![Jak to działa](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Zapytania i przepływ danych:

1. Zapytanie jest tworzony przez usługi w chmurze hello o hello zaszyfrowane poświadczenia dla źródła danych lokalne powitania. Następnie został wysłany tooa kolejki hello tooprocess bramy.
2. Witaj usługi bramy w chmurze analizuje zapytania hello i wypchnięcia toohello żądania hello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. Brama danych lokalne powitania sonduje hello Azure Service Bus dla żądań oczekujących.
4. bramy Hello pobiera hello zapytania, odszyfrowuje hello poświadczeń i łączy toohello źródeł danych z tych poświadczeń.
5. Brama Hello wysyła źródła danych toohello hello kwerendy do wykonania.
6. wyniki Hello są wysyłane z hello źródła danych, brama toohello Wstecz, a następnie na powitania usługi w chmurze, jak i na serwerze.

## <a name="windows-service-account"></a>Konta usługi systemu Windows
Hello bramy danych lokalnych jest skonfigurowany toouse *NT SERVICE\PBIEgwService* dla poświadczeń logowania usługi Windows hello. Domyślnie ma hello prawym końcu Logowanie jako usługa; w kontekście hello hello maszyna bramy hello jest instalowany na. To poświadczenie nie jest hello tego samego źródła danych konto używane tooconnect tooon lokalnego lub konta platformy Azure.  

Jeśli wystąpią problemy z serwerem proxy powodu tooauthentication, może być toochange hello Windows usługa tooa użytkownika domeny lub zarządzane konto usługi.

## <a name="ports"></a>Portów
Brama Hello tworzy tooAzure wychodzące połączenie usługi Service Bus. Komunikuje się ona portów wychodzących: TCP 443 (ustawienie domyślne), 5671, 5672, 9350 za pośrednictwem 9354.  Hello bramy nie jest wymagane porty dla ruchu przychodzącego.

Firma Microsoft zaleca dozwolonych adresów IP hello w Twoim regionie danych w zaporze. Możesz pobrać hello [listy Microsoft Azure Datacenter IP](https://www.microsoft.com/download/details.aspx?id=41653). Ta lista jest aktualizowana co tydzień.

> [!NOTE]
> Adresy IP Hello hello Azure Datacenter IP liście znajdują się w notacji CIDR. Na przykład 10.0.0.0/24 oznacza 10.0.0.0 za pośrednictwem 10.0.0.24. Dowiedz się więcej o hello [notacji CIDR](http://whatismyipaddress.com/cidr).
>
>

Oto Hello hello w pełni kwalifikowana nazwy domeny używane przez hello bramy.

| Nazwy domen | Porty wyjściowe | Opis |
| --- | --- | --- |
| *. witrynie powerbi.com |80 |Instalator hello toodownload HTTP używany. |
| *. witrynie powerbi.com |443 |HTTPS |
| *. analysis.windows.net |443 |HTTPS |
| *. login.windows.net |443 |HTTPS |
| *. servicebus.windows.net |5671-5672 |Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP) |
| *. servicebus.windows.net |443, 9350-9354 |Obiekty nasłuchujące na przekaźnik magistrali usług za pośrednictwem protokołu TCP (wymaga 443 dla tokenu przejęcie kontroli dostępu) |
| *. frontend.clouddatahub.net |443 |HTTPS |
| *. core.windows.net |443 |HTTPS |
| Login.microsoftonline.com |443 |HTTPS |
| *. msftncsi.com |443 |Połączenie z Internetem tootest należy użyć, jeśli brama hello jest nieosiągalny za hello usługi Power BI. |
| *.microsoftonline p.com |443 |Używany do uwierzytelniania w zależności od konfiguracji. |

### <a name="force-https"></a>Wymuszanie komunikację HTTPS z usługi Azure Service Bus
Możesz wymusić hello toocommunicate bramy z usługi Azure Service Bus przy użyciu protokołu HTTPS zamiast bezpośredniego TCP; Jednak to tak może znacznie zmniejszyć wydajność. Można zmodyfikować hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* pliku, zmieniając wartość hello z `AutoDetect` zbyt`Https`. Ten plik znajduje się zwykle w *bramy danych lokalnych Files\On C:\Program*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Często zadawane pytania

### <a name="general"></a>Ogólne

**Q**: należy bramy dla źródeł danych w chmurze hello, takie jak bazy danych SQL Azure? <br/>
**A**: nie. Brama łączy lokalnych tooon tylko źródła danych.

**Q**: hello bramy ma zainstalowane na powitania sam komputer jako źródło danych hello toobe? <br/>
**A**: nie. Brama Hello łączy toohello źródła danych przy użyciu informacji o połączeniu hello dostarczony. Jako aplikacja klienta, w tym sensie, należy wziąć pod uwagę hello bramy. Witaj bramy wystarczy hello możliwości tooconnect toohello nazwy serwera podany, zwykle na powitania sam sieci.

<a name="why-azure-work-school-account"></a>

**Q**: Dlaczego muszą toouse służbowego lub szkolnego konta toosign w? <br/>
**A**: można używać Praca Azure lub tylko konta służbowego, po zainstalowaniu bramy danych lokalne powitania. Twoje konto logowania są przechowywane w dzierżawie, który jest zarządzany przez usługę Azure Active Directory (Azure AD). Zazwyczaj główna nazwa użytkownika konta usługi Azure AD (UPN) jest zgodna hello adres e-mail.

**Q**: moich poświadczeń przechowywania? <br/>
**A**: poświadczenia powitania dla źródła danych są szyfrowane i przechowywane w hello usługi bramy w chmurze. poświadczenia Hello są odszyfrowywane w bramy danych lokalne powitania.

**Q**: istnieją wszelkie wymagania dotyczące przepustowości sieci? <br/>
**A**: ma zaleca sieci połączenie ma dobrej przepływności. Każde środowisko jest inne, a hello ilość danych wysyłanych dotyczy hello wyników. Przy użyciu usługi ExpressRoute może pomóc tooguarantee poziomu przepływności między lokalnymi i hello centrach danych platformy Azure.
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
**A**: W usługach, bramy hello nosi nazwę lokalną usługę bramy danych.

**Q**: można hello usługa systemu Windows bramy uruchomione przy użyciu konta usługi Azure Active Directory? <br/>
**A**: nie. Usługa Windows Hello muszą mieć prawidłowe konto systemu Windows. Domyślnie usługa hello jest uruchamiana z hello SID usługi NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Wysoka dostępność i odzyskiwanie po awarii

**Q**: jakie opcje są dostępne dla odzyskiwania po awarii? <br/>
**A**: możesz użyć toorestore klucza odzyskiwania hello lub przenieść bramy. Po zainstalowaniu bramy hello Określ hello klucza odzyskiwania.

**Q**: co to jest korzyść hello hello klucza odzyskiwania? <br/>
**A**: hello klucza odzyskiwania zawiera toomigrate sposób lub odzyskiwanie po awarii ustawienia bramy.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

**Q**: jak zobaczyć, jakie zapytania są wysyłane toohello lokalnego źródła danych? <br/>
**A**: można włączyć funkcja śledzenia zapytań, w tym hello zapytań, które są wysyłane. Należy pamiętać, zapytania toochange Śledzenie wstecz toohello oryginalnej wartości po zakończeniu rozwiązywania problemów. Jeśli pozostanie włączona funkcja śledzenia zapytań tworzy większe dzienniki.

Można też przyjrzeć się narzędzia, które ma źródła danych śledzenia zapytań. Na przykład można użyć zdarzeń rozszerzonych lub profilera SQL dla programu SQL Server i usług Analysis Services.

**Q**: gdzie są dzienniki bramy hello? <br/>
**A**: Zobacz dzienniki w dalszej części tego tematu.

### <a name="update"></a>Aktualizacja toohello najnowszej wersji

Wiele problemów można powierzchni, gdy wersja bramy hello staje się nieaktualne. Dobrym rozwiązaniem ogólne upewnij się, że używasz najnowszej wersji powitania. Witaj bramy nie były aktualizowane przez miesiąc lub dłużej, może zaleca się zainstalowanie najnowszej wersji bramy hello hello i zobacz, czy można odtworzyć problem hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Błąd: Nie tooadd toogroup użytkownika. (Użytkownicy dzienników wydajności PBIEgwService-2147463168)

Być może ten błąd przy próbie tooinstall hello bramy na kontrolerze domeny, który nie jest obsługiwany. Upewnij się, wdrożenie bramy hello na komputerze, który nie jest kontrolerem domeny.

## <a name="logs"></a>Dzienniki

Pliki dziennika są zasobów ważne podczas rozwiązywania problemów.

#### <a name="enterprise-gateway-service-logs"></a>Dzienniki usługi bramy przedsiębiorstwa

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Dzienniki konfiguracji

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Dzienniki zdarzeń

Możesz znaleźć hello dzienniki bramy zarządzania danymi i PowerBIGateway w obszarze **Dzienniki aplikacji i usług**.


## <a name="telemetry"></a>Telemetrii
Dane telemetryczne może służyć do monitorowania i rozwiązywania problemów. Domyślnie

**tooturn na telemetrii**

1.  Sprawdź katalog danych lokalnymi hello klienta bramy na komputerze hello. Zazwyczaj jest **bramy danych %systemdrive%\Program lokalnych Files\On**. Lub, otwórz konsolę usługi i sprawdź tooexecutable ścieżka hello: właściwość Usługa bramy danych lokalne powitania.
2.  W pliku Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config hello z katalogu klienta. Zmień hello SendTelemetry ustawienie tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Zapisz zmiany i ponownie uruchom usługę Windows hello: lokalnej usługi bramy danych.




## <a name="next-steps"></a>Następne kroki
* [Zarządzanie usług Analysis Services](analysis-services-manage.md)
* [Pobieranie danych z usług Azure Analysis Services](analysis-services-connect.md)
