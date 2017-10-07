---
title: "aaaAzure pakiet IoT — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące Pakietu IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Często zadawane pytania dotyczące Pakietu IoT

Zobacz też określonych połączonych fabryki hello [— często zadawane pytania](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Gdzie znaleźć kodu źródłowego hello hello wstępnie rozwiązań?

Kod źródłowy Hello są przechowywane w powitania po repozytoriów GitHub:
* [Zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-remote-monitoring-github]
* [Rozwiązanie do konserwacji predykcyjnej wstępnie][lnk-predictive-maintenance-github]
* [Fabryka połączonych wstępnie skonfigurowane rozwiązanie](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Jak zaktualizować toohello najnowszą wersję hello zdalnego monitorowania wstępnie skonfigurowane rozwiązanie czy używa hello funkcje zarządzania urządzeniami Centrum IoT?

* Jeśli wdrożono wstępnie skonfigurowane rozwiązanie z witryny https://www.azureiotsuite.com/ hello zawsze wdraża nowe wystąpienie klasy hello najnowsza wersja rozwiązania hello.
* W przypadku wdrożenia przy użyciu wiersza polecenia hello wstępnie skonfigurowane rozwiązanie, należy zaktualizować istniejące wdrożenie o nowy kod. Zobacz [wdrożenie w chmurze] [ lnk-cloud-deployment] w hello GitHub [repozytorium][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Jak dodać obsługę nowych toohello — metoda urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie?

Zobacz sekcję hello [obsługę nowych symulatora toohello — metoda] [ lnk-add-method] w hello [dostosować wstępnie skonfigurowane rozwiązanie] [ lnk-customize] artykułu.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>Symulowane urządzenie Hello ignoruje zmiany żądanej właściwości, dlaczego?
W hello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie, hello symulowane urządzenie kod używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** żądanego właściwości Witaj tooupdate zgłosił właściwości. Wszystkie inne żądanej właściwości żądania zmiany są ignorowane.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Urządzenie nie ma hello listy urządzeń na pulpicie nawigacyjnym rozwiązania hello, dlaczego?

Witaj listy urządzeń na pulpicie nawigacyjnym rozwiązania hello używa zapytania tooreturn hello listę urządzeń. Obecnie kwerendy nie może zwrócić więcej niż 10 tys urządzeń. Spróbuj bardziej restrykcyjne hello kryteria wyszukiwania dla zapytania.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Jaka jest różnica hello usunięcie grupy zasobów w hello Azure portalu i klikając przycisk Usuń na wstępnie skonfigurowane rozwiązanie w azureiotsuite.com?

* Jeśli usuniesz hello wstępnie skonfigurowane rozwiązanie w [azureiotsuite.com][lnk-azureiotsuite], należy usunąć wszystkie zasoby hello, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie. Jeśli dodano grupę zasobów toohello dodatkowe zasoby, te zasoby są także usuwane. 
* Usunięcie grupy zasobów hello w hello [portalu Azure][lnk-azure-portal], zostaną usunięte tylko hello zasobów w danej grupie zasobów. Należy również aplikacji usługi Azure Active Directory hello toodelete skojarzonej z hello wstępnie skonfigurowane rozwiązanie w hello [klasycznego portalu Azure][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Jak wiele wystąpień Centrum IoT można udostępnić w ramach subskrypcji?

Domyślnie można udostępnić [10 centra IoT na subskrypcję][link-azuresublimits]. Można utworzyć [biletu pomocy technicznej platformy Azure] [ link-azuresupportticket] tooraise ten limit. W rezultacie od każdego przepisy wstępnie skonfigurowane rozwiązanie z nowym Centrum IoT można tylko należy się too10 wstępnie rozwiązań w ramach danej subskrypcji. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Jak wiele wystąpień bazy danych Azure rozwiązania Cosmos można udostępnić w ramach subskrypcji?

50. Można utworzyć [biletu pomocy technicznej platformy Azure] [ link-azuresupportticket] tooraise to ograniczenie, ale domyślnie umożliwia tylko obsługę 50 wystąpień rozwiązania Cosmos bazy danych na subskrypcję. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Ile bezpłatnych interfejsów API usługi Mapy Bing można aprowizować w ramach subskrypcji?

Dwa. W subskrypcji platformy Azure można utworzyć tylko dwa wewnętrzne transakcje poziom 1 mapy Bing dla planów organizacji. rozwiązanie monitorowania zdalnego Hello jest udostępniana domyślnie z planem hello wewnętrzny poziom 1 transakcji. W związku z tym umożliwia tylko obsługę tootwo zdalnego monitorowanie rozwiązań w ramach subskrypcji, bez żadnych modyfikacji.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Mam wdrożone rozwiązanie do monitorowania zdalnego z mapą statyczną. Jak dodać interaktywną mapę Bing?

1. Pobierz interfejsu API map Bing dla QueryKey przedsiębiorstwa z [portalu Azure][lnk-azure-portal]: 
   
   1. Przejdź toohello grupy zasobów, w przypadku interfejsu API map Bing dla przedsiębiorstwa hello [portalu Azure][lnk-azure-portal].
   2. Kliknij przycisk **wszystkie ustawienia**, następnie **zarządzanie kluczami**. 
   3. Można zobaczyć dwa klucze: **umożliwia** i **QueryKey**. Skopiuj wartość hello **QueryKey**.
      
      > [!NOTE]
      > Nie masz konta interfejsu API usługi Mapy Bing dla przedsiębiorstw? Utworzyć w hello [portalu Azure] [ lnk-azure-portal] klikając + nowe wyszukiwanie interfejsu API map Bing dla przedsiębiorstwa i wykonaj monituje toocreate.
      > 
      > 
2. Rozwiń hello najnowsze kod z hello [Azure IoT — zdalnego-monitorowania][lnk-remote-monitoring-github].
3. Uruchom lokalnie lub w chmurze po hello dotyczące wdrażania wiersza polecenia w folderze /docs/ hello w repozytorium hello wdrożenia. 
4. Po uruchomiono na komputerze lokalnym lub w chmurze, wdrażania, poszukać w folderze głównym dla hello *. plików user.config utworzonych podczas wdrażania. Otwórz ten plik w edytorze tekstu. 
5. Zmień hello następująca linia wartość hello tooinclude skopiowany z Twojej **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>Czy można utworzyć wstępnie skonfigurowane rozwiązanie w przypadku korzystania z platformy Microsoft Azure dla programu DreamSpark?

Obecnie nie można utworzyć wstępnie skonfigurowane rozwiązanie o [Microsoft Azure dla programu DreamSpark] [ lnk-dreamspark] konta. Można jednak utworzyć [bezpłatnego konta wersji próbnej platformy Azure] [ lnk-30daytrial] w zaledwie kilka minut, umożliwiająca tworzenie wstępnie skonfigurowanego rozwiązania.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Jeśli subskrypcja Cloud Solution Provider (CSP) można utworzyć wstępnie skonfigurowane rozwiązanie?

Obecnie nie można utworzyć wstępnie skonfigurowane rozwiązanie z subskrypcją Cloud Solution Provider (CSP). Można jednak utworzyć [bezpłatnego konta wersji próbnej platformy Azure] [ lnk-30daytrial] w zaledwie kilka minut, umożliwiająca tworzenie wstępnie skonfigurowanego rozwiązania.

### <a name="how-do-i-delete-an-aad-tenant"></a>Jak usunąć dzierżawę usługi AAD?

Zobacz Golpe marek blogu [wskazówki usunięcia dzierżawy usługi Azure AD][lnk-delete-aad-tennant].

### <a name="next-steps"></a>Następne kroki

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]
* [Fabryka połączonych wstępnie Omówienie rozwiązania](iot-suite-connected-factory-overview.md)
* [Zabezpieczenia IoT z hello tła w][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
