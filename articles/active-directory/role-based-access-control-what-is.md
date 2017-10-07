---
title: "aaaManage dostępu i uprawnienia z RBAC - Azure RBAC | Dokumentacja firmy Microsoft"
description: "Rozpocznij zarządzanie dostępem przy użyciu kontroli dostępu opartej na rolach na platformie Azure w hello portalu Azure. Użyj uprawnień tooassign przypisania roli w katalogu."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Rozpoczynanie pracy z opartej na rolach kontrola dostępu w hello portalu Azure
Nastawionych zabezpieczeń skoncentrować się nadanie uprawnień dokładne hello potrzebnych im pracowników. Za dużo uprawnienia mogą uwidaczniać tooattackers konta. Za mało uprawnienia oznacza, że pracownicy nie można pobrać ich pracować wydajnie. Azure opartej na rolach kontroli dostępu (RBAC) pomaga rozwiązać ten problem, oferując precyzyjne zarządzanie dostępem dla platformy Azure.

Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań. Zamiast nadanie każdy nieograniczonych uprawnień w Twojej subskrypcji platformy Azure lub zasobów, można zezwolić tylko pewne akcje. Na przykład użyj RBAC toolet jednego pracownika zarządzania maszynami wirtualnymi w ramach subskrypcji, podczas gdy inny można zarządzać baz danych SQL w ramach hello takie same subskrypcji.

## <a name="basics-of-access-management-in-azure"></a>Podstawy zarządzania dostępem w systemie Azure
Każda subskrypcja platformy Azure jest skojarzony z jednego katalogu usługi Azure Active Directory (AD). Użytkownicy, grupy i aplikacje z katalogu mogą zarządzać zasobami w hello subskrypcji platformy Azure. Przypisz te prawa dostępu przy użyciu hello portalu Azure, narzędzi wiersza polecenia platformy Azure i interfejsów API zarządzania platformy Azure.

Udziel dostępu przypisując hello odpowiednie RBAC roli toousers, grup i aplikacji w określonego zakresu. Witaj zakres przypisania roli może być pojedynczego zasobu, grupy zasobów lub subskrypcji. Rola przypisana w zakresie nadrzędnej również udziela dostępu toohello dzieci w nim zawarte. Na przykład użytkownika z grupy zasobów tooa dostępu może zarządzać wszystkie zasoby hello, który zawiera, takie jak witryny sieci Web, maszyn wirtualnych i podsieci.

![Relacja między elementami usługi Azure Active Directory — diagram](./media/role-based-access-control-what-is/rbac_aad.png)

Hello RBAC rolę, którą należy przypisać decyduje, jakie zasoby hello użytkownika, grupy lub aplikacji można zarządzać w ramach tego zakresu.

## <a name="built-in-roles"></a>Wbudowane role
Azure RBAC ma trzy podstawowe role dotyczące typów zasobów tooall:

* **Właściciel** ma pełny dostęp tooall zasobów, w tym hello toodelegate prawo dostępu tooothers.
* **Współautor** można tworzyć i zarządzania wszystkimi typami zasobów platformy Azure, ale nie może udzielić dostępu tooothers.
* **Czytnik** można wyświetlić istniejących zasobów platformy Azure.

Zezwalaj na zarządzanie określonych zasobów platformy Azure Hello pozostałe role RBAC hello na platformie Azure. Na przykład hello roli współautora maszyny wirtualnej umożliwia hello toocreate użytkowników i zarządzania maszynami wirtualnymi. Nie daje im sieci wirtualnej toohello dostępu lub łączy się z podsieci hello, która hello maszyny wirtualnej. 

[Wbudowane role RBAC](role-based-access-built-in-roles.md) list hello ról dostępnej na platformie Azure. Określa operacje hello i że każdy wbudowana rola przyznaje toousers zakresu. Jeśli szukasz toodefine własne role, aby uzyskać większą kontrolę, zobacz temat jak toobuild [niestandardowych ról w Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Dziedziczenie hierarchii i dostęp do zasobów
* Każdy **subskrypcji** na platformie Azure należy tooonly jeden katalog. (Ale każdego katalogu mogą mieć więcej niż jedną subskrypcję).
* Każdy **grupy zasobów** należy tooonly jedną subskrypcję.
* Każdy **zasobów** należy tooonly jednej grupy zasobów.

Przyznaj na nadrzędne zakresy dostępu jest dziedziczone na zakresy podrzędne. Na przykład:

* Można przypisać grupy usługi Azure AD hello czytnika ról tooan w zakresie subskrypcji hello. Hello Członkowie tej grupy mogą wyświetlać każdej grupy zasobów i zasobów hello subskrypcji.
* Można przypisać hello współautora roli tooan aplikacji w zakresie grupy zasobów hello. Może on zarządzać zasoby wszystkich typów w tej grupie zasobów, ale nie innych grup zasobów w subskrypcji hello.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Azure RBAC, a administratorzy subskrypcji klasycznego
Klasyczni Administratorzy i współadministratorzy ma pełny dostęp toohello subskrypcji platformy Azure. Mogą zarządzać zasobów przy użyciu hello [portalu Azure](https://portal.azure.com) z interfejsów API usługi Azure Resource Manager lub hello [klasycznego portalu Azure](https://manage.windowsazure.com) i Azure klasycznego modelu wdrażania. W modelu RBAC hello klasycznego Administratorzy mają przypisaną rolę właściciela hello w zakresie subskrypcji hello.

Witaj portalu Azure, i tylko hello Obsługa nowych interfejsów API usługi Azure Resource Manager Azure RBAC. Użytkownicy i aplikacje, które są przypisane role RBAC nie można użyć portalu klasycznego zarządzania hello i hello Azure klasycznego modelu wdrażania.

## <a name="authorization-for-management-vs-data-operations"></a>Autoryzacji do zarządzania, a operacje na danych
Azure RBAC tylko operacje zarządzania obsługuje hello zasobów platformy Azure w hello portalu Azure i interfejsów API usługi Azure Resource Manager. Nie można go autoryzacji wszystkie operacje poziomu danych zasobów platformy Azure. Na przykład ktoś autoryzować toomanage kont magazynu, ale nie toohello obiektów blob lub tabel w ramach konta magazynu. Podobnie bazy danych SQL mogą być zarządzane, ale nie hello tabel znajdujące się w nim.

## <a name="next-steps"></a>Następne kroki
* Rozpoczynanie pracy z [opartej na rolach kontrola dostępu w portalu Azure hello](role-based-access-control-configure.md).
* Zobacz hello [wbudowane role RBAC](role-based-access-built-in-roles.md)
* Definiowanie własnych [niestandardowych ról dla kontroli dostępu opartej na rolach na platformie Azure](role-based-access-control-custom-roles.md)
