---
title: "zagadnienia dotyczące aaaNetworking ze środowiska usługi aplikacji Azure"
description: "Wyjaśniono hello ASE ruchu sieciowego i w jaki sposób tooset grup NSG i Udr z Twojej ASE"
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
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Zagadnienia dotyczące sieci dla środowiska usługi aplikacji #

## <a name="overview"></a>Omówienie ##

 Azure [środowiska usługi aplikacji] [ Intro] wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet). Istnieją dwa typy wdrażania dla środowiska usługi App Service (ASE):

- **Zewnętrzne ASE**: ujawnia hello aplikacji hostowanej ASE na internet dostępny adres IP. Aby uzyskać więcej informacji, zobacz [Tworzenie zewnętrznych ASE][MakeExternalASE].
- **ILB ASE**: ujawnia hello hostowanej ASE aplikacji na adres IP w sieci wirtualnej. Wewnętrzny punkt końcowy Hello jest wewnętrzny moduł równoważenia obciążenia (ILB), dlatego jest określana mianem ASE ILB. Aby uzyskać więcej informacji, zobacz [tworzenie i używanie ASE ILB][MakeILBASE].

Teraz są dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2. Aby uzyskać informacje na ASEv1, zobacz [tooApp wprowadzenie v1 środowiska usługi][ASEv1Intro]. ASEv1 można wdrożyć w klasyczny lub Menedżera zasobów w sieci wirtualnej. ASEv2 mogą być wdrażane tylko w sieci wirtualnej Menedżera zasobów.

Wywołania z ASE wykraczające toohello internet pozostaw hello sieci wirtualnej za pośrednictwem adresu VIP przypisanych do hello ASE. Witaj publicznego adresu IP z tego adresu VIP jest następnie hello źródłowy adres IP dla wszystkich wywołań z hello ASE Przejdź toohello internet. Jeśli aplikacji hello w Twojej ASE tooresources wywołań w sieci lub sieci VPN, hello źródłowy adres IP jest jednym z hello adresów IP w podsieci hello używany przez Twoje ASE. Ponieważ hello ASE znajduje się wewnątrz hello sieci wirtualnej, można także używać zasobów w ramach hello sieci wirtualnej bez przeprowadzania dodatkowej konfiguracji. Jeśli hello sieci wirtualnej sieci lokalnej podłączonej tooyour, aplikacje w Twojej ASE również mają tooresources dostępu istnieje. Nie trzeba tooconfigure hello ASE lub aplikacji żadnych dalszych.

![Zewnętrzne ASE][1] 

Jeśli masz zewnętrznych ASE hello publicznego adresu VIP jest również hello punktu końcowego, że aplikacje ASE rozpoznać toofor:

* HTTP/S 
* FTP/S. 
* Wdrażanie sieci Web.
* Debugowanie zdalne.

![ILB ASE][2]

Jeśli masz ASE ILB, adres IP hello hello ILB jest hello końcowy dla protokołu HTTP/S, FTP/S, wdrożenie w sieci web i debugowanie zdalne.

porty dostępu normalne aplikacji Hello są:

| Użycie | Z | zbyt|
|----------|---------|-------------|
|  HTTP/HTTPS.  | Konfigurowane przez użytkownika |  80, 443 |
|  FTP/FTPS    | Konfigurowane przez użytkownika |  21, 990, 10001-10020 |
|  Visual Studio debugowanie zdalne  |  Konfigurowane przez użytkownika |  4016, 4018, 4020, 4022 |

