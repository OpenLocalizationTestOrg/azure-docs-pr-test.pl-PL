---
title: "aaaCharacteristics usługi Azure Active Directory dzierżawy intercaction | Dokumentacja firmy Microsoft"
description: "Zarządzanie dzierżawcom dzierżawy usługi Azure Active zrozumienie dzierżawcom jako całkowicie niezależne zasoby"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Zrozumienie, jak wiele dzierżaw usługi Azure Active Directory interakcji

W usłudze Azure Active Directory (Azure AD), każdej dzierżawy jest pełni niezależnym zasobem: elementu równorzędnego, który jest logicznie niezależny od hello innych dzierżawców, którymi zarządzasz. Nie ma żadnej zależności nadrzędny podrzędny między dzierżawcami. Ta niezależność między dzierżawcami obejmuje niezależność zasobów, niezależność administracyjną i niezależność synchronizacji.

## <a name="resource-independence"></a>Niezależność zasobów
* Jeśli utworzysz lub usuniesz zasób w jednym dzierżawy go nie ma wpływu na wszystkich zasobów w innej dzierżawie, z hello częściowym wyjątkiem dotyczącym zewnętrznych użytkowników. 
* Jeśli używasz nazwy domeny z jednej dzierżawy nie można używać z innymi dzierżawami.

## <a name="administrative-independence"></a>Niezależność administracyjna
Jeśli użytkownika niebędącego administratorem dzierżawy "Contoso" utworzy dzierżawy testowej "Test", następnie:

* Domyślnie program hello użytkownik, który tworzy dzierżawcy jest dodawana jako użytkownik zewnętrzny w tej nowej dzierżawy i hello przypisaną rolę administratora globalnego w tej dzierżawie.
* Administratorzy dzierżawy "Contoso" Hello mieć nie bezpośrednich uprawnień administracyjnych tootenant "Test", chyba że administrator "Test" jawnie nada im odpowiednie uprawnienia. Jednak Administratorzy "Contoso" mogą kontrolować dostęp tootenant "Test", jeśli ich kontroli konta użytkownika hello utworzony "Test".
* Jeśli należy usunąć rolę administratora dla użytkownika w jednym dzierżawy, zmiany hello nie nie wpływają na role administratora hello hello ten użytkownik ma w innej dzierżawie.

## <a name="synchronization-independence"></a>Niezależność synchronizacji
Można skonfigurować każdego Azure AD niezależnie dzierżawy tooget synchronizowania danych z jednego wystąpienia każdej:

* Narzędzie Hello Azure AD Connect toosynchronize danych z pojedynczym lasem usługi AD.
* Witaj dzierżawy usługi Azure Active łącznik dla programu Forefront Identity Manager, toosynchronize dane z jedną lub więcej lokalnymi lasami i/lub źródeł danych innych niż Azure AD.

## <a name="add-an-azure-ad-tenant"></a>Dodaj dzierżawa usługi Azure AD
tooadd dzierżawa usługi Azure AD w hello portalu Azure, zaloguj się za[hello portalu Azure](https://portal.azure.com) przy użyciu konta administratora globalnego usługi Azure AD, a po lewej stronie powitania, wybierz **nowy**.

> [!NOTE]
> W przeciwieństwie do innych zasobów platformy Azure dzierżawcy nie są zasobami podrzędnymi subskrypcji platformy Azure. Jeśli subskrypcja platformy Azure jest anulowane lub wygasła, dane dzierżawcy przy użyciu programu Azure PowerShell, hello interfejsu API Graph platformy Azure lub Centrum administracyjnego usługi Office 365 hello nadal są dostępne. Można również skojarzyć inną subskrypcję z dzierżawcą hello.
>

## <a name="next-steps"></a>Następne kroki
Zawiera ogólne omówienie usługi Azure AD licencjonowania problemów i najlepsze rozwiązania dla [co to jest dzierżawy usługi Azure Active licencjonowania?](active-directory-licensing-whatis-azure-portal.md)
