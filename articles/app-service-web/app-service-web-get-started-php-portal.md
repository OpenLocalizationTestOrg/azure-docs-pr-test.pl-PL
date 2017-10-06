---
title: "aaaDeploy aplikacji WordPress w portalu Azure w ciągu pięciu minut hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łatwo jest toorun aplikacje sieci web w usłudze App Service, wdrażając aplikacji WordPress. Wyniki będą widoczne od razu."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Wdrażanie aplikacji WordPress w hello portalu Azure w ciągu pięciu minut

W tym samouczku przedstawiono sposób toodeploy pierwszego [WordPress](https://wordpress.org/) sieci web aplikacji zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) w minutach.

![Witryna WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Wymagania wstępne
Potrzebujesz konta platformy Microsoft Azure. Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure. Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Wdrażanie aplikacji WordPress hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Otwórz link [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    To łącze jest tooimmediately skrótów skonfiguruj nową aplikację WordPress w hello portalu Azure.

3. W polu **Nazwa aplikacji** wpisz nazwę aplikacji sieci Web. Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `azurewebsites.net` domeny.
   
5. W **grupy zasobów**, kliknij przycisk **Utwórz nowy** toocreate nowy [grupy zasobów](../azure-resource-manager/resource-group-overview.md), następnie nadaj mu nazwę.

6. W polu **Dostawca bazy danych** wybierz pozycję **CleaDB**.

7. Kliknij pozycję **Plan/lokalizacja usługi App Service** > **Utwórz nowy**. Skonfiguruj hello [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pokazany:

    - W **planu usługi aplikacji**, żądana nazwa hello typu.
    - W **lokalizacji**, wybierz plan toohost lokalizacji.
    - Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F1** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.
    - Kliknij przycisk **OK**.

8. Kliknij pozycję **Baza danych** > **Utwórz nową**. Skonfiguruj hello bazy danych SQL, jak pokazano:

    - W polu **Nazwa bazy danych** wpisz nazwę bazy danych. 
    - W **lokalizacji**, wybierz hello tej samej lokalizacji co hello planu usługi aplikacji.
    - Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Mercury** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.
    - Kliknij pozycję **Postanowienia prawne**, a następnie pozycję **Zakup**.
    - Kliknij przycisk **OK**.

9. Kliknij przycisk **Utwórz**.

    Platforma Azure utworzy teraz aplikację WordPress zgodnie z konfiguracją. Powinno być widoczne powiadomienie **Wdrażanie rozpoczęte...**.

    ![Wdrażanie rozpoczęte — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Uruchamianie aplikacji sieci Web WordPress i zarządzanie nią

Po zakończeniu wdrażania aplikacji przez platformę Azure zostanie wyświetlone kolejne powiadomienie.

![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Kliknij powiadomienie hello. Jeśli pominięte go, należy zawsze do niego dostęp, klikając hello dzwonka powiadomień (![powiadomień poniższych — pierwszy WordPress w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Powinien zostać wyświetlony [blok](../azure-resource-manager/resource-group-portal.md#manage-resources) zarządzania aplikacją sieci Web (*blok*: strona portalu otwierana poziomo).

3. W hello górnej części strony Przegląd hello, kliknij przycisk **Przeglądaj**.
   
    ![Przeglądanie — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    Teraz zostanie wyświetlony hello WordPress **powitalnej** strony. Skonfiguruj hello WordPress instalację i rozpocząć odtwarzanie z nim!

    ![Konfiguracja platformy WordPress — pierwsza aplikacja WordPress w usłudze Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Następne kroki
* [Tworzenie, konfigurowanie i wdrażanie tooAzure aplikacji sieci web Laravel](app-service-web-php-get-started.md) — Dowiedz się hello podstawowe umiejętności toorun dowolnej aplikacji sieci web PHP na platformie Azure, takich jak:

    * tworzenie i konfigurowanie aplikacji na platformie Azure z poziomu programu PowerShell/Bash;
    * ustawianie wersji języka PHP;
    * Użyj pliku początkowej, który nie znajduje się w katalogu aplikacji hello głównego.
    * włączanie automatyzacji narzędzia Composer;
    * uzyskiwanie dostępu do zmiennych określonych dla środowiska;
    * rozwiązywanie typowych problemów.

* [Wdrażanie tooAzure Twojego kodu usługi aplikacji —](web-sites-deploy.md)— Dowiedz się, jak toodeploy z FTP lub źródło kontroli repozytoriów.
* [Dodawanie funkcji tooyour pierwszej aplikacji sieci web](app-service-web-get-started-2.md) -podjąć toohello Twojej aplikacji Azure obok poziomu. Uwierzytelniaj użytkowników. Skaluj ją zależnie od potrzeb. Skonfiguruj alerty dotyczące wydajności. Wszystkie te czynności możesz wykonać za pomocą kilku kliknięć.
