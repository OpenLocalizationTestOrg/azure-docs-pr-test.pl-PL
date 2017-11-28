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
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="96409-103">Zrozumienie, jak wiele dzierżaw usługi Azure Active Directory interakcji</span><span class="sxs-lookup"><span data-stu-id="96409-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="96409-104">W usłudze Azure Active Directory (Azure AD), każdej dzierżawy jest pełni niezależnym zasobem: elementu równorzędnego, który jest logicznie niezależny od hello innych dzierżawców, którymi zarządzasz.</span><span class="sxs-lookup"><span data-stu-id="96409-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="96409-105">Nie ma żadnej zależności nadrzędny podrzędny między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="96409-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="96409-106">Ta niezależność między dzierżawcami obejmuje niezależność zasobów, niezależność administracyjną i niezależność synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="96409-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="96409-107">Niezależność zasobów</span><span class="sxs-lookup"><span data-stu-id="96409-107">Resource independence</span></span>
* <span data-ttu-id="96409-108">Jeśli utworzysz lub usuniesz zasób w jednym dzierżawy go nie ma wpływu na wszystkich zasobów w innej dzierżawie, z hello częściowym wyjątkiem dotyczącym zewnętrznych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="96409-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="96409-109">Jeśli używasz nazwy domeny z jednej dzierżawy nie można używać z innymi dzierżawami.</span><span class="sxs-lookup"><span data-stu-id="96409-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="96409-110">Niezależność administracyjna</span><span class="sxs-lookup"><span data-stu-id="96409-110">Administrative independence</span></span>
<span data-ttu-id="96409-111">Jeśli użytkownika niebędącego administratorem dzierżawy "Contoso" utworzy dzierżawy testowej "Test", następnie:</span><span class="sxs-lookup"><span data-stu-id="96409-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="96409-112">Domyślnie program hello użytkownik, który tworzy dzierżawcy jest dodawana jako użytkownik zewnętrzny w tej nowej dzierżawy i hello przypisaną rolę administratora globalnego w tej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="96409-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="96409-113">Administratorzy dzierżawy "Contoso" Hello mieć nie bezpośrednich uprawnień administracyjnych tootenant "Test", chyba że administrator "Test" jawnie nada im odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="96409-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="96409-114">Jednak Administratorzy "Contoso" mogą kontrolować dostęp tootenant "Test", jeśli ich kontroli konta użytkownika hello utworzony "Test".</span><span class="sxs-lookup"><span data-stu-id="96409-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="96409-115">Jeśli należy usunąć rolę administratora dla użytkownika w jednym dzierżawy, zmiany hello nie nie wpływają na role administratora hello hello ten użytkownik ma w innej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="96409-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="96409-116">Niezależność synchronizacji</span><span class="sxs-lookup"><span data-stu-id="96409-116">Synchronization independence</span></span>
<span data-ttu-id="96409-117">Można skonfigurować każdego Azure AD niezależnie dzierżawy tooget synchronizowania danych z jednego wystąpienia każdej:</span><span class="sxs-lookup"><span data-stu-id="96409-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="96409-118">Narzędzie Hello Azure AD Connect toosynchronize danych z pojedynczym lasem usługi AD.</span><span class="sxs-lookup"><span data-stu-id="96409-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="96409-119">Witaj dzierżawy usługi Azure Active łącznik dla programu Forefront Identity Manager, toosynchronize dane z jedną lub więcej lokalnymi lasami i/lub źródeł danych innych niż Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96409-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="96409-120">Dodaj dzierżawa usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96409-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="96409-121">tooadd dzierżawa usługi Azure AD w hello portalu Azure, zaloguj się za[hello portalu Azure](https://portal.azure.com) przy użyciu konta administratora globalnego usługi Azure AD, a po lewej stronie powitania, wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="96409-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="96409-122">W przeciwieństwie do innych zasobów platformy Azure dzierżawcy nie są zasobami podrzędnymi subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="96409-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="96409-123">Jeśli subskrypcja platformy Azure jest anulowane lub wygasła, dane dzierżawcy przy użyciu programu Azure PowerShell, hello interfejsu API Graph platformy Azure lub Centrum administracyjnego usługi Office 365 hello nadal są dostępne.</span><span class="sxs-lookup"><span data-stu-id="96409-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="96409-124">Można również skojarzyć inną subskrypcję z dzierżawcą hello.</span><span class="sxs-lookup"><span data-stu-id="96409-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="96409-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96409-125">Next steps</span></span>
<span data-ttu-id="96409-126">Zawiera ogólne omówienie usługi Azure AD licencjonowania problemów i najlepsze rozwiązania dla [co to jest dzierżawy usługi Azure Active licencjonowania?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="96409-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
