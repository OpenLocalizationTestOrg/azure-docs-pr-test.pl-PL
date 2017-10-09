---
title: "na podstawie aaaRole kontroli dostępu w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Rozpocznij zarządzanie dostępem z opartej na rolach kontrola dostępu w portalu Azure hello. Użyj roli przypisania tooassign uprawnienia tooyour zasobów."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Korzystanie z kontroli dostępu opartej na rolach toomanage dostępu tooyour subskrypcji platformy Azure zasobów
> [!div class="op_single_selector"]
> * [Zarządzanie dostępem użytkowników lub grup](role-based-access-control-manage-assignments.md)
> * [Zarządzanie dostępem do zasobów](role-based-access-control-configure.md)

Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Przy użyciu funkcji RBAC, można udzielić tylko hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań. W tym artykule opisano, jak rozpocząć pracę z RBAC w hello portalu Azure. Jeśli chcesz uzyskać więcej szczegółowych informacji na temat sposobu, w jaki RBAC ułatwia zarządzanie dostępem, zobacz [Co to jest kontrola dostępu oparta na rolach](role-based-access-control-what-is.md).

W ramach każdej subskrypcji można przyznać się too2000 przypisań ról. 

## <a name="view-access"></a>Wyświetlanie dostępu
Można zobaczyć, kto ma dostęp do zasobów tooa, grupy zasobów lub subskrypcji z głównego bloku hello [portalu Azure](https://portal.azure.com). Na przykład chcemy toosee, kto ma dostęp tooone naszych grup zasobów:

1. Wybierz **grup zasobów** hello pasku nawigacyjnym po lewej stronie powitania.  
    ![Grupy zasobów — ikona](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Witaj wybierz nazwę grupy zasobów hello z hello **grup zasobów** bloku.
3. Wybierz **(IAM) kontroli dostępu** z menu po lewej stronie powitania.  
4. blok kontroli dostępu Hello zawiera listę wszystkich użytkowników, grup i aplikacji, które zostały przyznane grupy zasobów toohello dostępu.  
   
    ![Blok użytkowników — dostęp dziedziczony a przypisany (zrzut ekranu)](./media/role-based-access-control-configure/view-access.png)

Zwróć uwagę, zbyt ograniczone niektóre role**tego zasobu** a inne **dziedziczonych** go z innym zakresem. Dostępu jest przypisane w szczególności toohello grupy zasobów albo dziedziczony z subskrypcji nadrzędnej toohello przypisania.

> [!NOTE]
> Klasyczni Administratorzy i współadministratorzy są traktowani jako właściciele subskrypcji hello w nowym modelu RBAC hello.

## <a name="add-access"></a>Dodawanie dostępu
Można przyznać dostęp z wewnątrz hello zasobu, grupy zasobów lub subskrypcji, która jest zakresem hello hello przypisania roli.

1. Wybierz **Dodaj** w bloku kontroli dostępu hello.  
2. Czy chcesz tooassign z hello roli wybierz hello **wybierz rolę** bloku.
3. Wybierz użytkownika hello, grupę lub aplikację w katalogu, który ma dostęp toogrant do. Można przeszukiwać katalog hello o nazw wyświetlanych, adresów e-mail i identyfikatorów obiektów.  
   
    ![Blok dodawania użytkowników — zrzut ekranu wyszukiwania](./media/role-based-access-control-configure/grant-access2.png)
4. Wybierz **OK** toocreate hello przypisania. Witaj **Dodawanie użytkownika** podręcznego śledzi postęp hello.  
    ![Pasek postępu dodawania użytkownika — zrzut ekranu](./media/role-based-access-control-configure/addinguser_popup.png)

Po pomyślnym dodaniu przypisania roli, pojawi się na powitania **użytkowników** bloku.

## <a name="remove-access"></a>Usuwanie dostępu
1. Wskaźnik nad hello nazwy przypisania hello, które mają tooremove. Pole wyboru zostanie wyświetlona nazwa toohello dalej.
2. Użyj hello tooselect pola wyboru jednego lub więcej przypisań ról.
2. Wybierz pozycję **Usuń**.  
3. Wybierz **tak** tooconfirm hello usuwania.

Przypisań dziedziczonych nie można usunąć. Tooremove dziedziczone przypisania, należy należy toodo go na powitania zakresu, której utworzono hello przypisania roli. W hello **zakres** kolumny, obok zbyt**dziedziczonych** jest łącze, które umożliwia przejście zasobów toohello gdy ta rola została przypisana. Przejście zasobu toohello podane przypisania roli hello tooremove.

![Blok Użytkownicy — dostęp dziedziczony wyłącza przycisk usuwania (zrzut ekranu)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Inne narzędzia toomanage dostępu
Można przypisywać role i Zarządzaj dostępem za pomocą poleceń Azure RBAC w narzędziach innych niż hello portalu Azure.  Wykonaj toolearn łącza hello więcej o warunkach wstępnych hello i wprowadzenie do poleceń Azure RBAC hello.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Interfejs wiersza polecenia platformy Azure](role-based-access-control-manage-access-azure-cli.md)
* [Interfejs API REST](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Następne kroki
* [Tworzenie raportu historii zmian dostępu](role-based-access-control-access-change-history-report.md)
* Zobacz hello [wbudowane role RBAC](role-based-access-built-in-roles.md)
* Definiowanie własnych [niestandardowych ról dla kontroli dostępu opartej na rolach na platformie Azure](role-based-access-control-custom-roles.md)

