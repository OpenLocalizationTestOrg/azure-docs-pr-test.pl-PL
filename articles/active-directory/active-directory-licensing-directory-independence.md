---
title: "Właściwości usługi Azure Active Directory dzierżawy intercaction | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="6e851-103">Zrozumienie, jak wiele dzierżaw usługi Azure Active Directory interakcji</span><span class="sxs-lookup"><span data-stu-id="6e851-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="6e851-104">W usłudze Azure Active Directory (Azure AD), każdej dzierżawy jest pełni niezależnym zasobem: elementu równorzędnego, który jest logicznie niezależny od pozostałych dzierżawców, którymi zarządzasz.</span><span class="sxs-lookup"><span data-stu-id="6e851-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="6e851-105">Nie ma żadnej zależności nadrzędny podrzędny między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="6e851-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="6e851-106">Ta niezależność między dzierżawcami obejmuje niezależność zasobów, niezależność administracyjną i niezależność synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="6e851-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="6e851-107">Niezależność zasobów</span><span class="sxs-lookup"><span data-stu-id="6e851-107">Resource independence</span></span>
* <span data-ttu-id="6e851-108">Jeśli utworzysz lub usuniesz zasób w jednym dzierżawy go nie ma wpływu na wszystkich zasobów w innej dzierżawie, z częściowym wyjątkiem dotyczącym zewnętrznych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6e851-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="6e851-109">Jeśli używasz nazwy domeny z jednej dzierżawy nie można używać z innymi dzierżawami.</span><span class="sxs-lookup"><span data-stu-id="6e851-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="6e851-110">Niezależność administracyjna</span><span class="sxs-lookup"><span data-stu-id="6e851-110">Administrative independence</span></span>
<span data-ttu-id="6e851-111">Jeśli użytkownika niebędącego administratorem dzierżawy "Contoso" utworzy dzierżawy testowej "Test", następnie:</span><span class="sxs-lookup"><span data-stu-id="6e851-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="6e851-112">Domyślnie użytkownik tworzący dzierżawcy jest dodany jako użytkownik zewnętrzny w tej nowej dzierżawy i przypisano rolę administratora globalnego w tej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="6e851-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="6e851-113">Administratorzy dzierżawy "Contoso" ma nie bezpośrednich uprawnień administracyjnych do dzierżawy "Test", chyba że administrator "Test" jawnie nada im odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="6e851-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="6e851-114">Jednak Administratorzy "Contoso" mogą kontrolować dostęp do dzierżawy "Test", jeśli ich kontroli konta użytkownika, które utworzyło "Test".</span><span class="sxs-lookup"><span data-stu-id="6e851-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="6e851-115">Należy usunąć rolę administratora dla użytkownika w jednym dzierżawy, zmiana nie wpływa na ról administratora, które użytkownik ma w innej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="6e851-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="6e851-116">Niezależność synchronizacji</span><span class="sxs-lookup"><span data-stu-id="6e851-116">Synchronization independence</span></span>
<span data-ttu-id="6e851-117">Można skonfigurować każdej dzierżawy usługi Azure AD niezależnie w celu synchronizowania danych z jednego wystąpienia każdej:</span><span class="sxs-lookup"><span data-stu-id="6e851-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="6e851-118">Narzędzie Azure AD Connect, aby zsynchronizować dane z pojedynczym lasem usługi AD.</span><span class="sxs-lookup"><span data-stu-id="6e851-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="6e851-119">Dzierżawca usługi Azure Active łącznik dla programu Forefront Identity Manager, aby zsynchronizować dane z jednego lub więcej lokalnymi lasami i/lub źródeł danych innych niż Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e851-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="6e851-120">Dodaj dzierżawa usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e851-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="6e851-121">Aby dodać dzierżawa usługi Azure AD w portalu Azure, zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta administratora globalnego usługi Azure AD, a po lewej stronie, wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="6e851-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="6e851-122">W przeciwieństwie do innych zasobów platformy Azure dzierżawcy nie są zasobami podrzędnymi subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e851-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="6e851-123">Jeśli anulowania subskrypcji platformy Azure lub ważność, można nadal uzyskać dostępu do danych dzierżawy przy użyciu programu Azure PowerShell, interfejsu API Graph platformy Azure lub Centrum administracyjnego usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="6e851-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="6e851-124">Można również skojarzyć inną subskrypcję z dzierżawą.</span><span class="sxs-lookup"><span data-stu-id="6e851-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="6e851-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e851-125">Next steps</span></span>
<span data-ttu-id="6e851-126">Zawiera ogólne omówienie usługi Azure AD licencjonowania problemów i najlepsze rozwiązania dla [co to jest dzierżawy usługi Azure Active licencjonowania?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6e851-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