Jest to wartość true, jeśli jesteś w elemencie ASE zewnętrznych lub w elemencie ASE ILB. Jeśli używasz zewnętrznego ASE naciśniesz tych portów na powitania publicznego adresu VIP. Jeśli jesteś w elemencie ASE ILB naciśniesz tych portów na powitania ILB. Jeśli Zablokowanie portu 443, może być wpływ na niektóre funkcje widoczne w portalu hello. Aby uzyskać więcej informacji, zobacz [zależności Portal](#portaldep).

## <a name="ase-dependencies"></a>Zależności ASE ##

ASE zależność dostępu ruchu przychodzącego jest:

| Użycie | Z | zbyt|
|-----|------|----|
| Zarządzanie | Adresy zarządzania usługi aplikacji | Podsieci ASE: 454, 455 |
|  Wewnętrznej komunikacji ASE | Podsieci ASE: wszystkie porty | Podsieci ASE: wszystkie porty
|  Zezwalaj na usługi równoważenia obciążenia Azure dla ruchu przychodzącego | Moduł równoważenia obciążenia Azure | Podsieci ASE: wszystkie porty
|  Aplikacji przypisanych adresów IP | Adresy przypisywane aplikacji | Podsieci ASE: wszystkie porty

Hello ruchu przychodzącego udostępnia polecenia i kontroli ASE hello dodanie toosystem monitorowania. Źródło Hello adresów IP dla tego rodzaju ruch, są wyświetlane w hello [dotyczy zarządzania ASE] [ ASEManagement] dokumentu. Konfiguracja zabezpieczeń sieci Hello wymaga dostępu tooallow z wszystkich adresów IP w portach 454 i 455.

W podsieci hello ASE istnieje wiele porty używane do wewnętrznej komunikacji i mogą zmieniać.  Wymaga to wszystkie porty hello w hello ASE podsieci toobe dostępny z hello ASE podsieci. 

Witaj komunikacji między modułu równoważenia obciążenia Azure hello i hello ASE podsieci hello niezbędne porty tego toobe potrzeby otwórz są 454 i 455 16001. Hello 16001 port jest używany keep alive ruch między hello modułu równoważenia obciążenia i hello ASE. Jeśli używasz ASE ILB można zablokować ruch w dół toojust hello 454, 455, 16001 portów.  Jeśli używasz zewnętrznego ASE należy tootake do konta hello normalne aplikacji dostępu do portów.  Jeśli używane są adresy aplikację przypisaną należy tooopen go tooall portów.  Adres przypisany tooa specyficzne dla aplikacji, usługi równoważenia obciążenia hello użyje portów, które nie są znane z wyprzedzeniem toosend HTTP i HTTPS ruchu toohello ASE.

Jeśli używane są adresy IP przypisane aplikacji należy tooallow ruch z powitalne adresy IP przypisane tooyour aplikacji toohello ASE podsieci.

Dla ruchu wychodzącego dostępu ASE zależy od wielu systemami zewnętrznymi. Te zależności systemu są zdefiniowane z nazwami DNS i nie mapują tooa ustalony zbiór adresów IP. W związku z tym hello ASE wymaga wychodzący dostęp z tooall podsieci hello ASE zewnętrznych adresów IP w różnych portów. ASE ma powitania po wychodzącego zależności:

| Użycie | Z | zbyt|
|-----|------|----|
| Azure Storage | Podsieci ASE | TABLE.Core.Windows.NET, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 jest potrzebna tylko dla ASEv1.) |
| Usługa Azure SQL Database | Podsieci ASE | Database.Windows.NET: 1433, 11000 11999, 14000 14999 (Aby uzyskać więcej informacji, zobacz [użycia portu bazy danych SQL V12](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)|
| Zarządzania platformy Azure | Podsieci ASE | Management.Core.Windows.NET, management.azure.com: 443 
| Weryfikacja certyfikatu SSL |  Podsieci ASE            |  OCSP.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Usługa Azure Active Directory        | Podsieci ASE            |  Internet: 443
| Zarządzanie usługami aplikacji        | Podsieci ASE            |  Internet: 443
| System DNS platformy Azure                     | Podsieci ASE            |  Internet: 53
| Wewnętrznej komunikacji ASE    | Podsieci ASE: wszystkie porty |  Podsieci ASE: wszystkie porty

Jeśli hello ASE utracenia dostępu toothese zależności, przestanie działać. Jeśli tak się stanie długo za mało, ASE hello jest wstrzymana.

### <a name="customer-dns"></a>Klient DNS ###

Jeśli hello sieć wirtualna jest skonfigurowana na serwerze DNS przez klienta, obciążeń dzierżawców hello go użyć. Witaj ASE nadal wymaga toocommunicate z usługi Azure DNS do celów zarządzania. 

Jeśli hello sieć wirtualna jest skonfigurowana z klienta DNS na hello drugiej stronie sieci VPN, hello serwer DNS musi być dostępny z hello podsieci, która zawiera hello ASE.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Zależności portalu ##

W toohello ASE dodawania funkcjonalności zależności istnieje kilka dodatkowych elementów powiązanych toohello portalu obsługi. Niektóre możliwości hello w portalu Azure hello są zależne od site_ too_SCM bezpośredni dostęp. Istnieją dwa adresy URL, dla każdej aplikacji w usłudze Azure App Service. pierwszy adres URL Hello jest tooaccess aplikacji. Witaj drugi adres URL jest tooaccess hello SCM lokacji, który jest również nazywany hello _konsoli Kudu_. Funkcje używające hello SCM lokacji:

-   Zadania sieci Web
-   Funkcje
-   Dziennik przesyłania strumieniowego
-   Kudu
-   Rozszerzenia
-   Eksplorator procesów
-   Konsola

Użycie ASE ILB, hello SCM lokacji nie jest dostępny spoza sieci wirtualnej hello internet. Kiedy aplikacji znajduje się w elemencie ASE ILB, niektóre funkcje nie będą działać z hello portalu.  

Wiele z tych funkcji, które zależą od lokacji SCM hello są również dostępne bezpośrednio w konsoli Kudu hello. Możesz połączyć tooit bezpośrednio, a nie za pomocą portalu hello. Jeśli aplikacja jest obsługiwana w elemencie ASE ILB, użyj programu publikowania toosign poświadczeń w. Hello lokacji SCM hello tooaccess adres URL aplikacji hostowanej w elemencie ASE ILB ma hello następującego formatu: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

Jeśli Twoje ASE ILB jest nazwą domeny hello *contoso.net* i Twoja nazwa aplikacji jest *testapp*, aplikacja hello osiągnięciu na *testapp.contoso.net*. Hello SCM lokacji, która łączy się z jego osiągnięciu na *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>Funkcje i zadania sieci Web ###

Zarówno funkcje, jak i sieci Web zadania są zależne od hello SCM lokacji, ale można używać w portalu hello, nawet jeśli aplikacje będą w elemencie ASE ILB tak długo, jak przeglądarka może nawiązać połączenie hello SCM lokacji.  Jeśli używasz certyfikatu z podpisem własnym z Twojej ASE ILB, konieczne będzie tooenable Twojego tootrust przeglądarki, który certyfikat.  Dla programu Internet Explorer i krawędzi, który oznacza, że certyfikat hello ma toobe w relacji zaufania komputera hello przechowywania.  Jeśli używasz programu Chrome, a następnie oznacza to, że wcześniej zaakceptowane hello certyfikatu w przeglądarce hello przez prawdopodobnie naciśnięcie hello scm lokacji bezpośrednio.  Witaj najlepszym rozwiązaniem jest toouse komercyjnych certyfikat w łańcuchu przeglądarki hello zaufania.  

## <a name="ase-ip-addresses"></a>Adresy ASE IP ##

ASE ma kilka toobe adresy IP znane. Są to:

- **Publiczny adres IP dla ruchu przychodzącego**: używany do ruchu aplikacji w elemencie ASE zewnętrznych i ruch związany z zarządzaniem w elemencie ASE zewnętrznych i ASE ILB.
- **Wychodzące publicznego adresu IP**: używany jako hello "od" IP dla połączenia wychodzące z hello ASE tego hello pozostaw sieci wirtualnej, które nie są przesyłane w dół sieci VPN.
- **Adres ILB IP**: Jeśli używasz ASE ILB.
- **Adresy przypisane aplikacji opartych na protokole SSL**: tylko to możliwe z zewnętrznego ASE i opartych na protokole SSL jest skonfigurowany.

Te adresy IP są łatwo widoczna w ASEv2 w portalu Azure hello z hello ASE interfejsu użytkownika. Jeśli masz ASE ILB hello IP dla hello ILB, znajduje się.

![Adresy IP][3]

### <a name="app-assigned-ip-addresses"></a>Adresy IP przypisane aplikacji ###

Za pomocą zewnętrznego ASE można przypisać adresów IP tooindividual aplikacji. Nie możesz tego zrobić z ASE ILB. Aby uzyskać więcej informacji na temat tooconfigure toohave Twojej aplikacji własnego adresu IP, zobacz [Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacje sieci web](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Gdy aplikacja ma własny adres opartych na protokole SSL, hello ASE rezerwuje dwa porty toomap toothat adresu IP. Jeden port dla ruchu HTTP, i hello innych port jest dla protokołu HTTPS. Te porty są wyświetlane w hello ASE interfejsu użytkownika, w sekcji adresy IP hello. Ruch musi być możliwe tooreach tych portów z aplikacji hello lub hello VIP są niedostępne. To wymaganie dotyczy tooremember ważne podczas konfigurowania grup zabezpieczeń sieci (NSG).

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci ##

[Sieciowe grupy zabezpieczeń] [ NSGs] zapewnić hello możliwości toocontrol dostęp w sieci wirtualnej. Korzystając z portalu hello, istnieje niejawna odmowa reguły na powitania najniższy priorytet toodeny wszystko. Możesz utworzyć są z reguły zezwalania.

W elemencie ASE nie ma systemu dostępu toohello maszyn wirtualnych użyć toohost hello ASE samej siebie. Są one w ramach subskrypcji zarządzany przez firmę Microsoft. Jeśli chcesz, aby toorestrict dostępu toohello aplikacje na powitania ASE, należy ustawić grup NSG podsieci ASE hello. W ten sposób należy zwrócić uwagę dokładne toohello ASE zależności. Jeśli zablokujesz wszelkie zależności hello ASE przestaje działać.

Grupy NSG można skonfigurować za pomocą hello portalu Azure lub za pomocą programu PowerShell. tutaj informacje Hello pokazuje hello portalu Azure. Utwórz i Zarządzaj grup NSG w portalu hello jako zasób najwyższego poziomu w obszarze **sieci**.

Gdy hello wymagania dla ruchu przychodzącego i wychodzącego są brane pod uwagę, hello grup NSG powinien wyglądać podobnie toohello grup NSG w poniższym przykładzie. Witaj zakres adresów sieci wirtualnej jest _192.168.250.0/16_, i jest hello podsieci, która jest hello ASE _192.168.251.128/25_.

Hello dwóch pierwszych przychodzących wymagania dotyczące hello ASE toofunction są wyświetlane u góry hello lista hello w tym przykładzie. Włącz zarządzanie ASE, a Zezwalaj toocommunicate ASE hello z samym sobą. Hello inne pozycje są wszystkie konfigurowalne dzierżawy i można kontrolować aplikacje hostowanej ASE toohello dostępu do sieci. 

![Reguły zabezpieczeń ruchu przychodzącego][4]

Domyślna reguła umożliwia hello adresów IP w hello sieci wirtualnej tootalk toohello ASE podsieci. Inna reguła domyślna umożliwia hello równoważenia obciążenia, nazywane również hello publicznego adresu VIP, toocommunicate z hello ASE. reguły domyślne hello toosee, wybierz **domyślne zasady** dalej toohello **Dodaj** ikony. Umieszczenie Odmów, wszystkie inne reguły po hello NSG zasady pokazano, uniemożliwia ruch między hello VIP i hello ASE. tooprevent ruchu przychodzącego z wewnątrz hello sieci wirtualnej, dodać własną tooallow reguły ruchu przychodzącego. Użyj tooAzureLoadBalancer równy źródła z docelowym **żadnych** i zakres portów  **\*** . Ponieważ reguły NSG hello jest stosowane toohello ASE podsieci, nie potrzebujesz toobe określonych w lokalizacji docelowej hello.

Po przypisaniu aplikacji tooyour adres IP, upewnij się, że zachowasz hello otwartych portów. Wybierz toosee hello portów, **środowiska usługi aplikacji** > **adresów IP**.  

Wszystkie elementy hello pokazano hello następujące reguły wychodzące są potrzebne, z wyjątkiem ostatniego elementu hello. Umożliwiają one zależności ASE toohello dostępu do sieci, które zostały wymienione w tym artykule. Jeśli zablokujesz ich z ASE przestanie działać. Witaj ostatniego elementu na liście hello umożliwia toocommunicate Twojego ASE z innymi zasobami w sieci wirtualnej.

![Zasady zabezpieczeń dla ruchu wychodzącego][5]

Po zdefiniowaniu grup NSG, przypisz toohello podsieci, która jest Twoje ASE na. Jeśli nie pamiętasz hello ASE sieci wirtualnej lub podsieci, można to sprawdzić w portalu zarządzania ASE hello. tooassign hello podsieci tooyour NSG, przejdź toohello podsieci interfejsu użytkownika i wybierz hello NSG.

## <a name="routes"></a>Trasy ##

Trasy stanie najczęściej powodować problemy podczas konfigurowania sieci wirtualnej z platformy Azure ExpressRoute. Istnieją trzy typy tras w sieci wirtualnej:

-   Trasy systemowe
-   Trasy protokołu BGP
-   Trasy zdefiniowane przez użytkownika (Udr)

Trasy protokołu BGP musi zostać zastąpiona tras systemowych. Udr zastąpić trasy protokołu BGP. Aby uzyskać więcej informacji dotyczących tras w sieci wirtualnych platformy Azure, zobacz [trasy zdefiniowane przez użytkownika — omówienie][UDRs].

Baza danych Azure SQL Hello hello ASE używany toomanage hello system ma zapory. Wymaga to toooriginate komunikacji z hello ASE publicznego adresu VIP. Baza danych SQL toohello połączeń z hello ASE będą odrzucane, jeśli są one wysyłane w dół hello połączenia ExpressRoute i innego adresu IP.

Jeśli żądań zarządzania tooincoming odpowiedzi są wysyłane w dół hello ExpressRoute, adres zwrotny hello jest inny niż hello początkowego miejsca docelowego. Ta niezgodność dzieli hello TCP komunikacji.

Dla Twojego toowork ASE sieci wirtualnej jest konfigurowana ExpressRoute najprostszym toodo operacją hello jest:

-   Konfigurowanie usługi ExpressRoute tooadvertise _0.0.0.0/0_. Domyślnie go wymusić tuneli wszystkie wychodzący ruch lokalnymi.
-   Utwórz przez. Zastosować toohello podsieci, która zawiera ASE hello z prefiksem adresu o _0.0.0.0/0_ i następnego przeskoku typu _Internet_.

Jeśli te dwie zmiany, ruch kierowany przez internet pochodzący z hello ASE podsieci nie jest wymuszone hello ExpressRoute i hello ASE działa. 

> [!IMPORTANT]
> Hello tras określonych w przez musi być wystarczająco konkretny tootake pierwszeństwo za pośrednictwem żadnych trasy anonsowane przez hello konfiguracji usługi ExpressRoute. Witaj poprzedniego przykładu używa hello szerokie 0.0.0.0/0 adres zakresu. Go może potencjalnie być przypadkowo zastąpione anonsów tras, korzystających z bardziej szczegółowych zakresów adresów.
>
> ASEs nie są obsługiwane w przypadku konfiguracji usługi ExpressRoute, które między anonsować tras z hello publicznej komunikacji równorzędnej ścieżki toohello prywatnej komunikacji równorzędnej ścieżki. Konfiguracji usługi ExpressRoute z publicznej komunikacji równorzędnej skonfigurowane otrzymywać anonsów tras od firmy Microsoft. anonse Hello zawiera duży zbiór zakresów adresów IP firmy Microsoft Azure. Jeśli między anonsowane w ścieżce prywatnej komunikacji równorzędnej hello hello zakresów adresów, wszystkie pakiety wychodzącego z podsieci hello ASE na są infrastruktury sieci lokalnej klienta tunelowane tooa force. Ten przepływ sieci nie jest obecnie obsługiwane z ASEs. Rozwiązanie toothis problemem jest toostop tras między reklamy hello publicznej komunikacji równorzędnej ścieżka toohello prywatnej komunikacji równorzędnej ścieżka.

toocreate przez, wykonaj następujące kroki:

1. Przejdź toohello portalu Azure. Wybierz **sieci** > **tabel tras**.

2. Utwórz nową tabelę tras hello — w tym samym regionie co sieci wirtualnej.

3. W tabeli routingu interfejsu użytkownika, zaznacz **tras** > **Dodaj**.

4. Zestaw hello **następnego przeskoku typu** za**Internet** i hello **prefiks adresu** za**0.0.0.0/0**. Wybierz pozycję **Zapisz**.

    Zostanie wyświetlony ekran podobny do następujących hello:

    ![Trasy funkcjonalności][6]

5. Po utworzeniu nowej tabeli tras hello Przejdź toohello podsieci, która zawiera ASE użytkownika. Wybierz z tabeli tras z listy hello w portalu hello. Po zapisaniu zmian hello należy następnie zobacz grupy NSG hello i oznaczane przy użyciu podsieci trasy.

    ![Tras i grupy NSG][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Wdróż do istniejącej sieci wirtualnych platformy Azure zintegrowanych z usługi ExpressRoute ###

toodeploy Twojego ASE w sieci wirtualnej, który jest zintegrowany z usługi ExpressRoute, należy wstępnie skonfigurować podsieci hello miejscu ASE hello wdrożone. Następnie użyj toodeploy szablonu usługi Resource Manager go. toocreate ASE w sieci wirtualnej ma już ExpressRoute skonfigurowane:

- Utwórz podsieć toohost hello ASE.

    > [!NOTE]
    > Nic znajdować się w podsieci hello, ale hello ASE. Można toochoose się na przestrzeń adresową, która umożliwia rozwój w przyszłości. Nie można zmienić tego ustawienia później. Firma Microsoft zaleca rozmiar `/25` z adresami 128.

- Tworzenie Udr (na przykład, tabele tras), jak opisano wcześniej i ustawić go na powitania podsieci.
- Tworzenie hello ASE przy użyciu szablonu usługi Resource Manager, zgodnie z opisem w [utworzyć ASE przy użyciu szablonu usługi Resource Manager][MakeASEfromTemplate].

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
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
