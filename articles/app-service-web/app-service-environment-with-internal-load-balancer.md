---
title: "aaaCreating i przy użyciu wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji | Dokumentacja firmy Microsoft"
description: Tworzenie i korzystanie z ILB ASE
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Przy użyciu wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji

> [!NOTE] 
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji. Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
>

Hello funkcji środowiska usługi aplikacji (ASE) to opcja usługi Premium usługi Azure App Service oferuje możliwość rozszerzonej konfiguracji, która nie jest dostępna w hello wielodostępne sygnatury. Funkcja ASE Hello wdraża zasadniczo hello Azure App Service w Twojej Network(VNet) wirtualnych Azure. toogain lepsze zrozumienie hello możliwości oferowane przez środowiska usługi App Service odczytu hello [co to jest środowisko usługi aplikacji] [ WhatisASE] dokumentacji. Jeśli nie znasz korzyści hello systemu operacyjnego w sieci wirtualnej odczytu hello [często zadawane pytania sieci wirtualnych Azure][virtualnetwork]. 

## <a name="overview"></a>Omówienie
ASE można wdrożyć z dostępnym punkcie końcowym internet lub z adresu IP w sieci wirtualnej. W kolejności tooset hello IP address tooa adresów sieci wirtualnej należy toodeploy Twojego ASE z wewnętrznego Balancer(ILB) obciążenia. Po skonfigurowaniu sieci ASE ILB zawierają:

* własnych domeny lub poddomeny. toomake go łatwo, w tym dokumencie przyjęto założenie domeny podrzędnej, ale można go skonfigurować w obu przypadkach. 
* Witaj certyfikatu używanego na potrzeby protokołu HTTPS
* Zarządzanie systemem DNS z domeny podrzędnej. 

W zamian można wykonać czynności takich jak:

* hosta aplikacji intranetowych, takich jak aplikacje biznesowe, bezpiecznie na powitania w chmurze, które dostęp za pośrednictwem witryny tooSite lub sieci VPN usługi ExpressRoute
* aplikacje hosta w chmurze hello, które nie są wymienione w publicznych serwerów DNS
* Tworzenie aplikacji zaplecza internet samodzielnie, których fronton aplikacji bezpiecznego można zintegrować z

#### <a name="disabled-functionality"></a>Funkcje wyłączone
Istnieje kilka kwestii, które nie można wykonać przy użyciu ASE ILB. Czynności te obejmują:

* przy użyciu IPSSL
* Przypisywanie adresów IP toospecific aplikacji
* kupowanie i z aplikacji za pośrednictwem portalu hello przy użyciu certyfikatu. Oczywiście nadal można uzyskać certyfikatów bezpośrednio z urzędu certyfikacji i używać go z aplikacji, nie za pośrednictwem hello portalu Azure.

## <a name="creating-an-ilb-ase"></a>Tworzenie ILB ASE
Tworzenie ASE ILB nie jest znacznie różni się od tworzenia ASE normalnie. Omówienie więcej danych na temat tworzenia ASE odczytu [jak tooCreate środowiska usługi aplikacji][HowtoCreateASE]. Hello toocreate procesu, który ASE ILB jest hello między różnymi tworzenia sieci wirtualnej podczas tworzenia ASE lub wybierz istniejące sieci wirtualnej. toocreate ASE ILB: 

1. W hello Azure wybierz portalu **nowy -> sieci Web i mobilność -> środowisko usługi aplikacji**
2. Wybierz subskrypcję
3. Wybierz lub Utwórz grupę zasobów
4. Wybierz lub Utwórz sieć wirtualną
5. Utwórz podsieć, w przypadku wybrania sieci wirtualnej
6. Wybierz **wirtualnego lokalizacji-> Konfiguracja sieci wirtualnej** i zestaw hello tooInternal typu VIP
7. Podaj nazwę domeny podrzędnej (będzie używany dla aplikacji utworzone w tym ASE poddomeny hello)
8. Wybierz przycisk Ok, a następnie utwórz

![][1]

W bloku sieci wirtualnej hello jest opcja Konfiguracja sieci wirtualnej. Pozwala to wybrać między zewnętrznego adresu VIP lub wewnętrznego adresu VIP. Domyślnie Hello jest zewnętrzny. Jeśli trzeba ustawić tooExternal Twojego ASE użyje internet dostępne wirtualne adresy IP. W przypadku wybrania wewnętrzne Twojej ASE zostaną skonfigurowane ILB na adres IP w sieci wirtualnej. 

