---
title: "tooCreate aaaHow v1 środowiska usługi aplikacji"
description: "Tworzenie opisu przepływu v1 środowiska usługi aplikacji"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Jak tooCreate v1 środowiska usługi aplikacji 

> [!NOTE]
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji. Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Omówienie
Witaj środowiska usługi aplikacji (ASE) to opcja usługi Premium usługi Azure App Service oferuje możliwość rozszerzonej konfiguracji, która nie jest dostępna w hello wielodostępne sygnatury. Funkcja ASE Hello wdraża zasadniczo hello Azure App Service w sieci wirtualnej do klienta. toogain lepsze zrozumienie hello możliwości oferowane przez środowiska usługi App Service odczytu hello [co to jest środowisko usługi aplikacji] [ WhatisASE] dokumentacji.

### <a name="before-you-create-your-ase"></a>Przed utworzeniem sieci ASE
Jest ważne toobe uwagę hello rzeczy, o których nie można zmienić. Te aspekty, nie można zmienić o Twojej ASE po jego utworzeniu są:

* Lokalizacja
* Subskrypcja
* Grupa zasobów
* Używane w sieci wirtualnej
* Podsieci używane 
* Rozmiar podsieci

Podczas pobierania sieci wirtualnej i określania podsieci, sprawdzać, czy jest wystarczająco duży tooaccomodate przyszłego rozwoju. 

### <a name="creating-an-app-service-environment-v1"></a>Tworzenie aplikacji usługi v1 środowiska
toocreate v1 środowiska usługi aplikacji muszą toosearch hello Azure Marketplace w celu ***v1 środowiska usługi aplikacji***, lub za pośrednictwem nowy -> Sieć Web i mobilność -> środowisko usługi aplikacji. toocreate ASEv1:

1. Podaj nazwę użytkownika ASE hello. Nazwa Hello, określony dla hello ASE będzie używana dla aplikacji hello utworzone w hello ASE. Jeśli nazwa hello ASE jest appsvcenvdemo następnie nazwy poddomeny hello będzie. *appsvcenvdemo.p.azurewebsites.net*. Jeśli w związku z tym utworzono aplikację o nazwie *mytestapp* , a następnie byłoby adresowanego na *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Nie można użyć biały znak w nazwie hello Twojej ASE. Jeśli używasz wielkich liter w nazwie hello hello nazwy domeny będzie hello całkowita małe litery wersją tej nazwy. Jeśli używasz ILB to nazwę ASE nie jest używana w Twojej domeny podrzędnej, ale zamiast tego jest jasno określone podczas tworzenia ASE
   
    ![][1]
2. Wybierz subskrypcję. Subskrypcja Hello używana na potrzeby Twojego ASE jest również hello jedną wszystkie aplikacje w tym ASE zostanie utworzony z. Twoje ASE nie można umieścić w sieci wirtualnej, który znajduje się w innej subskrypcji
3. Wybierz lub określ nową grupę zasobów. grupy zasobów Hello używane dla sieci ASE musi być hello samo hasło, które jest używane dla sieci wirtualnej. Jeśli wybierz istniejące sieci wirtualnej, a następnie hello wybranej grupy zasobów dla Twojego ASE zostaną zaktualizowane tooreflect z sieci wirtualnej.
   
    ![][2]
