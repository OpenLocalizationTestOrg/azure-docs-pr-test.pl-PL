---
title: "aaaManaging Azure zasobami za pomocą Eksploratora chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobrowse Eksplorator chmury toouse i zarządzania zasobami Azure w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Zarządzanie zasobami hello skojarzone z konta platformy Azure w Visual Studio Cloud Explorer
Eksplorator chmury umożliwia możesz tooview zasobów platformy Azure i grup zasobów, sprawdzić ich właściwości i akcje developer klucza diagnostycznych z poziomu programu Visual Studio. 

Podobnie jak hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Eksplorator chmury jest zbudowany na powitania stosu usługi Azure Resource Manager. W związku z tym Eksplorator chmury rozumie zasobów, takich jak grupy zasobów platformy Azure i usług Azure, takich jak aplikacje logiki i interfejsu API apps i obsługuje [kontroli dostępu opartej na rolach](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Wymagania wstępne
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) z hello **obciążenia Azure** zaznaczone, lub starszej wersji programu Visual Studio z hello [Microsoft Azure SDK dla programu .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Konto Microsoft Azure — Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](http://go.microsoft.com/fwlink/?LinkId=623901) lub [aktywować korzyści dla subskrybentów programu Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> Wybierz tooview Eksplorator chmury **widoku** > **Eksplorator chmury** hello paska menu.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Dodaj konto platformy Azure tooCloud Explorer
zasoby hello tooview skojarzone z kontem platformy Azure, należy najpierw dodać hello konta tooCloud Explorer. 

1. W **Eksplorator chmury**, wybierz pozycję **ustawienia konta Azure**.

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Wybierz **Dodaj nowe konto**. 

    ![Łącze Eksploratora Dodaj konto w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Zaloguj się za toohello konto platformy Azure, którego zasoby mają toobrowse. 

1. Po zalogowaniu tooan konto platformy Azure, wyświetlanie subskrypcji hello skojarzonych z tym kontem. Wybierz hello pola wyboru dla subskrypcji kont hello mają toobrowse, a następnie wybierz **Zastosuj**. 
 
    ![Eksplorator chmury: Wybierz toodisplay subskrypcji platformy Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Po wybraniu subskrypcji hello którego zasoby mają toobrowse, te subskrypcje i zasobów wyświetlane w hello Eksplorator chmury.

    ![Eksplorator zasobów dla konta platformy Azure w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Usuń konto platformy Azure w Eksploratorze chmury 

1. W **Eksplorator chmury**, wybierz pozycję **ustawienia konta Azure**.

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Wybierz następny toohello konta tooremove, **Usuń**.

    ![Ikona ustawienia konta Azure Eksplorator chmury](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Wyświetlanie typów zasobów lub grupy zasobów
tooview zasobów platformy Azure, można wybrać jedną **typów zasobów** lub **grup zasobów** widoku.

1. W **Eksplorator chmury**, wybierz hello lista rozwijana widok zasobów.

    ![Cloud Explorer listy rozwijanej liście tooselect hello żądany widok zasobów](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Z menu kontekstowego hello wybierz widok hello potrzeby: 

    - **Typy zasobów** widok - hello widok typowych używany na powitania [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), pokazuje zasobów platformy Azure podzielone według typu, takich jak aplikacje sieci web, konta magazynu i maszyn wirtualnych. 
    - **Grupy zasobów** view - zasobów Azure kategoryzuje przez hello grupy zasobów platformy Azure, z którym są powiązane. Grupa zasobów to pakiet zasobów platformy Azure, zwykle używanych przez określoną aplikację. toolearn więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).

    Witaj poniższej ilustracji przedstawiono porównanie hello dwa widoki zasobów:

    ![Eksplorator zasobów widoków porównania w chmurze](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Wyświetlanie i przejdź do zasobów w Eksploratorze chmury
tooan toonavigate zasobów platformy Azure i wyświetlić informacje o nim w Eksploratorze chmury, rozwiń element hello typu lub grupy zasobów, a następnie wybierz hello zasobów. Po wybraniu zasobu informacje są wyświetlane na kartach hello dwu - **akcje** i **właściwości** — u dołu hello Eksplorator chmury. 

- **Akcje** karcie - list hello akcje można wykonać w Eksploratorze chmury dla zasobu hello wybrane. Można również wyświetlić te opcje przez kliknięcie prawym przyciskiem myszy tooview zasobów hello jego menu kontekstowego.

- **Właściwości** karcie — pokazuje hello właściwości zasobu hello, takich jak grupy jego typu, ustawienia regionalne i zasobów, z którym jest skojarzona.

Witaj poniższej ilustracji przedstawiono przykład porównanie informacje wyświetlane na każdej karcie usługi aplikacji:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Każdy zasób istnieje akcja hello **Otwórz w portalu**. Po wybraniu tej akcji, Eksplorator chmury Wyświetla zasobów hello wybrane w hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Witaj **Otwórz w portalu** funkcja jest przydatna do nawigowania toodeeply zagnieżdżone zasoby.

Dodatkowe akcje i wartości właściwości mogą również wyświetlane w zależności od hello zasobów platformy Azure. Na przykład aplikacje sieci web i aplikacje logiki również mieć akcje hello **Otwórz w przeglądarce** i **dołączyć debuger** dodatkowo zbyt**Otwórz w portalu**. Edytory tooopen akcje są wyświetlane po wybraniu obiektu blob z konta magazynu, kolejki lub tabeli. Aplikacje platformy Azure ma **adres URL** i **stan** właściwości, gdy zasobów magazynu ma właściwości parametrów połączenia i klucza.

## <a name="find-resources-in-cloud-explorer"></a>Znajdź zasoby w Eksploratorze chmury
zasoby toolocate o określonej nazwie w subskrypcji konto platformy Azure, wprowadź nazwę hello w hello **wyszukiwania** pole w Eksploratorze chmury.

![Znajdowanie zasobów w Eksploratorze chmury](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Podczas wprowadzania znaków hello **wyszukiwania** okno, tylko zasoby, spełniające te znaki są wyświetlane w drzewie zasobów hello.
