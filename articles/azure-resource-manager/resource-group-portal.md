---
title: "aaaUse toomanage portalu Azure zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj portalu Azure i usługi Azure Resource Manager toomanage zasobów. Pokazuje sposób toowork z zasobami toomonitor pulpitów nawigacyjnych."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Zarządzania zasobami Azure za pośrednictwem portalu
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfejs wiersza polecenia platformy Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [Interfejs API REST](resource-manager-rest-api.md)
> 
> 

W tym temacie przedstawiono sposób toouse hello [portalu Azure](https://portal.azure.com) z [usługi Azure Resource Manager](resource-group-overview.md) toomanage zasobów platformy Azure. Zobacz toolearn dotyczących wdrażania zasobów za pośrednictwem portalu hello [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).

Obecnie nie wszystkie usługi obsługuje portalu hello lub Menedżera zasobów. W przypadku tych usług należy toouse hello [klasyczny portal](https://manage.windowsazure.com). Witaj stan każdej usługi, zobacz [wykresu dostępności portalu Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Zarządzanie grupami zasobów

Grupa zasobów jest kontenerem, który zawiera powiązane zasoby Azure rozwiązania. Grupa zasobów Hello mogą obejmować wszystkie zasoby hello hello rozwiązania lub tylko tych zasobów, które mają toomanage jako grupa. Możesz zdecydować, jak zasoby tooallocate tooresource grupy oparte na to, co sprawia, że hello najbardziej odpowiednie dla Twojej organizacji. Ogólnie rzecz biorąc, Dodaj zasoby, które współużytkują hello tego samego toohello cyklu życia zasobów w tej samej grupy tak łatwe wdrażanie, aktualizować i usuwać je jako grupę. 

Grupa zasobów Hello są przechowywane metadane dotyczące hello zasobów. W związku z tym po określeniu lokalizacji dla grupy zasobów hello określisz przechowywania tych metadanych. Ze względu na zgodność może być konieczne tooensure danych przechowywanych w określonym regionie.

1. Wybierz wszystkie grupy zasobów hello w ramach subskrypcji, toosee **grup zasobów**.
   
    ![Przeglądaj grup zasobów](./media/resource-group-portal/browse-groups.png)
2. Wybierz toocreate pustej grupy zasobów, **Dodaj**.
   
    ![Dodaj grupę zasobów](./media/resource-group-portal/add-resource-group.png)
3. Podaj nazwę i lokalizację hello nową grupę zasobów. Wybierz pozycję **Utwórz**.
   
    ![Utwórz grupę zasobów](./media/resource-group-portal/create-empty-group.png)
4. Może być konieczne tooselect **Odśwież** grupy zasobów toosee hello niedawno utworzona.
   
    ![Odśwież grupę zasobów](./media/resource-group-portal/refresh-resource-groups.png)
5. Wybierz toocustomize hello informacje wyświetlane dla grupy zasobów, **kolumn**.
   
    ![Dostosowywanie kolumn](./media/resource-group-portal/select-columns.png)
6. Wybierz hello tooadd kolumny, a następnie wybierz **aktualizacji**.
   
    ![Dodawanie kolumn](./media/resource-group-portal/add-columns.png)
7. toolearn dotyczących wdrażania zasobów tooyour nową grupę zasobów, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).
8. Szybki dostęp tooa grupy zasobów można przypiąć hello bloku tooyour w pulpicie nawigacyjnym.
   
    ![Grupa zasobów numeru PIN](./media/resource-group-portal/pin-group.png)
9. pulpit nawigacyjny Hello Wyświetla hello grupy zasobów i jego zasoby. Można wybrać grupy zasobów hello lub dowolną z jego element toohello toonavigate zasobów.
   
    ![Grupa zasobów numeru PIN](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Tag zasobów
Można stosować grup tooresource tagów i toologically zasobów organizowania zasobów. Informacje o pracy z tagami, zobacz [używanie tagów tooorganize zasobów platformy Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Monitorowanie zasobów
Po wybraniu zasobu bloku zasobów hello przedstawia domyślne wykresów i tabel do monitorowania tego typu zasobu.

1. Wybierz hello zasobów i zwróć uwagę, **monitorowanie** sekcji. Zawiera wykresy toohello odpowiedniego typu zasobu. Witaj poniższej ilustracji przedstawiono domyślne hello monitorowania danych dla konta magazynu.
   
    ![Pokaż monitorowania](./media/resource-group-portal/show-monitoring.png)
2. Części pulpitu nawigacyjnego tooyour bloku hello można przypiąć, wybierając hello wielokropek (...) powyżej hello sekcji. Można również dostosować hello rozmiar hello części bloku hello lub całkowicie usunąć. Witaj Poniższa ilustracja przedstawia przykładowy sposób dostosować toopin, lub usuń hello procesora CPU i pamięci sekcji.
   
    ![sekcja numeru PIN](./media/resource-group-portal/pin-cpu-section.png)
3. Po przypięciu pulpitu nawigacyjnego toohello sekcji hello, zobaczysz hello podsumowania na powitania pulpitu nawigacyjnego. I wybierając ją od razu przejście toomore szczegóły hello danych.
   
    ![widok pulpitu nawigacyjnego](./media/resource-group-portal/view-startboard.png)
4. toocompletely dostosować hello danych monitorowania za pośrednictwem portalu hello, przejdź tooyour domyślnego pulpitu nawigacyjnego i wybierz **nowego pulpitu nawigacyjnego**.
   
    ![pulpit nawigacyjny](./media/resource-group-portal/dashboard.png)
5. Nadaj nazwę nowego pulpitu nawigacyjnego i przeciągnij Kafelki na pulpicie nawigacyjnym hello. Kafelki Hello są filtrowane według różnych opcji.
   
    ![pulpit nawigacyjny](./media/resource-group-portal/create-dashboard.png)
   
     toolearn o pracy z pulpitów nawigacyjnych, zobacz [tworzenie i udostępnianie pulpitów nawigacyjnych w portalu Azure hello](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Zarządzanie zasobami
W bloku hello zasobu widać hello opcje zarządzania hello zasobów. Hello portal przedstawia opcje zarządzania dla tego typu zasobu. Widzisz polecenia zarządzania hello hello górze bloku zasobów hello i po lewej stronie powitania.

![Zarządzanie zasobami](./media/resource-group-portal/manage-resources.png)

Z tych opcji można wykonywać operacje, takie jak uruchamianie i zatrzymywanie maszyny wirtualnej lub ponownej konfiguracji właściwości hello hello maszyny wirtualnej.

## <a name="move-resources"></a>Przenoszenie zasobów
Aby uzyskać grupy zasobów tooanother zasobów toomove lub inną subskrypcję, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](resource-group-move-resources.md).

## <a name="lock-resources"></a>Blokowanie zasobów
Można zablokować subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów. Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Wyświetlanie Twoich subskrypcji i kosztów
Można wyświetlić informacji o subskrypcji i hello zestawienia kosztów dla wszystkich zasobów. Wybierz **subskrypcje** i subskrypcji hello ma toosee. Może mieć tylko jeden tooselect subskrypcji.

![subskrypcja](./media/resource-group-portal/select-subscription.png)

W bloku subskrypcji hello zobacz temat ocena wydajności.

![współczynnik spalania](./media/resource-group-portal/burn-rate.png)

I podziału kosztów według typów zasobów.

![koszt zasobów](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Eksportowanie szablonu
Po skonfigurowaniu grupy zasobów, można szablonu usługi Resource Manager hello tooview hello grupy zasobów. Eksportowanie szablonu hello oferuje dwie korzyści:

1. Można łatwo automatyzować przyszłych wdrożeń hello rozwiązania, ponieważ szablon hello zawiera wszystkie hello całej infrastruktury.
2. Należy zaznajomić o składni szablonu analizując hello JavaScript Object Notation (JSON) reprezentujący rozwiązania.

Aby uzyskać instrukcje, zobacz [szablonu eksportu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Usuń grupę zasobów lub zasobów
Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów hello w nim zawarte. Można również usunąć pojedynczych zasobów w grupie zasobów. Ma tooexercise ostrożność podczas usuwania grupy zasobów, ponieważ innych grup zasobów, które są połączone tooit może być zasobów. Menedżer zasobów nie powoduje usunięcia połączonych zasobów, ale ich nie może działać poprawnie bez hello oczekiwano zasobów.

![Usuwanie grupy](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz dzienniki aktywności tooview, [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).
* tooview szczegóły dotyczące wdrożenia, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
* Zobacz zasoby toodeploy za pośrednictwem portalu hello [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](resource-group-template-deploy-portal.md).
* toomanage tooresources dostępu, zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