4. Wybierz odpowiednie opcje sieci wirtualnej i lokalizacji. Można wybrać toocreate nowej sieci wirtualnej lub wybierz istniejące sieci wirtualnej. W przypadku wybrania nowej sieci wirtualnej, a następnie można określić nazwy i lokalizacji. Witaj nowej sieci wirtualnej mają 192.168.250.0/23 zakres adresów hello i podsieć o nazwie **domyślne** zdefiniowanej jako 192.168.250.0/24. Można także po prostu wybierz klasyczny istniejące lub Menedżera zasobów w sieci wirtualnej. Hello wybrany typ VIP Określa, czy Twoje ASE są bezpośrednio dostępne z hello internet (zewnętrzne) lub jeśli używa wewnętrznego modułu równoważenia obciążenia (ILB). więcej informacji na temat je odczytać toolearn [przy użyciu wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji][ILBASE]. W przypadku wybrania typu zewnętrznego adresu VIP, można wybrać, ile zewnętrzny system hello adresów IP jest tworzony z do celów IPSSL. W przypadku wybrania wewnętrznego należy poddomeny hello toospecify, który będzie używany przez Twoje ASE. ASEs można wdrożyć w sieci wirtualnych, które używają *albo* zakresy publicznych adresów, *lub* przestrzeni adresowych RFC1918 (czyli adresy prywatne). W kolejności toouse sieci wirtualnej z zakresem adresów publicznych konieczne będzie toocreate hello sieci wirtualnej wcześniejsze. Po wybraniu wstępnie istniejącej sieci wirtualnej należy toocreate nowej podsieci podczas tworzenia ASE. **Nie można użyć podsieci wstępnie utworzone w portalu hello. W przypadku utworzenia użytkownika ASE przy użyciu szablonu usługi resource manager, możesz utworzyć ASE z istniejącym podsieci.** toocreate ASE z szablonu miejscu użyć informacji hello [tworzenia środowiska usługi aplikacji na podstawie szablonu] [ ILBAseTemplate] i w tym miejscu [tworzenia środowiska usługi aplikacji ILB na podstawie szablonu] [ASEfromTemplate].

### <a name="details"></a>Szczegóły
ASE jest tworzony z 2 frontonu i 2 procesy robocze. frontonu Hello działać jako punktów końcowych HTTP/HTTPS hello i wysyłania ruchu toohello pracowników, które są hello ról, które Hostuj aplikacje sieci. Można dopasować ilość powitania po utworzeniu ASE i może nawet zestawu reguł skalowania automatycznego na tych pul zasobów. Więcej szczegółów wokół ręczne skalowanie, zarządzania i monitorowania środowiska usługi aplikacji w tym miejscu: [jak tooconfigure środowiska usługi aplikacji][ASEConfig] 

W podsieci hello używane przez hello ASE może istnieć tylko hello ASE jeden. Nie można użyć podsieci Hello do wszelkich innych niż hello ASE

### <a name="after-app-service-environment-v1-creation"></a>Po utworzeniu v1 środowiska usługi aplikacji
Po utworzeniu ASE można dostosować:

* Ilość frontonu (minimalna: 2)
* Liczba procesów roboczych (minimalna: 2)
* Liczba adresów IP dostępnych dla protokołu SSL z adresu IP
* Obliczeniowe rozmiary zasobów używanych przez hello frontonu lub pracowników (minimalny rozmiar fronton jest P2)

Brak więcej szczegółów dotyczących ręczne skalowania, zarządzania i monitorowania środowiska usługi App Service w tym miejscu: [jak tooconfigure środowiska usługi aplikacji][ASEConfig] 

Aby uzyskać informacje dotyczące skalowania automatycznego jest przewodnik tutaj: [jak tooconfigure funkcja automatycznego skalowania dla środowiska usługi aplikacji][ASEAutoscale]

Istnieją dodatkowe zależności, które nie są możliwe do dostosowania, takie jak hello bazy danych i magazynu. Są obsługiwane przez platformę Azure i wyposażone w hello system. obsługuje magazyn systemu Hello się too500 GB dla hello całego środowiska usługi aplikacji i hello bazy danych zostanie zmieniona przez platformę Azure, zgodnie z potrzebami Skala hello hello systemu.

## <a name="getting-started"></a>Wprowadzenie
Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

tooget wprowadzenie v1 środowiska usługi aplikacji, zobacz [toohello wprowadzenie v1 środowiska usługi aplikacji][WhatisASE]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
