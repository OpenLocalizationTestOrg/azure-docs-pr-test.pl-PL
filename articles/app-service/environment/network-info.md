---
title: "Zagadnienia dotyczące sieci ze środowiska usługi aplikacji Azure"
description: "Wyjaśniono ASE ruchu sieciowego i ustawiania grup NSG i Udr z Twojej ASE"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: 3ac630982b47f7105feb034982eae070faa72d9e
ms.sourcegitcommit: 8aa014454fc7947f1ed54d380c63423500123b4a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/23/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Zagadnienia dotyczące sieci dla środowiska usługi aplikacji #

## <a name="overview"></a>Omówienie ##

 Azure [środowiska usługi aplikacji] [ Intro] wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet). Istnieją dwa typy wdrażania dla środowiska usługi App Service (ASE):

- **Zewnętrzne ASE**: udostępnia aplikacje hostowane ASE na internet dostępny adres IP. Aby uzyskać więcej informacji, zobacz [Tworzenie zewnętrznych ASE][MakeExternalASE].
- **ILB ASE**: udostępnia aplikacje hostowane ASE na adres IP w sieci wirtualnej. Wewnętrzny punkt końcowy jest wewnętrzny moduł równoważenia obciążenia (ILB), dlatego jest określana mianem ASE ILB. Aby uzyskać więcej informacji, zobacz [tworzenie i używanie ASE ILB][MakeILBASE].

Teraz są dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2. Aby uzyskać informacje na ASEv1, zobacz [wprowadzenie do środowiska usługi aplikacji v1][ASEv1Intro]. ASEv1 można wdrożyć w klasyczny lub Menedżera zasobów w sieci wirtualnej. ASEv2 mogą być wdrażane tylko w sieci wirtualnej Menedżera zasobów.

Wywołania z ASE, które pobierana przez internet pozostaw sieci wirtualnej za pośrednictwem adresu VIP przypisanych do ASE. Publiczny adres IP z tego adresu VIP jest następnie źródłowy adres IP dla wszystkich wywołań z ASE pobierana przez internet. Jeśli do aplikacji w Twojej ASE wywołań do zasobów w sieci lub sieci VPN, źródłowy adres IP jest jednym z adresów IP w podsieci używane przez użytkownika ASE. Ponieważ ASE znajduje się w sieci wirtualnej, można także używać zasobów w sieci wirtualnej bez przeprowadzania dodatkowej konfiguracji. Jeśli sieć wirtualna jest podłączony do sieci lokalnej, aplikacji w Twojej ASE mają także dostęp do zasobów istnieje. Nie trzeba skonfigurować ASE lub aplikacji żadnych dalszych.

![Zewnętrzne ASE][1] 

Jeśli masz zewnętrznych ASE publicznego adresu VIP jest również punktu końcowego, który aplikacji ASE rozpoznać dla:

* HTTP/S 
* FTP/S. 
* Wdrażanie sieci Web.
* Debugowanie zdalne.

![ILB ASE][2]

Jeśli masz ASE ILB, adres IP ILB jest punkt końcowy dla protokołu HTTP/S, FTP/S, wdrożenie w sieci web i debugowanie zdalne.

Porty dostępu normalne aplikacji są:

| Użycie | Od | Do |
|----------|---------|-------------|
|  HTTP/HTTPS.  | Konfigurowane przez użytkownika |  80, 443 |
|  FTP/FTPS    | Konfigurowane przez użytkownika |  21, 990, 10001-10020 |
|  Visual Studio debugowanie zdalne  |  Konfigurowane przez użytkownika |  4016, 4018, 4020, 4022 |

