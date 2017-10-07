---
title: "aaaCreate środowiska usługi aplikacji Azure zewnętrznych"
description: "Wyjaśniono, jak toocreate środowiska usługi aplikacji, podczas tworzenia aplikacji lub autonomiczne"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Tworzenie środowiska usługi aplikacji zewnętrznych #

Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet). Istnieją dwa sposoby toodeploy środowiska usługi App Service (ASE):

- Z adresów VIP na zewnętrzny adres IP często nazywane ASE zewnętrznych.
- Z hello VIP wewnętrznego adresu IP często nazywane ASE ILB, ponieważ hello wewnętrzny punkt końcowy jest wewnętrzny moduł równoważenia obciążenia (ILB).

W tym artykule opisano sposób toocreate ASE zewnętrznych. Omówienie hello ASE, zobacz [toohello wprowadzenie środowiska usługi aplikacji][Intro]. Aby uzyskać informacje dotyczące toocreate ILB ASE, zobacz temat [tworzenie i używanie ASE ILB][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Przed utworzeniem sieci ASE ##

Po utworzeniu sieci ASE, nie można zmienić następujących hello:

- Lokalizacja
- Subskrypcja
- Grupa zasobów
- Używane w sieci wirtualnej
- Podsieci używane
- Rozmiar podsieci

> [!NOTE]
> Po wybraniu sieci wirtualnej i określ podsieć, upewnij się, że jest wystarczająco duży tooaccommodate przyszłego rozwoju. Firma Microsoft zaleca rozmiar `/25` z adresami 128.
>

## <a name="three-ways-toocreate-an-ase"></a>Trzy sposoby toocreate ASE ##

Istnieją trzy sposoby toocreate ASE:

- **Podczas tworzenia planu usługi App Service**. Ta metoda tworzy hello ASE i hello planu usługi aplikacji w jednym kroku.
- **Jako akcję autonomiczny**. Ta metoda tworzy autonomiczny ASE, czyli ASE pustą. Ta metoda jest bardziej zaawansowanych toocreate procesu ASE. Używany toocreate ASE z ILB.
- **Za pomocą szablonu usługi Azure Resource Manager**. Ta metoda jest dla użytkowników zaawansowanych. Aby uzyskać więcej informacji, zobacz [utworzyć ASE na podstawie szablonu][MakeASEfromTemplate].

Zewnętrzne ASE ma publiczny adres VIP, co oznacza, że wszystkie aplikacje toohello ruchu HTTP/HTTPS w hello ASE trafienia internet dostępny adres IP. ASE z ILB ma adres IP z podsieci hello używane przez hello ASE. Witaj aplikacji hostowanych w elemencie ASE ILB nie są udostępniane bezpośrednio toohello internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Utwórz razem ASE i plan usługi aplikacji ##

Witaj planu usługi aplikacji to kontener aplikacji. Po utworzeniu aplikacji w usłudze App Service wybierz lub Utwórz plan usługi aplikacji. Hello kontenera modelu środowisk przytrzymaj planów usługi App Service i planów usługi App Service przechowywania aplikacji.

toocreate ASE podczas tworzenia planu usługi aplikacji:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz pozycję **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.

    ![Tworzenie aplikacji sieci Web][1]

2. Wybierz subskrypcję. Aplikacja Hello i hello ASE są tworzone w hello sam subskrypcji.

3. Wybierz lub utwórz grupę zasobów. Z grupami zasobów można zarządzać jako jednostka powiązanych zasobów systemu Azure. Grupy zasobów są także przydatne podczas ustanawiania zasady kontroli dostępu opartej na rolach dla aplikacji. Aby uzyskać więcej informacji, zobacz hello [Omówienie usługi Azure Resource Manager][ARMOverview].

4. Wybierz hello planu usług aplikacji, a następnie wybierz **Utwórz nowy**.

    ![Nowy plan usługi aplikacji][2]

5. W hello **lokalizacji** listy rozwijanej, region hello wybierz miejsce toocreate hello ASE. W przypadku wybrania istniejącego ASE nowe ASE nie jest tworzone. plan usługi aplikacji Hello jest tworzony w hello ASE wybrany. 

6. Wybierz **warstwa cenowa**i wybierz jedną z hello **izolowany** cennik jednostki SKU. Jeśli wybierzesz **izolowany** karty jednostki SKU i lokalizacji, która nie jest ASE nowe ASE jest tworzony w tej lokalizacji. Wybierz toostart hello procesu toocreate ASE **wybierz**. Witaj **izolowany** jednostka SKU jest dostępna tylko w połączeniu z ASE. Również nie można użyć innych SKU cenową w elemencie ASE innych niż **izolowany**.

    ![Wybór warstwy cenowej][3]

7. Wprowadź nazwę użytkownika ASE hello. Ta nazwa jest używana w nazwie adresowanego powitania dla aplikacji. Jeśli nazwa hello hello ASE jest _appsvcenvdemo_, nazwa domeny hello jest *. appsvcenvdemo.p.azurewebsites.net*. Jeśli tworzysz aplikację o nazwie *mytestapp*, jest adresowanego na mytestapp.appsvcenvdemo.p.azurewebsites.net. Nie można użyć biały znak w nazwie hello. Jeśli używasz wielkich liter, hello nazwy domeny jest hello całkowita małe litery wersja tej nazwy.

    ![Nowa nazwa planu usługi aplikacji][4]

8. Określ szczegóły sieci wirtualnej platformy Azure. Wybierz opcję **tworzenia nowych** lub **wybierz istniejącą**. tooselect opcja Hello istniejącej sieci wirtualnej jest dostępna tylko wtedy, gdy sieć wirtualną w wybranym regionie hello. W przypadku wybrania **Utwórz nowy**, wprowadź nazwę hello sieci wirtualnej. Utworzono nową sieć wirtualną Menedżera zasobów o tej nazwie. Używa przestrzeni adresowej hello `192.168.250.0/23` w wybranym regionie hello. W przypadku wybrania **wybierz istniejącą**, musisz:

    a. Wybierz hello blok adresów sieci wirtualnej, jeśli masz więcej niż jeden.

    b. Wprowadź nazwę nowej podsieci.

    c. Wybierz rozmiar hello hello podsieci. *Należy pamiętać, tooselect rozmiar tooaccommodate wystarczająco duży przyszłego rozwoju Twojej ASE.* Firma Microsoft zaleca `/25`, który 128 adresów i może obsłużyć ASE rozmiar maksymalny. Nie zaleca się `/28`, na przykład tylko 16 adresów nie są dostępne. Infrastruktura używa co najmniej pięć adresów. W `/28` podsieci, w przypadku pozostałych z maksymalną skalowanie 11 wystąpień.

    d. Wybierz zakres adresów IP podsieci hello.

9. Wybierz **Utwórz** toocreate hello ASE. Ten proces tworzy również planu usługi aplikacji hello i aplikacja hello. Witaj ASE, planu usługi aplikacji i aplikacji są pod hello tej samej subskrypcji, a także w hello sam grupy zasobów. Twoje ASE wymaga oddzielnej grupie zasobów lub należy ASE ILB, wykonaj toocreate kroki hello ASE samodzielnie.

## <a name="create-an-ase-by-itself"></a>Utwórz ASE samodzielnie ##

Tworzenie autonomicznych ASE, nie ma nic w nim. Pusty ASE nadal wiąże miesięcznych opłat za infrastrukturę hello. Wykonaj te kroki toocreate ASE z ILB lub toocreate ASE w jego własnej grupy zasobów. Po utworzeniu sieci ASE mogą tworzyć aplikacje w nim przy użyciu standardowego procesu hello. Wybierz Twoje nowe ASE hello lokalizacji.

1. Wyszukiwanie hello Azure Marketplace w celu **środowiska usługi aplikacji**, lub wybierz **nowy** > **Web Mobile** > **usługi aplikacji Środowisko**. 

2. Wprowadź nazwę użytkownika ASE hello. Ta nazwa jest używana w przypadku aplikacji hello utworzone w hello ASE. Jeśli nazwa hello jest *mynewdemoase*, Nazwa poddomeny hello jest *. mynewdemoase.p.azurewebsites.net*. Jeśli tworzysz aplikację o nazwie *mytestapp*, jest adresowanego na mytestapp.mynewdemoase.p.azurewebsites.net. Nie można użyć biały znak w nazwie hello. Użycie wielkich liter, nazwy domeny hello jest hello całkowita małe litery wersja hello nazwy. Jeśli używasz ILB, nazwę ASE nie jest używana w Twojej domeny podrzędnej, ale zamiast tego jest jasno określone podczas tworzenia ASE.

    ![Nazewnictwo ASE][5]

3. Wybierz subskrypcję. Ta subskrypcja jest również hello, który wszystkie aplikacje w hello ASE używać. Twoje ASE nie można umieścić w sieci wirtualnej, który znajduje się w innej subskrypcji.

4. Wybierz lub określ nową grupę zasobów. Grupa zasobów Hello używane dla sieci ASE musi być hello tego samego jedną, która jest używana w sieci wirtualnej. W przypadku wybrania istniejącej sieci wirtualnej hello wybranej grupy zasobów dla Twojego ASE jest zaktualizowane tooreflect z sieci wirtualnej. *Możesz utworzyć ASE z grupą zasobów, która różni się od grupy zasobów hello sieci wirtualnej, jeśli używasz szablonu usługi Resource Manager.* toocreate ASE z szablonu, zobacz [tworzenie środowiska usługi aplikacji na podstawie szablonu][MakeASEfromTemplate].

    ![Wybór grupy zasobów][6]

5. Wybierz sieć wirtualną i lokalizacji. Możesz utworzyć nową sieć wirtualną lub wybierz istniejącej sieci wirtualnej: 

    * W przypadku wybrania nowej sieci wirtualnej można określić nazwy i lokalizacji. Witaj nowej sieci wirtualnej ma 192.168.250.0/23 zakres adresów hello i podsieć o nazwie domyślnej. podsieci Hello jest zdefiniowany jako 192.168.250.0/24. Można wybrać tylko sieć wirtualną Menedżera zasobów. Witaj **typu VIP** wybór określa, czy Twoje ASE są bezpośrednio dostępne z hello internet (zewnętrzne) lub gdy jest używana funkcja ILB. toolearn więcej informacji na temat tych opcji, zobacz [tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji][MakeILBASE]. 

      * W przypadku wybrania **zewnętrznych** dla hello **typu VIP**, można wybrać, ile zewnętrzny system hello adresów IP jest tworzony z celów opartych na protokole SSL. 
    
      * W przypadku wybrania **wewnętrzne** dla hello **typu VIP**, należy określić domeny hello, który korzysta z ASE. ASE można wdrożyć w sieci wirtualnej, które są używane zakresy adresów publicznych lub prywatnych. toouse sieci wirtualnej z zakresem adresów publicznych, należy toocreate hello sieci wirtualnej wcześniejsze. 
    
    * W przypadku wybrania istniejącej sieci wirtualnej nowa podsieć jest tworzony podczas tworzenia hello ASE. *Nie można użyć podsieci wstępnie utworzone w portalu hello. Jeśli używasz szablonu usługi Resource Manager, możesz utworzyć ASE się na istniejącą podsieć.* toocreate ASE z szablonu, zobacz [tworzenie środowiska usługi aplikacji na podstawie szablonu][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>Środowisko usługi App Service — wersja 1 ##

Można tworzyć wystąpień hello pierwszej wersji środowiska usługi aplikacji (ASEv1). toostart przetwarzające, wyszukiwania hello Marketplace dla **v1 środowiska usługi aplikacji**. Utwórz hello ASE w hello utworzenie ASE autonomiczny hello tak samo. Po zakończeniu Twojej ASEv1 ma dwa końce front i dwóch pracowników. Z ASEv1 możesz zarządzać hello front kończy się i pracowników. Są one automatycznie dodane, podczas tworzenia planów usługi aplikacji. Hello front kończy działanie jako punktów końcowych HTTP/HTTPS hello i wysyłania ruchu toohello pracowników. Pracownicy Hello są hello ról, które hosta aplikacji. Po utworzeniu sieci ASE, można dostosować ilość hello interfejsy i pracowników. 

toolearn więcej informacji na temat ASEv1, zobacz [toohello wprowadzenie v1 środowiska usługi aplikacji][ASEv1Intro]. Aby uzyskać więcej informacji na temat skalowania, zarządzanie i monitorowanie ASEv1, zobacz [jak tooconfigure środowiska usługi aplikacji][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



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