Po wybraniu wewnętrzne, hello tooadd możliwości więcej adresów IP tooyour ASE jest usunięte i zamiast tego należy tooprovide poddomeną hello hello ASE. W elemencie ASE z hello zewnętrznych adresów VIP nazwa hello ASE jest używany w poddomenie hello aplikacje utworzone w tym ASE. Jeśli została wywołana z ASE ***contosotest*** i aplikacji w tym ASE została wywołana ***test*** , a następnie będzie poddomeny hello formatu hello ***contosotest.p.azurewebsites.net*** i Witaj adres URL dla tej aplikacji będą ***mytest.contosotest.p.azurewebsites.net***. Jeśli ustawisz hello tooInternal typu VIP nazwę ASE nie jest używany podczas hello poddomeny dla hello ASE. Poddomeny hello są jawnie określić. Jeśli Twoje domeny podrzędnej ***contoso.corp.net*** i wprowadzone aplikacji, w tym o nazwie ASE ***timereporting*** następnie hello adres URL dla tej aplikacji może być ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Aplikacje w elemencie ASE ILB
Tworzenie aplikacji w elemencie ASE ILB jest hello jak w przypadku tworzenia aplikacji w elemencie ASE normalnie. 

1. W hello Azure wybierz portalu **nowy -> sieci Web i mobilność -> sieci Web** lub **Mobile** lub **aplikacji interfejsu API**
2. Wprowadź nazwę aplikacji
3. Wybieranie subskrypcji
4. Wybierz lub Utwórz grupę zasobów
5. Wybierz lub Utwórz Plan(ASP) usługi aplikacji. Jeśli następnie tworzenie nowych stron ASP Twojej ASE jako lokalizacji hello i wybierz hello puli procesów roboczych ma Twojej toobe ASP utworzone w. Po utworzeniu hello ASP należy wybrać Twojej ASE jako lokalizacji hello i hello puli procesów roboczych. Po określeniu hello nazwę tworzonej aplikacji hello zobaczysz tego poddomeny hello w obszarze nazwy aplikacji zastępuje hello poddomeny dla Twojego ASE. 
6. Wybierz opcję Utwórz. Należy wybrać hello **toodashboard numeru Pin** pole wyboru, jeśli chcesz tooshow aplikacji hello się na pulpicie nawigacyjnym. 

![][2]

W obszarze aplikacji hello nazwy poddomeny hello pobiera poddomeną hello zaktualizowane tooreflect Twojego ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Sprawdzanie poprawności tworzenia ILB ASE POST
ASE ILB są nieco inne niż hello nie - ILB ASE. Jak już zauważyć należy toomanage własne DNS i ma również tooprovide swój własny certyfikat dla połączeń HTTPS. 

Po utworzeniu sieci ASE można zauważyć, że poddomeny hello pokazuje poddomeny hello określono oraz w hello znajduje się nowy element **ustawienie** menu o nazwie **certyfikatu ILB**. Witaj ASE jest tworzony z certyfikatu z podpisem własnym, co pozwala na łatwiejsze tootest HTTPS. Witaj portalu informuje o należy tooprovide swój własny certyfikat dla protokołu HTTPS, ale jest to toodrive toohave certyfikatu, który łączy się z Twojej domeny podrzędnej. 

![][3]

Jeśli są po prostu testuje rzeczy, a nie wiadomo, jak toocreate certyfikat służy hello MMC programu IIS toocreate aplikacji konsoli, a własny certyfikat z podpisem. Po jego utworzeniu należy go wyeksportować w postaci pliku PFX, a następnie przekaż w hello interfejsu ILB certyfikatu użytkownika. Gdy dostępu lokacji zabezpieczone przy użyciu certyfikatu z podpisem własnym, przeglądarka będzie przekazywać ostrzeżenie, że hello lokacji, które uzyskują dostęp do nie jest zabezpieczony powodu toohello brakiem toovalidate hello certyfikatu. Jeśli chcesz tooavoid tego ostrzeżenia, należy poprawnie podpisane certyfikat, który jest zgodny z poddomeny i ma łańcuch zaufania, który jest rozpoznawany przez przeglądarkę.

![][6]

Jeśli chcesz tootry hello przepływ z własnych certyfikatów i testowanie protokołów HTTP i HTTPS ASE tooyour dostępu:

