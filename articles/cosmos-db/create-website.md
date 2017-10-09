---
title: "aaaDeploy aplikacji sieci web przy użyciu szablonu - DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy konta bazy danych Azure rozwiązania Cosmos, aplikacje sieci Web usługi aplikacji Azure i przykładowe aplikacji sieci web przy użyciu szablonu usługi Azure Resource Manager."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Wdrożenie bazy danych Azure rozwiązania Cosmos i Azure Web Apps App Service przy użyciu szablonu usługi Azure Resource Manager
W tym samouczku przedstawiono sposób toouse toodeploy szablonu usługi Azure Resource Manager oraz zintegrowanie [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/), [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci web i przykładowej aplikacji sieci web.

Korzystanie z szablonów usługi Azure Resource Manager, można łatwo automatyzować hello wdrażania i konfigurowania zasobów platformy Azure.  Ten samouczek pokazuje, jak toodeploy aplikacji sieci web i automatycznie skonfigurować parametry połączenia konta bazy danych Azure rozwiązania Cosmos.

Po ukończeniu tego samouczka, będą mogli tooanswer hello następujące pytania:  

* Jak używać toodeploy szablonu usługi Azure Resource Manager i integrowanie konto bazy danych rozwiązania Cosmos Azure i aplikacji sieci web w usłudze Azure App Service?
* Jak używać toodeploy szablonu usługi Azure Resource Manager i integrowanie konta bazy danych rozwiązania Cosmos platformy Azure, aplikacji sieci web w aplikacji usługi sieci Web aplikacji i aplikację Webdeploy?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Wymagania wstępne
> [!TIP]
> Podczas tego samouczka nie zakłada się doświadczenie z szablonów usługi Azure Resource Manager lub JSON, powinien mają toomodify hello przywoływany szablonów lub opcje wdrażania, a następnie wiedzę na temat każdego z tych obszarów będzie wymagane.
> 
> 

Przed rozpoczęciem powitalne instrukcje w tym samouczku, upewnij się, że masz następujące hello:

* Subskrypcja platformy Azure. Azure to platforma subskrypcji.  Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcje zakupu](https://azure.microsoft.com/pricing/purchase-options/), [oferty Członkowskie](https://azure.microsoft.com/pricing/member-offers/), lub [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Krok 1: Pobierz hello pliki szablonów
Zacznijmy od pobierania hello plików szablonów, które będą używane w tym samouczku.

1. Pobierz hello [Tworzenie konta bazy danych Azure rozwiązania Cosmos, aplikacje sieci Web i wdrażanie przykładowej aplikacji demonstracyjnej](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) szablonu tooa lokalny folder (np. C:\Azure rozwiązania Cosmos DBTemplates). Ten szablon zostanie wdrożona, konto bazy danych Azure rozwiązania Cosmos, aplikację usługi aplikacji sieci web i aplikacji sieci web.  Zostanie ona automatycznie skonfigurowana konto bazy danych Azure rozwiązania Cosmos toohello tooconnect hello aplikacji sieci web.
2. Pobierz hello [Tworzenie konta bazy danych Azure rozwiązania Cosmos i przykładowej aplikacji sieci Web](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) szablonu tooa lokalny folder (np. C:\Azure rozwiązania Cosmos DBTemplates). Ten szablon wdroży konto bazy danych Azure rozwiązania Cosmos aplikacji sieci web usługi aplikacji i zmodyfikuje hello lokacji ustawienia tooeasily powierzchni bazy danych Azure rozwiązania Cosmos połączenia informacje o aplikacji, ale nie zawiera aplikacji sieci web.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Krok 2: Wdrażanie hello Azure DB rozwiązania Cosmos konta usługi aplikacji sieci web aplikacji i pokaz aplikacji przykładowych
Teraz wdróżmy naszych pierwszego szablonu.

> [!TIP]
> Szablon Hello nie sprawdzić, czy nazwa aplikacji sieci web hello i nazwę konta bazy danych rozwiązania Cosmos Azure wprowadzono poniżej są) prawidłowe i (b) dostępne.  Zdecydowanie zaleca się, sprawdź dostępność hello hello nazwy należy zaplanować wdrożenie hello wcześniejsze toosubmitting toosupply.
> 
> 

1. Toohello logowania [Azure Portal](https://portal.azure.com), kliknij przycisk Nowy i wyszukaj "Wdrażanie szablonu".
    ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment1.png)
