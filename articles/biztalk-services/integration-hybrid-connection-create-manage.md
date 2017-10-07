---
title: "aaaCreate i Zarządzaj połączeniami hybrydowe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać połączenia hello toocreate połączenie hybrydowe i zainstalować hello Menedżera połączeń hybrydowych. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Tworzenie połączeń hybrydowych i zarządzanie nimi

> [!IMPORTANT]
> Połączenia hybrydowe BizTalk zostały wycofane i zastąpione połączeniami hybrydowymi usługi App Service. Aby uzyskać więcej informacji, łącznie ze sposobem toomanage istniejących połączeń hybrydowych BizTalk zobacz [połączeń hybrydowych usługi aplikacji Azure](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Omówienie kroków hello
1. Tworzenie połączenia hybrydowego wprowadzając hello **nazwy hosta** lub **FQDN** hello zasobów lokalnych w sieci prywatnej.
2. Łączenie z aplikacjami sieci web platformy Azure lub usługi Azure mobile apps toohello połączenia hybrydowego.
3. Zainstaluj Menedżera połączeń hybrydowych hello na zasób lokalną i połącz toohello określonego połączenia hybrydowego. Hello Azure portal udostępnia tooinstall środowisko jednym kliknięciem i nawiąż połączenie.
4. Zarządzanie połączeń hybrydowych i ich kluczy połączenia.

Ten temat zawiera następujące kroki. 

> [!IMPORTANT]
> Jest możliwe tooset adresu IP tooan punktu końcowego połączenia hybrydowego. Jeśli używasz adresu IP, może lub nie może skontaktować się zasób lokalną hello, w zależności od klienta. Witaj połączenia hybrydowego zależy od powitania klienta podczas wyszukiwania DNS. W większości przypadków hello **klienta** jest kod aplikacji. Jeśli hello klient wykonuje wyszukiwania DNS, (nie jest jego adres IP hello tooresolve tak, jakby był on nazwę domeny (x.x.x.x)), a następnie ruchu nie są wysyłane za pośrednictwem hello połączenia hybrydowego.
> 
> Na przykład (pseudocode), należy zdefiniować **10.4.5.6** jako hosta lokalnego:
> 
> **Witaj, następujące działania scenariusza:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **nie działa Hello następujących scenariuszy:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Tworzenie połączenia hybrydowego
Połączenie hybrydowe mogą być tworzone w hello portalu Azure za pomocą aplikacji sieci Web **lub** przy użyciu usługi BizTalk Services. 

**toocreate połączeń hybrydowych było możliwe za pomocą aplikacji sieci Web**, zobacz [tooan połączenia aplikacji sieci Web Azure zasób lokalną](../app-service-web/web-sites-hybrid-connection-get-started.md). Można także zainstalować hello Menedżera połączeń hybrydowych (HCM) z aplikacji sieci web, czyli hello preferowana metoda. 

**toocreate połączeń hybrydowych w usługi BizTalk Services**:

1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz w okienku nawigacji po lewej stronie powitania **usługi BizTalk Services** , a następnie wybierz usługę BizTalk. 
   
    Jeśli nie masz istniejącej usługi BizTalk, możesz [Utwórz usługę BizTalk](biztalk-provision-services.md).
3. Wybierz hello **połączeń hybrydowych** karty:  
   ![Karta połączenia hybrydowego][HybridConnectionTab]
4. Wybierz **Tworzenie połączenia hybrydowego** lub wybierz hello **dodać** przycisku na pasku zadań hello. Wprowadź poniżej hello:
   
   | Właściwość | Opis |
   | --- | --- |
   | Nazwa |Witaj połączenia hybrydowego nazwy muszą być unikatowe i nie może być hello takie same nazwy jako hello usługi BizTalk. Można wprowadź dowolną nazwę, ale przeznaczone z jej celem. Przykłady:<br/><br/>Lista płac*SQLServer*<br/>SupplyList*SharepointServer*<br/>Klienci*OracleServer* |
   | Nazwa hosta |Wprowadź nazwę FQDN hosta hello, tylko nazwę hosta hello, lub hello adres IPv4 hello zasobów lokalnych. Przykłady:<br/><br/>Mójserwersql<br/>*Mójserwersql*. *Domeny*. corp.*NazwaFirmy*com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*. *NazwaFirmy*com<br/>10.100.10.10<br/><br/>Użycie adresu IPv4 hello, należy pamiętać, że kod klienta lub aplikacji nie może rozpoznać adresu IP hello. Zobacz hello ważne Uwaga na początku hello w tym temacie. |
   | Port |Wprowadź numer portu hello hello zasobu lokalnego. Na przykład jeśli używasz aplikacji sieci Web, wprowadź port 80 lub port 443. Jeśli używasz programu SQL Server, wprowadź port 1433. |
5. Wybierz hello znacznik wyboru toocomplete hello Instalatora. 

#### <a name="additional"></a>Informacje dodatkowe
* Można tworzyć wiele połączeń hybrydowych. Zobacz hello [usługi BizTalk Services: wykres wersje](biztalk-editions-feature-chart.md) hello liczbę dozwolonych połączeń. 
* Każde połączenie hybrydowe jest tworzony przy użyciu pary ciągów połączeń: aplikacja klucze tego WYSYŁANIA i lokalnymi klucze, które NASŁUCHUJĄ. Każda para ma podstawowego i pomocniczego klucza. 

## <a name="LinkWebSite"></a>Łączenie aplikacji mobilnej lub aplikacji sieci Web usługi aplikacji Azure
Wybierz aplikację sieci Web lub aplikacji mobilnej toolink w usłudze Azure App Service tooan istniejące połączenie hybrydowe **Użyj istniejącego połączenia hybrydowego** w bloku połączeń hybrydowych hello. Zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Zainstaluj hello Menedżera połączeń hybrydowych lokalnej
Po utworzeniu połączenia hybrydowego hello zasobu lokalnego należy zainstalować hello Menedżera połączeń hybrydowych. Można go pobrać z aplikacji sieci web platformy Azure lub usługi BizTalk. Usługi BizTalk Services kroki: 

1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz w okienku nawigacji po lewej stronie powitania **usługi BizTalk Services** , a następnie wybierz usługę BizTalk. 
3. Wybierz hello **połączeń hybrydowych** karty:  
   ![Karta połączenia hybrydowego][HybridConnectionTab]
4. Na pasku zadań hello, wybierz **instalacji lokalnej**:  
   ![Ustawienia lokalnych][HCOnPremSetup]
5. Wybierz **zainstalować i skonfigurować** toorun lub pobierania hello Menedżera połączeń hybrydowych na powitania lokalnego systemu. 
6. Wybierz hello znacznik wyboru toostart hello instalacji. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Informacje dodatkowe
* Menedżera połączeń hybrydowych można zainstalować na powitania następujące systemy operacyjne:
  
  * Windows Server 2008 R2 (.NET Framework 4.5 + i Windows Management Framework 4.0 + wymagane)
  * Windows Server 2012 (Windows Management Framework 4.0 + wymagane)
  * Windows Server 2012 R2
* Po zainstalowaniu hello Menedżera połączeń hybrydowych występuje hello następujące czynności: 
  
  * Witaj połączenia hybrydowego hostowanej na platformie Azure jest automatycznie skonfigurowana toouse hello podstawowe parametry połączenia aplikacji. 
  * zasób lokalną Hello jest automatycznie skonfigurowana toouse hello podstawowe parametry połączenia lokalnego.
* Witaj Menedżera połączeń hybrydowych należy użyć lokalnej prawidłowe parametry połączenia do autoryzacji. Hello Azure Web Apps lub Mobile Apps musi mieć prawidłową aplikację parametry połączenia do autoryzacji.
* Można skalować połączeń hybrydowych było możliwe, instalując inne wystąpienie Menedżera połączeń hybrydowych hello na innym serwerze. Skonfiguruj hello lokalnymi odbiornika toouse hello sama adresu jako pierwszy odbiornika lokalne powitania. W takiej sytuacji ruch hello jest losowo rozproszone (działanie okrężne) między hello active lokalnymi odbiorników. 

## <a name="ManageHybridConnection"></a>Zarządzanie połączeń hybrydowych
toomanage połączeń hybrydowych, można wykonywać następujące czynności:

* Użyć hello portalu Azure i przejść tooyour usługi BizTalk. 
* Użyj [interfejsów API REST](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Parametry połączenia hybrydowe hello kopiowania/regenerate
1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz w okienku nawigacji po lewej stronie powitania **usługi BizTalk Services** , a następnie wybierz usługę BizTalk. 
3. Wybierz hello **połączeń hybrydowych** karty:  
   ![Karta połączenia hybrydowego][HybridConnectionTab]
4. Wybierz hello połączenia hybrydowego. Na pasku zadań hello, wybierz **Zarządzanie połączenia**:  
   ![Zarządzanie opcjami][HCManageConnection]
   
    **Zarządzanie połączenia** list hello parametry połączenia aplikacji i lokalnie. Możesz skopiować hello parametry połączenia lub ponownie wygenerować klucz dostępu używany w parametrach połączenia hello powitalne. 
   
    **W przypadku wybrania Regenerate**, hello udostępniony klucz dostępu używany w ramach hello parametry połączenia zostaną zmienione. Witaj, po:
   
   * Hello klasycznego portalu Azure, wybierz **synchronizacji kluczy** w hello aplikacji Azure.
   * Uruchom ponownie hello **instalacji lokalnej**. Podczas ponownego uruchamiania hello instalacji lokalnej, powitalne zasób lokalną jest automatycznie skonfigurować parametry połączenia podstawowej hello zaktualizowane toouse.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Użyj grupy zasad toocontrol hello lokalnej zasoby używane przez połączenie hybrydowe
1. Pobierz hello [szablonów administracyjnych Menedżera połączeń hybrydowych](http://www.microsoft.com/download/details.aspx?id=42963).
2. Wyodrębnij pliki hello.
3. Na komputerze hello, który modyfikuje zasad grupy hello następujące:  
   
   * Skopiuj hello. ADMX pliki toohello *%WINROOT%\PolicyDefinitions* folderu.
   * Skopiuj hello. ŚILS pliki toohello *%WINROOT%\PolicyDefinitions\en-us* folderu.

Po skopiowaniu, można użyć zasad hello toochange Edytor zasad grupy.

## <a name="next"></a>Następne kroki
[Łączenie aplikacji sieci Web Azure tooan zasób lokalną](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Połącz tooon lokalnego programu SQL Server z aplikacji sieci Web Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Omówienie połączeń hybrydowych](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Zobacz też
[Interfejs API REST zarządzania usługi BizTalk Services na platformie Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[BizTalk Services: Editions Chart (Usługa BizTalk Services: zestawienie wersji)](biztalk-editions-feature-chart.md)  
[Utwórz usługę BizTalk przy użyciu klasycznego portalu Azure](biztalk-provision-services.md)  
[BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
