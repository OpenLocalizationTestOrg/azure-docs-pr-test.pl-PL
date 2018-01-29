---
title: "Właściwości usługi Azure Active Directory dzierżawy interakcji | Dokumentacja firmy Microsoft"
description: "Zarządzanie dzierżawcom dzierżawy usługi Azure Active zrozumienie dzierżawcom jako całkowicie niezależne zasoby"
services: active-tenant
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/10/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 2c00f382546a0e5f1e9da9dc90777dcf9622ec94
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2018
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Zrozumienie, jak wiele dzierżaw usługi Azure Active Directory interakcji

W usłudze Azure Active Directory (Azure AD), każdy dzierżawca jest pełni niezależnym zasobem: elementu równorzędnego, który jest logicznie niezależny od pozostałych dzierżawców, którymi zarządzasz. Nie ma żadnej zależności nadrzędny podrzędny między dzierżawcami. Ta niezależność między dzierżawcami obejmuje niezależność zasobów, niezależność administracyjną i niezależność synchronizacji.

## <a name="resource-independence"></a>Niezależność zasobów
* Jeśli utworzysz lub usuniesz zasób w jednym dzierżawy go nie ma wpływu na wszystkich zasobów w innej dzierżawie, z częściowym wyjątkiem dotyczącym zewnętrznych użytkowników. 
* Jeśli używasz nazwy domeny z jednej dzierżawy nie można używać z innymi dzierżawami.

## <a name="administrative-independence"></a>Niezależność administracyjna
Jeśli użytkownika niebędącego administratorem dzierżawy "Contoso" utworzy dzierżawy testowej "Test", następnie:

* Domyślnie użytkownik tworzący dzierżawcy jest dodany jako użytkownik zewnętrzny w tej nowej dzierżawy i przypisano rolę administratora globalnego w tej dzierżawie.
* Administratorzy dzierżawy "Contoso" ma nie bezpośrednich uprawnień administracyjnych do dzierżawy "Test", chyba że administrator "Test" jawnie nada im odpowiednie uprawnienia. Jednak Administratorzy "Contoso" mogą kontrolować dostęp do dzierżawy "Test", jeśli ich kontroli konta użytkownika, które utworzyło "Test".
* Należy usunąć rolę administratora dla użytkownika w jednym dzierżawy, zmiana nie wpływa na ról administratora, które użytkownik ma w innej dzierżawie.

## <a name="synchronization-independence"></a>Niezależność synchronizacji
Można skonfigurować każdej dzierżawy usługi Azure AD niezależnie w celu synchronizowania danych z jednego wystąpienia każdej:

* Narzędzie Azure AD Connect, aby zsynchronizować dane z pojedynczym lasem usługi AD.
* Dzierżawca usługi Azure Active łącznik dla programu Forefront Identity Manager, aby zsynchronizować dane z jednego lub więcej lokalnymi lasami i/lub źródeł danych innych niż Azure AD.

## <a name="add-an-azure-ad-tenant"></a>Dodaj dzierżawa usługi Azure AD
Aby dodać dzierżawa usługi Azure AD w portalu Azure, zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta administratora globalnego usługi Azure AD, a po lewej stronie, wybierz **nowy**.

> [!NOTE]
> W przeciwieństwie do innych zasobów platformy Azure dzierżawcy nie są zasobami podrzędnymi subskrypcji platformy Azure. Jeśli anulowania subskrypcji platformy Azure lub ważność, można nadal uzyskać dostępu do danych dzierżawy przy użyciu programu Azure PowerShell, interfejsu API Graph platformy Azure lub Centrum administracyjnego usługi Office 365. Możesz również [skojarzyć inną subskrypcję z dzierżawcą](active-directory-how-subscriptions-associated-directory.md).
>

## <a name="next-steps"></a>Kolejne kroki
Zawiera ogólne omówienie usługi Azure AD licencjonowania problemów i najlepsze rozwiązania dla [co to jest dzierżawy usługi Azure Active licencjonowania?](active-directory-licensing-whatis-azure-portal.md).