2. Wybierz element wdrożenia hello szablonu, a następnie kliknij przycisk **Utwórz** ![zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment2.png)
3. Kliknij przycisk **Edytuj szablon**, a następnie wklej zawartość pliku szablonu DocDBWebsiteTodo.json hello hello i kliknij przycisk **zapisać**.
   ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment3.png)
4. Kliknij przycisk **Edytuj parametry**, podaj wartości dla poszczególnych hello obowiązkowe parametry i kliknij przycisk **OK**.  Parametry Hello są następujące:
   
   1. Nazwa witryny: Określa hello Nazwa aplikacji sieci web usługi aplikacji i jest używane tooconstruct hello URL użyje aplikacji sieci web hello tooaccess (np. Jeśli określisz "mydemodocdbwebapp", a następnie będzie hello adresu URL za pomocą której będą uzyskiwać dostęp do aplikacji sieci web hello mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Określa nazwę hello hosting toocreate planu usługi aplikacji.
   3. LOKALIZACJĘ: Określa hello lokalizacji platformy Azure, w których toocreate hello sieci web i bazy danych Azure rozwiązania Cosmos zasobów aplikacji.
   4. DATABASEACCOUNTNAME: Określa nazwę hello toocreate konta bazy danych Azure rozwiązania Cosmos hello.   
      
      ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment4.png)
5. Wybierz istniejącą grupę zasobów lub podaj toomake nazwę nowej grupy zasobów, a następnie wybierz lokalizację dla grupy zasobów hello.

    ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment5.png)
6. Kliknij przycisk **Przejrzyj postanowienia prawne**, **zakupu**, a następnie kliknij przycisk **Utwórz** toobegin hello wdrożenia.  Wybierz **toodashboard numeru Pin** , wdrożenie wynikowy hello jest widoczny na stronie głównej portalu Azure.
   ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment6.png)
7. Po zakończeniu wdrożenia hello spowoduje otwarcie bloku grupy zasobów hello.
   ![Zrzut ekranu przedstawiający blok grupa zasobów hello](./media/create-website/TemplateDeployment7.png)  
8. toouse hello aplikacji, wystarczy przejść adres URL aplikacji sieci web toohello (w powyższym przykładzie hello, adres URL hello jest http://mydemodocdbwebapp.azurewebsites.net).  Zostanie wyświetlony hello następującej aplikacji sieci web:
   
   ![Przykładowa aplikacja Todo](./media/create-website/image2.png)
9. Przejdź dalej i Utwórz kilka zadań w aplikacji sieci web hello zwracany bloku grupy zasobów toohello w hello portalu Azure. Kliknij zasób konta bazy danych Azure rozwiązania Cosmos hello hello listy zasobów, a następnie kliknij przycisk **Eksploratora zapytań**.
    ![Zrzut ekranu przedstawiający hello podsumowanie obiektywu hello aplikacji sieci web wyróżnione](./media/create-website/TemplateDeployment8.png)  
10. Uruchom zapytanie domyślne Witaj, "Wybierz * c" i sprawdzić wyniki hello.  Należy zauważyć, że zapytania hello ma pobrać reprezentacja JSON hello hello zadań do wykonania, utworzony w kroku 7 powyżej.  Możesz wolnego tooexperiment z zapytaniami; na przykład, spróbuj uruchomić SELECT * z c WHERE c.isComplete = true tooreturn wszystkie elementy todo, które zostały oznaczone jako zakończone.
    
    ![Zrzut ekranu przedstawiający bloków Eksploratora zapytań i wyniki hello przedstawiający hello wyników zapytania](./media/create-website/image5.png)
11. Możesz hello wolnego tooexplore obsługi portalu Azure DB rozwiązania Cosmos lub zmodyfikuj hello przykładowej aplikacji Todo.  Jeśli wszystko jest gotowe, wdróżmy innego szablonu.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Krok 3: Wdrażanie hello konta dokumentu i przykładowej aplikacji sieci web
Teraz wdróżmy naszych drugiego formularza.  Ten szablon jest przydatne tooshow jak możesz można wstrzyknąć bazy danych Azure rozwiązania Cosmos połączenia informacje takie jak punkt końcowy konta i klucz główny do aplikacji sieci web jako ustawień aplikacji lub niestandardowe parametry połączenia. Na przykład być może masz własnych aplikacji sieci web, że chcesz toodeploy przy użyciu konta bazy danych Azure rozwiązania Cosmos i ma informacje o połączeniu hello automatycznie wypełniane podczas wdrażania.

> [!TIP]
> Szablon Hello nie sprawdzić, czy nazwa aplikacji sieci web hello i nazwę konta bazy danych rozwiązania Cosmos Azure wprowadzono poniżej są) prawidłowe i (b) dostępne.  Zdecydowanie zaleca się, sprawdź dostępność hello hello nazwy należy zaplanować wdrożenie hello wcześniejsze toosubmitting toosupply.
> 
> 

