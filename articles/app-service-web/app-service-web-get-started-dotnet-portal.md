---
title: "aaaDeploy Umbraco aplikacji sieci web w portalu Azure w ciągu pięciu minut hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak łatwo jest toorun aplikacje sieci web w usłudze App Service, wdrażając przykładową aplikację ASP.NET. Wyniki będą widoczne od razu."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Wdrażanie aplikacji sieci web Umbraco w hello portalu Azure w ciągu pięciu minut

Ten samouczek ułatwia wdrażanie n [Umbraco](https://our.umbraco.org/) sieci web aplikacji zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) w minutach.

![Aplikacja Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Wymagania wstępne
Potrzebujesz konta platformy Microsoft Azure. Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure. Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Wdrażanie aplikacji ASP.NET hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Otwórz link [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    To łącze jest tooimmediately skrótów skonfiguruj nową aplikację Umbraco w hello portalu Azure.

3. W polu **Nazwa aplikacji** wpisz nazwę aplikacji sieci Web. Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `azurewebsites.net` domeny.
   
5. W **grupy zasobów**, kliknij przycisk **Utwórz nowy** toocreate nowy [grupy zasobów](../azure-resource-manager/resource-group-overview.md), następnie nadaj mu nazwę.

7. Kliknij pozycję **Plan/lokalizacja usługi App Service** > **Utwórz nowy**. Skonfiguruj hello [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pokazany:

    - W **planu usługi aplikacji**, żądana nazwa hello typu.
    - W **lokalizacji**, wybierz plan toohost lokalizacji.
    - Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F1** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.
    - Kliknij przycisk **OK**.

    Umbraco CMS konfiguracji powinna wyglądać tak jak powitania po zrzut ekranu:

    ![Konfiguracja w toku — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Kliknij opcję **Baza danych SQL** > **Utwórz nową bazę danych**. Skonfiguruj hello bazy danych SQL, jak pokazano:

    - W polu **Nazwa** wpisz nazwę, np. **mojaBazaDanych**.
    - Kliknij pozycję **Warstwa cenowa**, wybierz warstwę **Bezpłatna F** lub inną warstwę, która Ci odpowiada, a następnie kliknij pozycję **Wybierz**.
    - Kliknij pozycję **Serwer docelowy** > **Utwórz nowy serwer**. Skonfiguruj powitania serwera bazy danych, jak pokazano:

        - W polu **Nazwa serwera** wpisz nazwę serwera. Jeśli nazwa hello jest unikatowa w hello zobaczą zielonym znacznikiem wyboru w polu hello `.database.windows.net` domeny.
        - W **identyfikator logowania administratora serwera**, hello typu potrzebne administratora nazwy użytkownika.
        - W **hasło** i **Potwierdź hasło**, typ hello wymagane hasło.
        - W lokalizacji wybierz hello tej samej lokalizacji, używane w przypadku aplikacji sieci web hello.
        - Upewnij się, że **Zezwalaj usługom platformy azure tooaccess serwera** jest zaznaczone.
        - Kliknij pozycję **Wybierz**.
    
    - Kliknij pozycję **Wybierz**.

13. Kliknij przycisk **ustawienia aplikacji w sieci Web**, określ hello bazy danych użytkownika i hasło i kliknij **OK**.

    Umbraco CMS konfiguracji powinna wyglądać tak jak powitania po zrzut ekranu:

    ![Konfiguracja ukończona — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Kliknij przycisk **Utwórz**.
    
    Platforma Azure utworzy teraz aplikację Umbraco zgodnie z konfiguracją. Powinno być widoczne powiadomienie **Wdrażanie rozpoczęte...**.

    ![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Uruchamianie aplikacji sieci Web Umbraco i zarządzanie nią

Po zakończeniu wdrażania aplikacji przez platformę Azure zostanie wyświetlone kolejne powiadomienie.

![Wdrażanie zakończyło się pomyślnie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Kliknij powiadomienie hello. Jeśli pominięte go, należy zawsze do niego dostęp, klikając hello dzwonka powiadomień (![powiadomień poniższych — pierwszy program Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Powinien zostać wyświetlony [blok](../azure-resource-manager/resource-group-portal.md#manage-resources) zarządzania aplikacją sieci Web (*blok*: strona portalu otwierana poziomo).

3. W hello górnej części strony Przegląd hello, kliknij przycisk **Przeglądaj**.
   
    ![Przeglądanie — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Teraz zostanie wyświetlony hello Umbraco **powitalnej** strony. Skonfiguruj hello Umbraco instalację i rozpocząć odtwarzanie z nim!

    ![Konfiguracja aplikacji Umbraco — pierwsza aplikacja Umbraco w usłudze Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Następne kroki
* [Wdrażanie tooAzure aplikacji sieci web ASP.NET App Service przy użyciu programu Visual Studio](app-service-web-get-started-dotnet.md) — Dowiedz się, jak toocreate nowej aplikacji sieci web platformy Azure w programie Visual Studio przy użyciu jednego z hello uwzględnione szablonów aplikacji.
* [Wdrażanie tooAzure Twojego kodu usługi aplikacji —](web-sites-deploy.md)— Dowiedz się, jak toodeploy z FTP lub źródło kontroli repozytoriów.
* [Dodawanie funkcji tooyour pierwszej aplikacji sieci web](app-service-web-get-started-2.md) -podjąć toohello Twojej aplikacji Azure obok poziomu. Uwierzytelniaj użytkowników. Skaluj ją zależnie od potrzeb. Skonfiguruj alerty dotyczące wydajności. Wszystkie te czynności możesz wykonać za pomocą kilku kliknięć.