1. Po utworzeniu ASE Przejdź tooASE interfejsu użytkownika **ASE -> Ustawienia -> ILB certyfikatów**
2. Określ certyfikat ILB, wybierając plik pfx certyfikatu i podaj hasło. Ten krok zajmuje trochę podczas tooprocess i wiadomość hello, która jest wykonywana operacja skalowania będzie widoczny.
3. Pobierz adres ILB powitania dla Twojego ASE (**ASE -> Właściwości -> wirtualnego adresu IP**)
4. Tworzenie aplikacji sieci web w ASE po utworzeniu 
5. Tworzenie maszyny Wirtualnej, jeśli nie istnieje w tej sieci Wirtualnej (nie w hello same podsieci co hello ASE lub podziału rzeczy)
6. Ustaw DNS z domeny podrzędnej. Można użyć symbolu wieloznacznego z Twojej domeny podrzędnej w systemie DNS lub toodo proste testy, Edycja pliku hosts hello na maszyna wirtualna tooset sieci web app name tooVIP adresu IP. Jeśli Twoje ASE ma nazwę poddomeny hello. ilbase.com zostanie wykonane i hello mytestapp aplikacji sieci web tak, aby będzie na mytestapp.ilbase.com następnie ustawić go w pliku hostów. (W systemie Windows hello plik hosts znajduje się w C:\Windows\System32\drivers\etc\)
7. Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź toohttp://mytestapp.ilbase.com (lub niezależnie od nazwę aplikacji sieci web jest z Twojej domeny podrzędnej)
8. Korzystanie z przeglądarki na tej maszynie Wirtualnej i przejdź toohttps://mytestapp.ilbase.com trzeba tooaccept hello braku zabezpieczeń, jeśli przy użyciu certyfikatu z podpisem własnym. 

adres IP Twojego ILB Hello wymienionym we właściwościach hello wirtualnego adresu IP

![][4]

## <a name="using-an-ilb-ase"></a>Przy użyciu ILB ASE
#### <a name="network-security-groups"></a>Grupy zabezpieczeń sieci
Izolacja sieci umożliwia ILB ASE dla aplikacji hello aplikacje nie są dostępne lub nawet znane przez hello internet. Jest to doskonały dla hostingu witryn intranetowych, takich jak aplikacje biznesowe. Jeśli potrzebujesz dostępu toorestrict nawet dalsze nadal służy dostępu toocontrol Groups(NSGs) zabezpieczeń sieci na poziomie sieci hello. 

W razie potrzeby toofurther grup NSG toouse ograniczenia dostępu, a następnie należy toomake się, że nie przerwanie komunikacji hello tego ASE hello musi w kolejności toooperate. Nawet jeśli jest hello HTTP/HTTPS dostęp tylko za pośrednictwem hello ILB używany przez hello powitalne ASE ASE nadal zależy od zasobu poza hello sieci wirtualnej. toosee, jaki dostęp do sieci jest wymagana przeglądania informacji hello w dokumencie hello na [tooan kontrolowanie ruch przychodzący środowiska usługi aplikacji] [ ControlInbound] i zarządzania dokumentami hello na [sieci Szczegóły konfiguracji środowiska usługi aplikacji z usługi ExpressRoute][ExpressRoute]. 

tooconfigure, który NSG należy tooknow hello IP adresu, który ma używany przez Azure toomanage Twojego ASE. Ten adres IP jest również hello wychodzący adres IP z sieci ASE, jeśli żądania internetowe. Hello wychodzący adres IP dla sieci ASE pozostanie statyczny dla hello użytkowania Twojej ASE. Jeśli Usuń i Utwórz ponownie Twoje ASE, otrzymasz nowy adres IP. toofind ten adres IP Przejdź zbyt**Ustawienia -> właściwości** i Znajdź hello **wychodzący adres IP**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Zarządzanie ogólne ILB ASE
Zarządzanie ASE ILB przede wszystkim jest hello taki sam jak zarządzanie ASE normalnie. Należy się z toohost pule procesu roboczego tooscale więcej wystąpień ASP i skalowanie w górę z frontonu serwerów toohandle zwiększenie ilości ruchu HTTP/HTTPS. Aby uzyskać ogólne informacje na temat zarządzania konfiguracją hello ASE odczytać dokument hello na [Konfigurowanie środowiska usługi aplikacji][ASEConfig]. 

elementy na dodatkowe Zarządzanie Hello są zarządzania certyfikatami i zarządzania DNS. Należy tooobtain i przekaż hello certyfikat używany do obsługi protokołu HTTPS, po utworzeniu ILB ASE i zastąp go przed jego wygaśnięciem. Ponieważ Azure jest właścicielem domeny podstawowej hello firma Microsoft może zapewnić certyfikaty dla ASEs z zewnętrznego adresu VIP. Ponieważ może to być dowolne hello poddomeny używane przez ASE ILB, należy tooprovide swój własny certyfikat dla protokołu HTTPS. 

#### <a name="dns-configuration"></a>Konfiguracja DNS
Jeśli przy użyciu zewnętrznego adresu VIP hello DNS jest zarządzana przez Azure. Wszystkich aplikacji utworzonych w Twojej ASE jest automatycznie dodawany tooAzure DNS, który jest publicznym systemie DNS. W elemencie ASE ILB masz toomanage własne DNS. Dla danej domeny podrzędnej, takich jak contoso.corp.net należy toocreate, którego ten adres ILB tooyour punktu rekordy A systemu DNS:

    * 
    publikowanie *.SCM ftp 


## <a name="getting-started"></a>Wprowadzenie
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi][WhatisASE]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
