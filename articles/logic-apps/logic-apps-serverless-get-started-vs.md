---
title: "aaaBuild niekorzystającą aplikacji w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do pierwszej aplikacji niekorzystającą z tego przewodnika na tworzenie, wdrażanie i Zarządzanie aplikacją hello w programie Visual Studio."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Tworzenie aplikacji bez serwera w programie Visual Studio z Logic Apps i funkcje

Pliki narzędzia i funkcje na platformie Azure umożliwia szybkie opracowywanie i wdrażanie aplikacji w chmurze.  Ten dokument koncentruje się na temat tooget uruchomiony w programie Visual Studio tworzenia aplikację niekorzystającą z serwera.  Omówienie niekorzystającą na platformie Azure [znajduje się w tym artykule](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Przygotowanie wszystko

Oto hello wymagania wstępne niezbędne toobuild aplikację niekorzystającą z programu Visual Studio:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) lub Visual Studio 2015 — Community, Professional lub Enterprise
* [Logic Apps Tools for Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [Najnowszy zestaw Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 lub nowszej)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Azure funkcje podstawowe narzędzia](https://www.npmjs.com/package/azure-functions-core-tools) toodebug działa lokalnie
* Access toohello w sieci web przy użyciu hello osadzone projektanta aplikacji logiki

## <a name="getting-started-with-a-deployment-template"></a>Wprowadzenie do szablonu wdrożenia

Zarządzanie zasobami na platformie Azure są wykonywane w ramach grupy zasobów.  Grupa zasobów jest logiczną grupą zasobów.  Grupy zasobów umożliwiają wdrażanie i zarządzanie kolekcją zasobów.  Pliki aplikacji na platformie Azure naszej grupy zasobów zawiera aplikacje logiki platformy Azure i usługi Azure Functions.  Za pomocą hello projektu grupy zasobów w programie Visual Studio, jesteśmy w stanie toodevelop, zarządzanie i wdrażanie całej aplikacji hello jako pojedynczy zasób.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Tworzenie projektu grupy zasobów w programie Visual Studio

1. W programie Visual Studio, kliknij przycisk tooadd **nowy projekt**
1. W hello **chmury** kategorii, wybierz opcję toocreate Azure **grupy zasobów** projektu  
 * Jeśli nie ma kategorii hello lub na liście projektu, upewnij się, że masz hello zestawu Azure SDK zainstalowany dla programu Visual Studio
1. Nadaj hello projektu, nazwy i lokalizacji, a następnie wybierz **Ok** toocreate programu Visual Studio monituje tooselect szablonu.  Toostart można wybierać puste, rozpoczyna się od logiki aplikacji lub innego zasobu.  Jednak w takim przypadku stosujemy tooget szablonie Szybki Start Azure nam pracę bez serwera aplikacji.
1. Wybierz szablony tooshow z **Szybki Start Azure** ![szablony wybranie Szybki Start Azure][1]
1. Wybierz hello szablonu niekorzystającą Szybki Start: **101-logic-app-and-function-app** i kliknij przycisk **Ok**

Szablon szybkiego startu Hello tworzy szablon wdrożenia w projekcie grupy zasobów.  Szablon Hello zawiera prostej aplikacji logiki, który wywołuje usługi Azure Functions i zwraca wynik hello.  Po otwarciu hello `azuredeploy.json` pliku w hello Eksploratorze rozwiązań, mogą zobaczyć hello zasobów dla aplikacji niekorzystającą hello.

## <a name="deploying-hello-serverless-application"></a>Wdrażanie aplikacji niekorzystającą hello

Zanim będzie można otworzyć projektanta wizualnego hello aplikacji logiki w programie Visual Studio, musi toobe wstępnie wdrożonej grupy zasobów platformy Azure.  Dzięki temu w aplikacji logiki hello hello toocreate projektanta i użyj połączenia tooresources i usług.  tooget uruchomiona, należy utworzyć rozwiązanie hello toodeploy.

1. Kliknij prawym przyciskiem myszy hello projektu programu Visual Studio, wybierz **Wdróż**i Utwórz **nowy** wdrożenia ![wybranie nowego zasobu wdrożenia][2]
1. Wybierz ważnej subskrypcji platformy Azure i grupy zasobów
1. Wybierz zbyt**Wdróż** hello rozwiązania
1. Wprowadź w hello nazwę hello aplikacji logiki i hello Azure funkcji aplikacji.  Nazwa funkcji Azure Hello, należy toobe będzie globalnie unikatowa

rozwiązanie niekorzystającą Hello wdraża do hello określonej grupy zasobów.  Jeśli przyjrzymy się hello **dane wyjściowe** w programie Visual Studio można wyświetlić stan hello hello wdrożenia.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Edytowanie aplikacji logiki hello w programie Visual Studio

Po hello rozwiązanie zostało wdrożone w dowolnej grupie zasobów, Projektant wizualny powitalnych można tooedit używane i utworzyć aplikację logiki toohello zmiany.

1. Powitania kliknij prawym przyciskiem myszy `azuredeploy.json` plików w Eksploratorze rozwiązań hello i wybierz **otwarty z logiki aplikacji Projektant**
1. Wybierz hello **grupy zasobów** i **lokalizacji** hello rozwiązanie zostało wdrożone wybierz tooand **OK**

Projektant wizualny aplikacji logiki Hello teraz powinny być widoczne z programem Visual Studio.  Można kontynuować czynności tooadd, Modyfikuj hello i Zapisz zmiany.  Można również utworzyć aplikacje logiki z programu Visual Studio.  Kliknięcie prawym przyciskiem myszy hello **zasobów** hello navigator szablonu, można wybrać tooadd **aplikacji logiki** toohello projektu.  Aplikacje logiki pusty ładowania projektanta wizualnego hello bez wykonaj wstępne wdrożenie w grupie zasobów.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Zarządzanie i historię uruchomień na potrzeby aplikacji logiki wdrożonej przeglądanie

Można również zarządzać i wyświetlić historię hello uruchamiania aplikacji logiki wdrożonych na platformie Azure.  Po otwarciu hello **Eksplorator chmury** narzędzia w programie Visual Studio, kliknij prawym przyciskiem myszy dowolną aplikację logiki i wybierz tooedit, wyłącz, właściwości widoku lub widok Historia uruchomień.  Klikając przycisk Edytuj pozwala również toodownload aplikacji logiki opublikowane w projekcie grupy zasobów w usłudze Visual Studio.  Oznacza to, że nawet jeśli Rozpoczęto tworzenie aplikacji logiki w hello portalu Azure, można nadal zaimportuj go i nim zarządzać za pomocą programu Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Tworzenie funkcji platformy Azure w programie Visual Studio

Witaj Szablon wdrożenia wdraża wszystkie funkcje platformy Azure, znajdujących się w rozwiązaniu hello repozytorium git hello określone w hello `azuredeploy.json` zmiennych.  Jeśli tworzenia projektu funkcji w ramach rozwiązania hello sprawdź go do kontroli źródła (GitHub, Visual Studio Team Services itp.) i zaktualizuj hello `repo` zmiennej, szablon hello wdroży hello funkcji platformy Azure.

### <a name="creating-an-azure-function-project"></a>Tworzenie projektu funkcji platformy Azure

Jeśli przy użyciu języka JavaScript, Python, F #, Bash, partii lub programu PowerShell, wykonaj hello [etapami hello funkcje interfejsu wiersza polecenia](../azure-functions/functions-run-local.md) toocreate projektu.  Tworzenie funkcji w języku C#, można użyć [biblioteki klas C#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) w bieżącym rozwiązaniu hello na powitania funkcji platformy Azure.

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak toobuild niekorzystającą społecznościowych pulpitu nawigacyjnego](logic-apps-scenario-social-serverless.md)
* [Zarządzanie aplikacji logiki z programu Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Język definicji przepływu pracy aplikacji logiki](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
