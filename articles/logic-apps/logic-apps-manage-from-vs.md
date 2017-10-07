---
title: "aplikacje logiki aaaManage w programie Visual Studio — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Zarządzanie logiki aplikacji i innych zasobów platformy Azure z programu Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Zarządzanie aplikacjami logiki za pomocą programu Visual Studio Cloud Explorer

Mimo że hello [portalu Azure](https://portal.azure.com/) zapewnia to dobry sposób możesz toodesign i zarządzać aplikacje logiki platformy Azure, programu Visual Studio Cloud Explorer można użyć do zarządzania wielu zasobów platformy Azure, w tym aplikacji logiki. Visual Studio Cloud Explorer umożliwia przeglądanie, zarządzanie, edytowanie i pobierania opublikowane aplikacje logiki. Zadania zarządzania obejmują Włącz, wyłącz i uruchom wyświetlanie historii. 

Można było uzyskać dostęp i zarządzać aplikacji logiki w programie Visual Studio, zainstalować i skonfigurować te narzędzia Visual Studio dla usługi Azure Logic Apps. 

## <a name="prerequisites"></a>Wymagania wstępne

* [Visual Studio 2015 lub Visual Studio 2017 r.](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [Najnowszy zestaw Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 lub nowszej)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Access toohello w sieci web używając projektanta osadzonych hello

## <a name="install-visual-studio-tools-for-logic-apps"></a>Instalowanie narzędzi Visual Studio tools for Logic Apps

Po zainstalowaniu wymagań wstępnych hello, Pobierz i zainstaluj hello Azure logiki aplikacji Tools for Visual Studio.

1. Otwórz program Visual Studio. Na powitania **narzędzia** menu, wybierz opcję **rozszerzenia i aktualizacje**.
2. Rozwiń węzeł hello **Online** kategorii, Wyszukaj w trybie online w hello galerii programu Visual Studio.
3. Wyszukaj **Logic Apps** do momentu znalezienia **Azure Logic Apps Tools for Visual Studio**.
4. toodownload i rozszerzenie hello instalacji, kliknij przycisk **Pobierz**.
5. Po zakończeniu instalacji uruchom ponownie program Visual Studio.

> [!NOTE]
> toodownload hello Azure Logic Apps Tools for Visual Studio przejdź bezpośrednio, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Przeglądaj w poszukiwaniu aplikacji logiki w Eksploratorze chmury

1.  tooopen Eksplorator chmury na powitania **widoku** menu, wybierz **Eksplorator chmury**.
2.  Przeglądaj w poszukiwaniu aplikacji logiki, grupy zasobów lub typ zasobu. 

    * Jeśli możesz przeglądać według typów zasobów, wybierz subskrypcję platformy Azure, rozwiń hello **Logic Apps** sekcji, a następnie wybierz aplikację logiki. 
    * Jeśli możesz przeglądać według grupy zasobów, rozwiń hello grupy zasobów aplikacji logiki, a następnie wybierz aplikację logiki.

    polecenia tooview aplikacji logiki, kliknij prawym przyciskiem myszy aplikację logiki, albo u dołu hello Eksplorator chmury, wybierz jedną z hello **akcje** menu.

    ![Przeglądaj w poszukiwaniu aplikacji logiki](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Edytuj w Projektancie aplikacji logiki aplikacji logiki

W Eksploratorze chmury, możesz otworzyć aplikację logiki aktualnie wdrożonych w hello tego samego projektanta, używanego w hello portalu Azure. 

* tooedit aplikację logiki w Eksploratorze chmury, kliknij prawym przyciskiem myszy aplikację logiki, a następnie wybierz **otwarty przy użyciu edytora aplikacji logiki**. 

* toopublish Twojego toohello aktualizacje w chmurze, wybrać **publikowania**. 

* Wybierz toostart nowy przebieg **uruchomić wyzwalacz**.

![Projektant aplikacji logiki](./media/logic-apps-manage-from-vs/designer.png)

Przy użyciu projektanta hello, możesz również **Pobierz** aplikacji logiki. Ta akcja automatycznie parameterizes definicję aplikacji logiki hello i definicji hello jest zapisywany jako szablon wdrożenia usługi Azure Resource Manager. Możesz dodać ten projekt wdrożenia szablonu tooyour grupy zasobów platformy Azure.

## <a name="browse-your-logic-app-run-history"></a>Przeglądaj Historia uruchomień aplikacji logiki

hello tooview Uruchom historii aplikacji logiki, kliknij prawym przyciskiem myszy aplikację logiki, a następnie wybierz **Historia uruchomień Otwórz**. tooreorder historii wykonywania oparte na żadnym z nagłówka kolumny hello pokazano, wybierz pozycję Właściwości hello.

![Historia uruchomień](media/logic-apps-manage-from-vs/runs.png)

Witaj tooshow Uruchom historii dla wystąpienia, aby przejrzeć hello Uruchom wynikami, w tym hello wejścia i wyjścia z każdym kroku, kliknij dwukrotnie jeden z hello uruchomionych wystąpień.

![Uruchom wyników historii, wejścia i wyjścia z kroków](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Następne kroki

* [Tworzenie pierwszej aplikacji logiki](logic-apps-create-a-logic-app.md)
* [Projektowanie, tworzenie i wdrażanie aplikacji logiki w programie Visual Studio](logic-apps-deploy-from-vs.md)
* [Wyświetlanie typowych przykładów i scenariuszy](logic-apps-examples-and-scenarios.md)
* [Wideo: Automatyzować procesy biznesowe z usługi Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Wideo: Integrować systemy z usługą Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