Jest to wartość true, jeśli jesteś w elemencie ASE zewnętrznych lub w elemencie ASE ILB. Jeśli używasz zewnętrznego ASE naciśniesz tych portów na publiczny adres VIP. Jeśli jesteś w elemencie ASE ILB naciśniesz tych portów na ILB. Jeśli Zablokowanie portu 443, może być wpływ na niektóre funkcje widoczne w portalu. Aby uzyskać więcej informacji, zobacz [zależności Portal](#portaldep).

## <a name="ase-dependencies"></a>Zależności ASE ##

ASE zależność dostępu ruchu przychodzącego jest:

| Użycie | Od | Do |
|-----|------|----|
| Zarządzanie | Adresy zarządzania usługi aplikacji | Podsieci ASE: 454, 455 |
|  Wewnętrznej komunikacji ASE | Podsieci ASE: wszystkie porty | Podsieci ASE: wszystkie porty
|  Zezwalaj na usługi równoważenia obciążenia Azure dla ruchu przychodzącego | Moduł równoważenia obciążenia Azure | Podsieci ASE: wszystkie porty
|  Aplikacji przypisanych adresów IP | Adresy przypisywane aplikacji | Podsieci ASE: wszystkie porty

Ruch przychodzący zawiera polecenia i kontroli ASE Oprócz monitorowania systemu. Źródło adresów IP dla tego rodzaju ruch, są wymienione w [dotyczy zarządzania ASE] [ ASEManagement] dokumentu. Konfiguracja zabezpieczeń sieci należy zezwolić na dostęp z wszystkich adresów IP w portach 454 i 455.

W podsieci ASE istnieje wiele portów używanych do składnika wewnętrznej komunikacji, a można zmienić.  Wymaga to wszystkie porty w podsieci ASE mają być dostępne z podsieci ASE. 

Do komunikacji między usługi równoważenia obciążenia Azure i podsieć ASE niezbędne porty, które muszą być otwarte są 454 i 455 16001. 16001 port jest używany dla keep alive ruchu między usługi równoważenia obciążenia i ASE. Jeśli używasz ASE ILB, można zablokować ruch do właśnie 454, 455, 16001 portów.  Jeśli używasz zewnętrznego ASE należy wziąć pod uwagę porty dostępu normalne aplikacji.  Jeśli używane są adresy aplikację przypisaną należy otworzyć go do wszystkich portów.  Gdy adres jest przypisany do określonej aplikacji, usługi równoważenia obciążenia będzie używać portów, które nie są znane z wyprzedzeniem do wysyłania ruchu HTTP i HTTPS do ASE.

Jeśli używasz aplikacji przypisanych adresów IP, należy zezwolić na ruch z adresów IP przypisanych do aplikacji z podsiecią ASE.

Dla ruchu wychodzącego dostępu ASE zależy od wielu systemami zewnętrznymi. Te zależności systemu są zdefiniowane z nazwami DNS i nie mapowania ustalony zbiór adresów IP. W związku z tym ASE wymaga wychodzący dostęp do wszystkich zewnętrznych adresów IP z podsieci ASE różnych portów. ASE charakteryzuje się następującymi zależnościami wychodzących:

| Użycie | Od | Do |
|-----|------|----|
| Azure Storage | Podsieci ASE | TABLE.Core.Windows.NET, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 jest potrzebna tylko dla ASEv1.) |
| Usługa Azure SQL Database | Podsieci ASE | Database.Windows.NET: 1433, 11000 11999, 14000 14999 (Aby uzyskać więcej informacji, zobacz [użycia portu bazy danych SQL V12](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)|
| Zarządzania platformy Azure | Podsieci ASE | Management.Core.Windows.NET, management.azure.com: 443 
| Weryfikacja certyfikatu SSL |  Podsieci ASE            |  OCSP.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Usługa Azure Active Directory        | Podsieci ASE            |  Internet: 443
| Zarządzanie usługami aplikacji        | Podsieci ASE            |  Internet: 443
| System DNS platformy Azure                     | Podsieci ASE            |  Internet: 53
| Wewnętrznej komunikacji ASE    | Podsieci ASE: wszystkie porty |  Podsieci ASE: wszystkie porty

Jeśli ASE utracenia dostępu do tych zależności, przestanie działać. W takim przypadku wystarczająco długo ASE jest wstrzymana.

### <a name="customer-dns"></a>Klient DNS ###

Jeśli sieć wirtualna jest skonfigurowana na serwerze DNS przez klienta, obciążeń dzierżawców go użyć. ASE nadal wymaga do komunikacji z usługą Azure DNS do celów zarządzania. 

Jeśli sieć wirtualna jest skonfigurowana z klienta DNS po drugiej stronie sieci VPN, serwer DNS musi być dostępny w podsieci, która zawiera ASE.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Zależności portalu ##

Oprócz ASE współzależności funkcjonalnych istnieje kilka dodatkowych elementów związanych z obsługi portalu. Niektóre z funkcji w portalu Azure są zależne od bezpośredni dostęp do _lokacji SCM_. Istnieją dwa adresy URL, dla każdej aplikacji w usłudze Azure App Service. Pierwszy adres URL jest dostęp do Twojej aplikacji. Drugi adres URL jest dostęp do witryny SCM, nazywane również _konsoli Kudu_. Funkcje korzystające z lokacji SCM obejmują:

-   Zadania sieci Web
-   Funkcje
-   Przesyłanie strumieniowe dzienników
-   Kudu
-   Rozszerzenia
-   Eksplorator procesów
-   Konsola

Gdy używasz ASE ILB lokacji SCM nie jest internet dostępne spoza sieci wirtualnej. Gdy aplikacja znajduje się na elemencie ASE ILB, niektóre funkcje nie będą działać z portalu.  

Wiele z tych funkcji, które zależą od lokacji SCM są również dostępne bezpośrednio w konsoli programu Kudu. Można podłączyć do niego bezpośrednio, a nie za pomocą portalu. Jeśli aplikacja jest obsługiwana w elemencie ASE ILB, Użyj poświadczeń publikowania do logowania. Adres URL, aby uzyskać dostęp do witryny SCM aplikacji hostowanej w elemencie ASE ILB ma następujący format: 

```
<appname>.scm.<domain name the ILB ASE was created with> 
```

Jeśli Twoje ASE ILB jest nazwą domeny *contoso.net* i Twoja nazwa aplikacji jest *testapp*, aplikacja zostanie osiągnięta w *testapp.contoso.net*. Witryna SCM, która łączy się z jego osiągnięciu w *testapp.scm.contoso.net*.

## <a name="functions-and-web-jobs"></a>Funkcje i zadania sieci Web ##

Zarówno funkcje, jak i sieci Web zadania są zależne od lokacji SCM, ale można używać w portalu, nawet jeśli aplikacje będą w elemencie ASE ILB tak długo, jak przeglądarka może nawiązać połączenie lokacji SCM.  Jeśli używasz certyfikatu z podpisem własnym z Twojej ASE ILB, należy włączyć przeglądarkę, aby zaufać certyfikatowi.  Dla programu Internet Explorer i krawędzi, która oznacza, że certyfikat musi się znajdować w magazynie zaufania komputera.  Jeśli używasz programu Chrome, a następnie oznacza to, że wcześniej zaakceptowane certyfikatu w przeglądarce przez prawdopodobnie naciśnięcie lokacji scm bezpośrednio.  Najlepszym rozwiązaniem jest używanie komercyjnych certyfikatu, który znajduje się w łańcuchu przeglądarki zaufania.  

## <a name="ase-ip-addresses"></a>Adresy ASE IP ##

ASE ma kilka adresów IP, należy pamiętać o. Są to:

- **Publiczny adres IP dla ruchu przychodzącego**: używany do ruchu aplikacji w elemencie ASE zewnętrznych i ruch związany z zarządzaniem w elemencie ASE zewnętrznych i ASE ILB.
- **Wychodzące publicznego adresu IP**: używany jako adres IP "od" dla połączenia wychodzące z ASE pozostaw sieci wirtualnej, które nie są przesyłane w dół sieci VPN.
- **Adres ILB IP**: Jeśli używasz ASE ILB.
- **Adresy przypisane aplikacji opartych na protokole SSL**: tylko to możliwe z zewnętrznego ASE i opartych na protokole SSL jest skonfigurowany.

Te adresy IP są łatwo widoczna w ASEv2 w portalu Azure w interfejsie użytkownika ASE. Jeśli masz ASE ILB, znajduje się adres IP dla ILB.

![Adresy IP][3]

### <a name="app-assigned-ip-addresses"></a>Adresy IP przypisane aplikacji ###

Z zewnętrznego ASE adresów IP można przypisać do poszczególnych aplikacji. Nie możesz tego zrobić z ASE ILB. Aby uzyskać więcej informacji na temat konfigurowania aplikacji na adres IP, zobacz [Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci web platformy Azure](../app-service-web-tutorial-custom-ssl.md).

Gdy aplikacja ma własny adres opartych na protokole SSL, ASE rezerwuje dwa porty do mapowania na ten adres IP. Jest jeden port dla ruchu HTTP i jest innego portu dla protokołu HTTPS. Te porty są wyświetlane w interfejsie użytkownika ASE w sekcji adresów IP. Ruch musi mieć dostęp do tych portów z adresu VIP lub aplikacje są niedostępne. To wymaganie dotyczy pamiętać podczas konfigurowania grup zabezpieczeń sieci (NSG).

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci ##

[Sieciowe grupy zabezpieczeń] [ NSGs] zapewniają możliwość kontrolowania dostępu do sieci w ramach sieci wirtualnej. Korzystając z portalu, istnieje reguła niejawna odmowa na najniższy priorytet odrzucanie wszystko. Możesz utworzyć są z reguły zezwalania.

W elemencie ASE nie masz dostępu do maszyn wirtualnych, używany do obsługi ASE samej siebie. Są one w ramach subskrypcji zarządzany przez firmę Microsoft. Jeśli chcesz ograniczyć dostęp do aplikacji w ASE, należy ustawić grup NSG podsieci ASE. W ten sposób należy zwrócić uwagę dokładne ASE zależności. Jeśli zablokujesz wszelkie zależności ASE przestanie działać.

Grupy NSG można skonfigurować za pomocą portalu Azure lub za pomocą programu PowerShell. Informacje w tym miejscu przedstawiono portalu Azure. Utwórz i Zarządzaj grup NSG w portalu jako zasób najwyższego poziomu w obszarze **sieci**.

Gdy wymagania dla ruchu przychodzącego i wychodzącego są brane pod uwagę, grup NSG powinien wyglądać podobnie do grup NSG, w poniższym przykładzie. Zakres adresów sieci wirtualnej jest _192.168.250.0/16_, i podsieci, która jest ASE _192.168.251.128/25_.

Pierwsze dwa wymagania dla ruchu przychodzącego ASE funkcji są wyświetlane na początku listy, w tym przykładzie. Włącz zarządzanie ASE, a Zezwalaj ASE do komunikowania się z nim samym. Inne pozycje są wszystkie konfigurowalne dzierżawy i można kontrolować dostępu do sieci dla aplikacji hostowanej ASE. 

![Reguły zabezpieczeń ruchu przychodzącego][4]

Domyślna reguła umożliwia adresów IP w sieci wirtualnej do komunikowania się z podsiecią ASE. Inna reguła domyślna umożliwia usługi równoważenia obciążenia, znanej także jako publiczny adres VIP, do komunikowania się z ASE. Aby wyświetlić reguły domyślne, wybierz **domyślne zasady** obok **Dodaj** ikony. Umieszczenie Odmów, wszystkie inne reguły po pokazano reguły grupy NSG, uniemożliwia ruch między adres VIP i ASE. Aby zapobiec ruchu przychodzącego z wewnątrz sieci wirtualnej, należy dodać własne reguły zezwalającej na przychodzące. Używać źródła równa AzureLoadBalancer, których miejscem docelowym **żadnych** i zakres portów  **\*** . Ponieważ reguła grupa NSG jest stosowana do podsieci ASE, nie trzeba być specyficzne dla miejsca docelowego.

Jeśli adres IP jest przypisany do aplikacji, upewnij się, że porty stale otwarte. Aby wyświetlić porty, wybierz **środowiska usługi aplikacji** > **adresów IP**.  

Wszystkie elementy, które są widoczne w następujące reguły wychodzące są potrzebne, z wyjątkiem ostatniego elementu. Umożliwiają one dostęp sieciowy do zależności ASE, które zostały wymienione w tym artykule. Jeśli zablokujesz ich z ASE przestanie działać. Ostatni element na liście umożliwia Twojej ASE do komunikowania się z innymi zasobami w sieci wirtualnej.

![Zasady zabezpieczeń dla ruchu wychodzącego][5]

Po zdefiniowaniu grup NSG, należy je przypisać do podsieci, która jest Twoje ASE na. Jeśli nie pamiętasz ASE sieci wirtualnej lub podsieci, można to sprawdzić na stronie portalu ASE. Aby przypisać grupie NSG do podsieci, przejdź do podsieci interfejsu użytkownika, a następnie wybierz grupy NSG.

## <a name="routes"></a>Trasy ##

Trasy stanie najczęściej powodować problemy podczas konfigurowania sieci wirtualnej z platformy Azure ExpressRoute. Istnieją trzy typy tras w sieci wirtualnej:

-   Trasy systemowe
-   Trasy protokołu BGP
-   Trasy zdefiniowane przez użytkownika (Udr)

Trasy protokołu BGP musi zostać zastąpiona tras systemowych. Udr zastąpić trasy protokołu BGP. Aby uzyskać więcej informacji dotyczących tras w sieci wirtualnych platformy Azure, zobacz [trasy zdefiniowane przez użytkownika — omówienie][UDRs].

Baza danych Azure SQL, która ASE używa do zarządzania systemem ma zapory. Wymaga to pochodzą z publicznych adresów VIP ASE komunikacji. Połączenia z bazą danych SQL z ASE będą odrzucane, jeśli są one wysyłane połączenie ExpressRoute i innego adresu IP.

Jeśli odpowiedzi na przychodzące żądania zarządzania są wysyłane w dół usługi ExpressRoute, adres, który różni się od początkowego miejsca docelowego. Ta niezgodność przerywa komunikację protokołu TCP.

Dla Twojego ASE pracę podczas sieci wirtualnej jest skonfigurowana z ExpressRoute najłatwiejszym jest:

-   Konfigurowanie usługi ExpressRoute anonsowanie _0.0.0.0/0_. Domyślnie go wymusić tuneli wszystkie wychodzący ruch lokalnymi.
-   Utwórz przez. Dotyczą podsieci, która zawiera ASE z prefiksem adresu o _0.0.0.0/0_ i następnego przeskoku typu _Internet_.

Jeśli te dwie zmiany, ruch kierowany przez internet pochodzący z podsieci ASE nie jest wymuszone usługi ExpressRoute i ASE działa. 

> [!IMPORTANT]
> Trasy zdefiniowane w przez musi być wystarczająco konkretny, aby mają pierwszeństwo względem dowolnego trasy anonsowane przez konfiguracji usługi ExpressRoute. W poprzednim przykładzie użyto 0.0.0.0/0 szerokiego zakresu adresów. Go może potencjalnie być przypadkowo zastąpione anonsów tras, korzystających z bardziej szczegółowych zakresów adresów.
>
> ASEs nie są obsługiwane w przypadku konfiguracji usługi ExpressRoute, które między anonsować tras z publicznej komunikacji równorzędnej ścieżki do ścieżki prywatnej komunikacji równorzędnej. Konfiguracji usługi ExpressRoute z publicznej komunikacji równorzędnej skonfigurowane otrzymywać anonsów tras od firmy Microsoft. Anonse zawiera zbiór duże zakresy adresów IP firmy Microsoft Azure. W przypadku zakresów adresów między anonsowany w ścieżce prywatnej komunikacji równorzędnej, wszystkie pakiety wychodzącego z podsieci ASE są życie tunel do infrastruktury sieci lokalnej klienta. Ten przepływ sieci nie jest obecnie obsługiwane z ASEs. Jedno rozwiązanie tego problemu jest zatrzymanie tras między reklamy ze ścieżki publicznej komunikacji równorzędnej do ścieżki prywatnej komunikacji równorzędnej.

Aby utworzyć przez, wykonaj następujące kroki:

1. Przejdź do portalu Azure. Wybierz **sieci** > **tabel tras**.

2. Utwórz nową tabelę tras w tym samym regionie co sieci wirtualnej.

3. W tabeli routingu interfejsu użytkownika, zaznacz **tras** > **Dodaj**.

4. Ustaw **następnego przeskoku typu** do **Internet** i **prefiks adresu** do **0.0.0.0/0**. Wybierz pozycję **Zapisz**.

    Zostanie wyświetlony ekran podobny do następującego:

    ![Trasy funkcjonalności][6]

5. Po utworzeniu nowej tabeli tras, przejdź do podsieci, która zawiera ASE użytkownika. Wybierz z tabeli tras z listy w portalu. Po zapisaniu zmian, należy następnie zobacz grupy NSG i oznaczane przy użyciu podsieci trasy.

    ![Tras i grupy NSG][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Wdróż do istniejącej sieci wirtualnych platformy Azure zintegrowanych z usługi ExpressRoute ###

Do wdrożenia programu ASE w sieci wirtualnej, który jest zintegrowany z usługi ExpressRoute, należy wstępnie skonfigurować podsieci, w którym ma ASE wdrożone. Następnie należy użyć szablonu usługi Resource Manager jej wdrożenia. Aby utworzyć ASE w sieci wirtualnej który już ma ExpressRoute skonfigurowane:

- Utwórz podsieć do hostowania ASE.

    > [!NOTE]
    > Nic może być w tej podsieci, ale ASE. Należy wybrać przestrzeń adresową, która umożliwia rozwój w przyszłości. Nie można zmienić tego ustawienia później. Firma Microsoft zaleca rozmiar `/25` z adresami 128.

- Utwórz Udr (na przykład, tabele tras), jak opisano wcześniej i ustawić go w podsieci.
- Tworzenie ASE przy użyciu szablonu usługi Resource Manager, zgodnie z opisem w [utworzyć ASE przy użyciu szablonu usługi Resource Manager][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
