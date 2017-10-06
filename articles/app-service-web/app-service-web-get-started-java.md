---
title: aaaCreate pierwszej aplikacji sieci web Java na platformie Azure
description: "Dowiedz się, jak toorun web apps w usłudze App Service przez wdrożenie podstawowego aplikacji Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Tworzenie pierwszej aplikacji internetowej w środowisku Java na platformie Azure

Witaj [aplikacje sieci Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funkcji [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web. Ta opcja szybkiego startu przedstawia, jak toodeploy Java web app tooApp usługi za pomocą hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).

![„Hello Azure!” — przykładowa aplikacja internetowa](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego przewodnika Szybki Start, zainstalować:

* Witaj wolnego [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/). W tym przewodniku Szybki start używane jest środowisko Eclipse Neon.
* Witaj [zestawu narzędzi platformy Azure dla programu Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Tworzenie dynamicznego projektu internetowego w środowisku Eclipse

W środowisku Eclipse wybierz pozycję **File** > **New** > **Dynamic Web Project** (Plik > Nowy > Dynamiczny projekt internetowy).

W hello **nowego projektu sieci Web dynamiczne** okno dialogowe, nazwa projektu hello **MyFirstJavaOnAzureWebApp**i wybierz **Zakończ**.
   
![Okno dialogowe New Dynamic Web Project (Nowy dynamiczny projekt internetowy)](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Dodawanie strony JSP

Jeśli obszar Project Explorer (Eksplorator projektów) nie jest wyświetlany, przywróć go.

![Obszar roboczy Java EE dla środowiska Eclipse](./media/app-service-web-get-started-java/pe.png)

W obszarze Eksplorator projektów rozwiń hello **MyFirstJavaOnAzureWebApp** projektu.
Kliknij prawym przyciskiem myszy folder **WebContent**, a następnie kliknij pozycję **New** > **JSP File** (Nowy > Plik JSP).

![Menu dla nowego pliku JSP w obszarze Project Explorer (Eksplorator projektów)](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

W hello **New JSP File** okno dialogowe:

* Nazwa pliku hello **index.jsp**.
* Wybierz pozycję **Finish** (Zakończ).

  ![Okno dialogowe New JSP File (Nowy plik JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

W pliku index.jsp hello Zastąp hello `<body></body>` element z powitania po znaczników:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Zapisz zmiany hello.

## <a name="publish-hello-web-app-tooazure"></a>Publikowanie tooAzure aplikacji sieci web hello

W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako aplikacji sieci Web Azure**.

![Menu kontekstowe Publish as Azure Web App (Publikuj jako aplikację internetową platformy Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

W hello **Azure logowania** okno dialogowe, Zachowaj hello **Interactive** opcji, a następnie wybierz **Zaloguj**.

Instrukcjami hello logowania.

### <a name="deploy-web-app-dialog-box"></a>Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)

Po zalogowaniu tooyour konta Azure hello **wdrażanie aplikacji sieci Web** zostanie wyświetlone okno dialogowe.

Wybierz pozycję **Utwórz**.

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Okno dialogowe Create App Service (Tworzenie usługi App Service)

Witaj **Tworzenie usługi App Service** zostanie wyświetlone okno dialogowe z wartościami domyślnymi. Witaj numer **170602185241** pokazano powitania po obrazu różni się w oknie dialogowym.

![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/cas1.png)

W hello **Tworzenie usługi App Service** okno dialogowe:

* Zachowaj nazwę hello generowany dla aplikacji sieci web hello. Ta nazwa musi być unikatowa w obrębie całej platformy Azure. Nazwa Hello jest częścią hello adres URL aplikacji sieci web hello. Na przykład: Jeśli nazwa aplikacji sieci web hello jest **MyJavaWebApp**, adres URL jest hello *myjavawebapp.azurewebsites.net*.
* Zachowaj hello domyślny kontener sieci web.
* Wybierz subskrypcję platformy Azure.
* Na powitania **plan usługi App service** karty:

  * **Utwórz nowe**: Zachowaj domyślne hello, czyli nazwa hello hello planu usługi aplikacji.
  * **Location** (Lokalizacja): wybierz pozycję **West Europe** (Europa Zachodnia) lub lokalizację w Twoim pobliżu.
  * **Warstwa cenowa**: Wybierz hello bezpłatną opcją. Aby uzyskać informacje o funkcjach, zobacz [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/) (Cennik usługi App Service).

   ![Okno dialogowe Create App Service (Tworzenie usługi App Service)](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Karta Resource group (Grupa zasobów)

Wybierz hello **grupy zasobów** kartę. Należy zachować wartość domyślną wygenerowany hello hello grupy zasobów.

![Karta Resource group (Grupa zasobów)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Wybierz pozycję **Utwórz**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello Azure Toolkit hello aplikacji sieci web tworzy i wyświetla okno dialogowe postępu.

![Okno dialogowe Create App Service Progress (Postęp tworzenia usługi App Service)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)

W hello **wdrażanie aplikacji sieci Web** okno dialogowe, wybierz opcję **wdrażanie tooroot**. Jeśli masz usługę aplikacji na *wingtiptoys.azurewebsites.net* i nie należy wdrażać toohello głównego, hello aplikacji sieci web o nazwie **MyFirstJavaOnAzureWebApp** jest wdrażany za *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Okno dialogowe Deploy Web App (Wdrażanie aplikacji internetowej)](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

Pokazuje okno dialogowe Hello hello Azure, JDK i opcje kontenera sieci web.

Wybierz **Wdróż** tooAzure aplikacji sieci web hello toopublish.

Po zakończeniu publikowania hello, wybierz hello **opublikowano** łącze w hello **dziennika aktywności platformy Azure** okno dialogowe.

![Okno dialogowe Azure Activity Log (Dziennik aktywności platformy Azure)](./media/app-service-web-get-started-java/aal.png)

Gratulacje! Pomyślnie wdrożono tooAzure aplikacji sieci web. 

![„Hello Azure!” — przykładowa aplikacja internetowa](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Aktualizowanie aplikacji sieci web hello

Zmień hello przykładowa JSP kodu tooa inną wiadomość.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Zapisz zmiany hello.

W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako aplikacji sieci Web Azure**.

Witaj **wdrażanie aplikacji sieci Web** zostanie wyświetlone okno dialogowe i pokazuje hello wcześniej utworzoną usługę aplikacji. 

> [!NOTE]
> Wybierz **wdrażanie tooroot** zawsze publikowania.
>

Wybierz aplikację sieci web hello i wybierz **Wdróż**, która publikuje hello zmiany.

Gdy hello **publikowania** łącze jest wyświetlane, wybierz go w aplikacji sieci web toohello toobrowse i zobaczyć zmiany hello.

## <a name="manage-hello-web-app"></a>Zarządzanie hello aplikacji sieci web

Przejdź toohello <a href="https://portal.azure.com" target="_blank">portalu Azure</a> aplikacji sieci web hello toosee, który został utworzony.

Wybierz z menu po lewej stronie powitania **grup zasobów**.

![Grupy tooresource nawigacji w portalu](media/app-service-web-get-started-java/rg.png)

Wybierz grupę zasobów hello. na stronie powitania są pokazane hello zasobów, które zostały utworzone w tym Szybki Start.

![Grupa zasobów myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Wybierz hello aplikacji sieci web (**170602193915 aplikacji sieci Web** w hello poprzedzające obraz).

Witaj **omówienie** zostanie wyświetlona strona. Ta strona umożliwia widok jak robi aplikacji hello. Tutaj możesz wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Witaj w lewej części strony hello hello kartach hello różne konfiguracje, które można otworzyć. 

![Strona usługi App Service w witrynie Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Mapowanie domeny niestandardowej](app-service-web-tutorial-custom-domain.md)