1. W hello [Azure Portal](https://portal.azure.com), kliknij przycisk Nowy i wyszukaj "Wdrażanie szablonu".
    ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment1.png)
2. Wybierz element wdrożenia hello szablonu, a następnie kliknij przycisk **Utwórz** ![zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment2.png)
3. Kliknij przycisk **Edytuj szablon**, a następnie wklej zawartość pliku szablonu DocDBWebSite.json hello hello i kliknij przycisk **zapisać**.
   ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment3.png)
4. Kliknij przycisk **Edytuj parametry**, podaj wartości dla poszczególnych hello obowiązkowe parametry i kliknij przycisk **OK**.  Parametry Hello są następujące:
   
   1. Nazwa witryny: Określa hello Nazwa aplikacji sieci web usługi aplikacji i jest używane tooconstruct hello URL użyje aplikacji sieci web hello tooaccess (np. Jeśli określisz "mydemodocdbwebapp", a następnie będzie hello adresu URL za pomocą której będą uzyskiwać dostęp do aplikacji sieci web hello mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Określa nazwę hello hosting toocreate planu usługi aplikacji.
   3. LOKALIZACJĘ: Określa hello lokalizacji platformy Azure, w których toocreate hello sieci web i bazy danych Azure rozwiązania Cosmos zasobów aplikacji.
   4. DATABASEACCOUNTNAME: Określa nazwę hello toocreate konta bazy danych Azure rozwiązania Cosmos hello.   
      
      ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment4.png)
5. Wybierz istniejącą grupę zasobów lub podaj toomake nazwę nowej grupy zasobów, a następnie wybierz lokalizację dla grupy zasobów hello.

    ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment5.png)
6. Kliknij przycisk **Przejrzyj postanowienia prawne**, **zakupu**, a następnie kliknij przycisk **Utwórz** toobegin hello wdrożenia.  Wybierz **toodashboard numeru Pin** , wdrożenie wynikowy hello jest widoczny na stronie głównej portalu Azure.
   ![Zrzut ekranu przedstawiający wdrażanie szablonu hello interfejsu użytkownika](./media/create-website/TemplateDeployment6.png)
7. Po zakończeniu wdrożenia hello spowoduje otwarcie bloku grupy zasobów hello.
   ![Zrzut ekranu przedstawiający blok grupa zasobów hello](./media/create-website/TemplateDeployment7.png)  
8. Kliknij zasób aplikacji sieci Web hello hello listy zasobów, a następnie kliknij przycisk **ustawienia aplikacji** ![zrzut ekranu przedstawiający hello grupy zasobów](./media/create-website/TemplateDeployment9.png)  
9. Należy zwrócić uwagę, jak są obecne dla punktu końcowego bazy danych Azure rozwiązania Cosmos hello i każdy klucz główny bazy danych Azure rozwiązania Cosmos hello ustawienia aplikacji.

    ![Zrzut ekranu przedstawiający ustawień aplikacji](./media/create-website/TemplateDeployment10.png)  
10. Możesz wolnego toocontinue eksploracji hello portalu Azure lub użyj jednego z naszych Azure DB rozwiązania Cosmos [przykłady](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate aplikacji bazy danych Azure rozwiązania Cosmos.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Następne kroki
Gratulacje! Wdrożeniu Azure rozwiązania Cosmos bazy danych, aplikacji sieci web usługi aplikacji i przykładowej aplikacji sieci web przy użyciu szablonów usługi Azure Resource Manager.

* toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, kliknij przycisk [tutaj](http://azure.com/docdb).
* toolearn więcej informacji na temat aplikacji sieci Web usługi aplikacji Azure, kliknij przycisk [tutaj](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn więcej informacji na temat szablonów usługi Azure Resource Manager, kliknij przycisk [tutaj](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
* Toohello przewodnik zmiany hello starego portalu toohello nowego portalu dla: [odwołanie do nawigowania hello klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](http://go.microsoft.com/fwlink/?LinkId=523751), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

