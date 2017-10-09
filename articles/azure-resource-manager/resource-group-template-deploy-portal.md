---
title: "aaaUse toodeploy portalu Azure zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj portalu Azure i usługi Azure Resource Manager toodeploy zasobów."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Deploy resources with Resource Manager templates and Azure portal (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i witryny Azure Portal)
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interfejs wiersza polecenia platformy Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [Interfejs API REST](resource-group-template-deploy-rest.md)
> 
> 

W tym temacie przedstawiono sposób toouse hello [portalu Azure](https://portal.azure.com) z [usługi Azure Resource Manager](resource-group-overview.md) toodeploy zasobów platformy Azure. toolearn dotyczące zarządzania zasobami, zobacz [zasobów Azure zarządzania za pośrednictwem portalu](resource-group-portal.md).

Obecnie nie wszystkie usługi obsługuje portalu hello lub Menedżera zasobów. W przypadku tych usług należy toouse hello [klasyczny portal](https://manage.windowsazure.com). Witaj stan każdej usługi, zobacz [wykresu dostępności portalu Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Tworzenie grupy zasobów
1. Wybierz toocreate pustej grupy zasobów, **nowy** > **zarządzania** > **grupy zasobów**.
   
    ![Tworzenie pustej grupy zasobów](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Nadaj nazwę i lokalizację, a w razie potrzeby wybierz subskrypcję. Należy tooprovide lokalizację dla grupy zasobów hello, ponieważ hello grupy zasobów są przechowywane metadane dotyczące hello zasobów. Ze względu na zgodność można toospecify przechowywania tych metadanych. Ogólnie rzecz biorąc firma Microsoft zaleca, aby określić lokalizację, w której będą znajdować się większość zasobów. Przy użyciu hello sam lokalizacji może uprościć szablonu.
   
    ![zestaw wartości grupy](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Wdrażanie zasobów z witryny Marketplace
Po utworzeniu grupy zasobów, można wdrożyć tooit zasoby z hello Marketplace. Hello Marketplace udostępnia wstępnie zdefiniowane rozwiązań dla typowych scenariuszy.

1. toostart wdrożenia, wybierz **nowy** i hello typ zasobu ma toodeploy. Następnie, poszukaj dla określonej wersji hello zasobu hello chcesz toodeploy.
   
    ![Wdrażanie zasobów](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Jeśli nie ma hello danego rozwiązania, które chcesz toodeploy, możesz wyszukać hello Marketplace go.
   
    ![Wyszukiwanie w witrynie marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. W zależności od typu wybranego zasobu hello masz kolekcję tooset odpowiednie właściwości przed przystąpieniem do wdrożenia. Te opcje nie są wyświetlane w tym miejscu, zgodnie z ich różnić w zależności od typu zasobu. Dla wszystkich typów należy wybrać grupę zasobu docelowego. następujące Hello obraz przedstawia sposób toocreate aplikacji sieci web i wdróż je utworzoną grupę zasobów toohello.
   
    ![Utwórz grupę zasobów](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Alternatywnie można określić toocreate grupę zasobów, w przypadku wdrażania zasobów. Wybierz **Utwórz nowy** i nadaj nazwę grupy zasobów hello.
   
    ![Utwórz nową grupę zasobów](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Rozpoczyna się wdrożenia. Witaj wdrażania może potrwać kilka minut. Po zakończeniu wdrażania hello zostanie wyświetlone powiadomienie.
   
    ![Wyświetl powiadomienie](./media/resource-group-template-deploy-portal/view-notification.png)
5. Po wdrożeniu zasobów, można dodać więcej grupy zasobów toohello zasobów za pomocą hello **Dodaj** polecenia w bloku grupy zasobów hello.
   
    ![dodawanie zasobu](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Wdrażanie zasobów z szablonu niestandardowego
Tooexecute wdrożenia, ale nie używane szablony hello w hello Marketplace, można utworzyć szablon niestandardowy, który definiuje infrastrukturę Twojego rozwiązania hello. toolearn o tworzeniu szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).

1. Wybierz szablon niestandardowy za pośrednictwem portalu hello toodeploy **nowy**i rozpocząć wyszukiwanie **wdrażania szablonu** dopóki nie zostanie ona wybrana, korzystając z opcji hello.
   
    ![Wdrażanie szablonu wyszukiwania](./media/resource-group-template-deploy-portal/search-template.png)
2. Wybierz **wdrażania szablonu** z hello dostępnych zasobów.
   
    ![Wybierz szablon wdrażania](./media/resource-group-template-deploy-portal/select-template.png)
3. Po uruchomieniu hello szablonu wdrażania, otwórz hello pustego szablonu, dostępnej dostosowywania.
   
    ![Tworzenie szablonu](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    W edytorze hello Dodaj składni JSON hello definiujący hello zasoby, które chcesz toodeploy. Wybierz **zapisać** po zakończeniu. Aby uzyskać wskazówki dotyczące pisania hello składni JSON, zobacz [Przewodnik po szablonie usługi Resource Manager](resource-manager-template-walkthrough.md).
   
    ![edytowanie szablonu](./media/resource-group-template-deploy-portal/edit-template.png)
4. Umożliwia wybranie istniejącego szablonu z hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/). Te szablony są tworzone przez społeczność hello. Obejmują one wielu typowych scenariuszy, a ktoś dodany szablon, który jest podobne toowhat próbujesz toodeploy. Można wyszukiwać toofind szablony hello odpowiadającego danego scenariusza.
   
    ![Wybierz szablon szybkiego startu](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    W edytorze hello można wyświetlić hello wybranego szablonu.
5. Po podaniu hello wszystkie inne wartości, wybierz **Utwórz** toodeploy hello szablonu. 
   
    ![wdrażanie szablonu](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Wdrażanie zasobów z szablonu zapisane tooyour konta
Hello portal umożliwia toosave tooyour szablonu konto platformy Azure i wdróż go ponownie później. Aby uzyskać więcej informacji na temat pracy z tych szablonów, zapisanych [Rozpoczynanie pracy z szablonami prywatnymi w portalu Azure hello](../marketplace-consumer/mytemplates-getstarted.md).

1. Wybierz zapisane szablony toofind **Przeglądaj** > **szablony**.
   
    ![Przeglądaj szablony](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Z listy hello zapisane konto tooyour szablony wybierz hello co chcesz toowork na.
   
    ![zapisane szablony](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Wybierz **Wdróż** tooredeploy zapisany szablon.
   
    ![zapisany szablon wdrażania](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Następne kroki
* Dzienniki inspekcji tooview, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).
* błędy wdrożenia tootroubleshoot, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
* tooretrieve szablonu z wdrożenia lub grupy zasobów, zobacz [szablonu eksportu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

