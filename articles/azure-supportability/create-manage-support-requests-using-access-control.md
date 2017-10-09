---
title: "toocontrol kontroli dostępu opartej na rolach (RBAC) aaaAzure toocreate prawa dostępu i zarządzanie żądaniami obsługi | Dokumentacja firmy Microsoft"
description: "Azure toocontrol kontroli dostępu opartej na rolach (RBAC) toocreate prawa dostępu i zarządzanie żądaniami obsługi"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure toocontrol kontroli dostępu opartej na rolach (RBAC) toocreate prawa dostępu i zarządzanie żądaniami obsługi

[Kontrola dostępu oparta na rolach (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure.
Obsługuje żądania tworzenia w hello portalu Azure, [portal.azure.com](https://portal.azure.com), używa toodefine modelu RBAC platformy Azure, który można utworzyć i zarządzanie żądaniami obsługi.
Dostęp przez przypisanie hello odpowiednie RBAC roli toousers, grup i aplikacji na niektórych zakresu, który może być subskrypcji, grupy zasobów lub zasobu.

Spójrzmy na przykład: jako właściciel grupy zasobów z uprawnienia do odczytu w zakresie subskrypcji hello, można zarządzać wszystkie zasoby hello w grupie zasobów hello, takie jak witryny sieci Web, maszyn wirtualnych i podsieci.
Jednak podczas toocreate żądania pomocy technicznej przed hello zasobu maszyny wirtualnej, wystąpi następujący błąd hello

![Błąd subskrypcji](./media/create-manage-support-requests-using-access-control/subscription-error.png)

W przystawce Zarządzanie żądania obsługi musisz mieć uprawnienia zapisu lub roli, która ma hello obsługuje akcji Microsoft.Support/* toocreate stanie zakresu toobe hello subskrypcji i zarządzanie żądaniami obsługi.

Hello poniższego artykułu wyjaśniono, jak używać niestandardowych toocreate kontroli dostępu opartej na rolach (RBAC) platformy Azure i zarządzanie żądaniami obsługi w hello portalu Azure.

## <a name="getting-started"></a>Wprowadzenie

Za pomocą powyższego przykładu hello, będzie możliwe toocreate żądania pomocy technicznej dla zasobu Jeśli niestandardową rolę RBAC subskrypcji hello zostały przypisane przez właściciela subskrypcji hello.
[Niestandardowe role RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) można tworzyć przy użyciu programu Azure PowerShell, interfejsu wiersza polecenia platformy Azure (CLI) i hello interfejsu API REST.

Właściwość Hello akcji niestandardowej roli zabezpieczeń określa hello Azure operacji toowhich hello rola przyznaje dostęp.
toocreate niestandardowej roli zabezpieczeń do zarządzania żądania pomocy technicznej, rola hello musi mieć hello akcji Microsoft.Support/*

Oto przykład niestandardowej roli zabezpieczeń można użyć toocreate i zarządzanie żądaniami obsługi.
Firma Microsoft nazwanego tej roli "Współautor żądania pomocy technicznej" i to, jak firma Microsoft można znaleźć toohello rola niestandardowa w tym artykule.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Wykonaj kroki hello opisane w temacie [ten film](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn jak toocreate niestandardowej roli zabezpieczeń dla Twojej subskrypcji.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Tworzenie i zarządzanie żądaniami obsługi w hello portalu Azure

Spójrzmy na przykład — Witaj właścicielem subskrypcji "Programu Visual Studio subskrypcji MSDN."
Jan jest z elementu równorzędnego jest toosome właściciela zasobu, hello grup zasobów w ramach tej subskrypcji, która ma subskrypcji toohello uprawnienia do odczytu.
Chcesz toogive dostępu tooyour równorzędnej, Jan, hello możliwości toocreate i zarządzanie biletami pomocy technicznej dla hello zasobów w ramach tej subskrypcji.

1. pierwszym krokiem Hello jest toogo toohello subskrypcji i w obszarze "Ustawienia" można wyświetlić listę użytkowników. Kliknij hello użytkownika Jan, kto ma dostęp czytnika na powitania subskrypcji i umożliwia przypisanie nowych toohim niestandardowej roli zabezpieczeń.

    ![Dodaj rolę](./media/create-manage-support-requests-using-access-control/add-role.png)

2. W bloku "Użytkownicy" hello, kliknij przycisk "Dodaj". Wybierz hello niestandardowej roli "Współautor żądania pomocy technicznej" z listy hello ról

    ![Dodaj rolę współautora pomocy technicznej](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Po wybraniu hello Nazwa roli, kliknij przycisk "Dodaj użytkowników", a następnie wprowadź poświadczenia e-mail hello Jan. Kliknij przycisk "Wybierz"

    ![Dodawanie użytkowników](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Kliknij przycisk "Ok" tooproceed

    ![Dodaj dostęp](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Spowoduje to wyświetlenie hello użytkownik z nowo dodanego rola niestandardowa "Obsługa współautora żądanie" w ramach subskrypcji hello, dla którego jesteś właścicielem hello hello

    ![Użytkownik dodany](./media/create-manage-support-requests-using-access-control/user-added.png)

    Jan rejestruje się w portalu hello, widzi on hello toowhich subskrypcji, który został on dodany.

7. Jan klika w bloku "Pomoc i obsługa" hello "Nowe żądanie pomocy technicznej" i może utworzyć żądania pomocy technicznej dla "Programu Visual Studio Ultimate z subskrypcją MSDN"

    ![Nowe żądanie pomocy technicznej](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Klikając przycisk "Obsługuje wszystkie żądania" Jan wyświetlana lista żądań pomocy technicznej utworzonych dla tej subskrypcji hello ![przypadku widoku szczegółów](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Usuń dostęp żądania pomocy technicznej w hello portalu Azure

Tak samo, jak to możliwe toogrant dostępu tooa użytkownika toocreate i zarządzanie żądaniami obsługi, jest możliwe tooremove dostępu dla użytkownika hello również.
tooremove hello toocreate możliwości i zarządzanie żądaniami obsługi, przejdź toohello subskrypcji, kliknij pozycję "Ustawienia" i kliknij przycisk hello użytkownika (w tym przypadku Jan).
Kliknij prawym przyciskiem myszy nazwę roli Witaj, "Współautora żądania pomocy technicznej" i kliknij przycisk Usuń,

![Usuń obsługę żądania dostępu](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Gdy Jan dzienniki w portalu toohello i próbuje toocreate żądania pomocy technicznej, wykryje on hello następujący błąd

![Subskrypcja błąd-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Jan nie widzą żadnych obsługuje żądania, po kliknięciu przycisku "Obsługuje wszystkie żądania"

![Wyświetl szczegóły sprawy-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
