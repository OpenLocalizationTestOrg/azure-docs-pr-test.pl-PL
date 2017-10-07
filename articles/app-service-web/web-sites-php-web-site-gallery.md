---
title: "aaaCreate aplikacji sieci web WordPress w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure nowej sieci web aplikacji dla bloga WordPress przy użyciu hello portalu Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Tworzenie aplikacji sieci Web WordPress w usłudze Azure App Service
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Ten samouczek pokazuje, jak toodeploy bloga WordPress lokacji z hello Azure Marketplace.

Po zakończeniu korzystania z samouczka hello będziesz mieć własne witrynę bloga WordPress i w chmurze hello.

![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Dowiesz się:

* Jak toofind szablonem aplikacji w hello Azure Marketplace.
* Jak toocreate aplikacji sieci web w aplikacji Azure usługi, który jest oparty na szablonie hello.
* Jak ustawienia usługi Azure App Service tooconfigure hello nowej sieci web, aplikacji i bazy danych.

Hello Azure Marketplace udostępnia szeroką gamę popularnych aplikacji sieci web opracowany przez firmę Microsoft, inne firmy i inicjatyw oprogramowania typu open source. aplikacje sieci web Hello są tworzone przy użyciu różnych popularnych platformach, takich jak [PHP](/develop/nodejs/) w tym przykładzie WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), i [Python](/develop/python/), tooname w kilku. toocreate aplikacji sieci web z portalu Azure Marketplace hello tylko oprogramowanie potrzebne jest hello przeglądarka, której używasz hello hello [Azure Portal](https://portal.azure.com/). 

Witaj witryna WordPress wdrażana w tym samouczku korzysta hello bazy danych MySQL. Jeśli chcesz, aby używany tooinstead bazy danych SQL z bazą danych hello, zobacz [Project Nami](http://projectnami.org/). **Project Nami** jest również dostępny za pośrednictwem hello Marketplace.

> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto Microsoft Azure. Jeśli nie masz konta, możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) lub [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/). W tej lokalizacji możesz od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service — bez karty kredytowej i bez zobowiązań.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Wybieranie platformy WordPress i konfigurowanie dla usługi Azure App Service
1. Zaloguj się za toohello [Azure Portal](https://portal.azure.com/).
2. Kliknij przycisk **Nowy**.
   
    ![Kliknięcie przycisku Nowe][5]
3. Wyszukaj wyrażenie **WordPress**, a następnie kliknij pozycję **WordPress**. Jeśli chcesz toouse SQL Database zamiast MySQL, wyszukaj **Project Nami**.
   
    ![Pozycja WordPress na liście][7]
4. Po przeczytaniu opisu aplikacji WordPress hello hello, kliknij przycisk **Utwórz**.
   
    ![Przycisk Utwórz](./media/web-sites-php-web-site-gallery/create.png)
5. Wprowadź nazwę dla aplikacji sieci web hello w hello **aplikacji sieci Web** pole.
   
    Ta nazwa musi być unikatowa w domenie azurewebsites.net hello, ponieważ adres URL aplikacji sieci web hello hello będzie {nazwa}. azurewebsites.net. Jeśli wprowadzona nazwa hello nie jest unikatowa, w polu tekstowym hello zostanie wyświetlony czerwony wykrzyknik.
6. Jeśli masz więcej niż jedną subskrypcję, wybierz hello co chcesz toouse. 
7. Wybierz **grupę zasobów** lub utwórz nową.
   
    Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Wybierz pozycję **Plan usługi App Service/Lokalizacja** lub utwórz nowy plan.
   
    Aby uzyskać więcej informacji na temat planów usługi App Service, zobacz [Omówienie planów usługi Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).    
9. Kliknij przycisk **bazy danych**, a następnie w hello **Nowa baza danych MySQL** bloku Podaj wartości hello wymagane do konfigurowania bazy danych MySQL.
   
    a. Wprowadź nową nazwę lub pozostaw nazwę domyślną hello.
   
    b. Pozostaw hello **typ bazy danych** ustawić także**Shared**.
   
    c. Wybierz hello wybranych w tej samej lokalizacji, co który hello hello aplikacji sieci web.
   
    d. Wybierz warstwę cenową. Warstwa Mercury (bezpłatnie z minimalnymi dopuszczalnymi połączeniami i miejscem na dysku) jest odpowiednia dla tego samouczka.
10. W hello **Nowa baza danych MySQL** bloku, kliknij przycisk **OK**. 
11. W hello **WordPress** bloku, zaakceptuj postanowienia prawne hello, a następnie kliknij przycisk **Utwórz**. 
    
     ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     Usługa aplikacji Azure tworzy hello aplikacji sieci web, zazwyczaj w mniej niż minutę. Możesz obserwować postęp hello, klikając ikonę dzwonka hello u góry hello hello strony portalu.
    
     ![Wskaźnik postępu](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Uruchamianie aplikacji sieci Web WordPress i zarządzanie nią
1. Po zakończeniu tworzenia aplikacji sieci web hello Przejdź w hello Azure Portal toohello grupie zasobów, w którym została utworzona aplikacja hello, i widoczne hello aplikacji sieci web i hello bazy danych.
   
    Witaj dodatkowym zasobem z ikoną żarówki hello jest [usługi Application Insights](/services/application-insights/), która umożliwia monitorowanie aplikacji sieci web.
2. W hello **grupy zasobów** bloku, kliknij wiersz aplikacji sieci web hello.
   
    ![Konfigurowanie aplikacji sieci Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. W bloku aplikacja sieci Web powitania kliknij **Przeglądaj**.
   
    ![Adres URL witryny][browse]
4. W hello WordPress **powitalnej** wprowadzania informacji konfiguracyjnych hello wymagane przez platformę WordPress, a następnie kliknij przycisk **zainstalować WordPress**.
   
    ![Konfigurowanie usługi WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Zaloguj się za pomocą poświadczeń hello utworzonych na powitania **powitalnej** strony.  
6. Zostanie otwarta strona pulpitu nawigacyjnego witryny.    
   
    ![Witryna WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Następne kroki
Przedstawiono sposób toocreate i wdrażanie aplikacji sieci web PHP z galerii hello. Aby uzyskać więcej informacji na temat używania struktury PHP na platformie Azure, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

Aby uzyskać więcej informacji o tym, jak toowork z aplikacjami sieci Web usługi aplikacji, zobacz linki hello na powitania po lewej stronie powitania stronie (szerokie okna przeglądarki) lub u góry hello hello strony (wąskie okna przeglądarki). 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik toohello zmian z tooApp witryn sieci Web Service, zobacz [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
