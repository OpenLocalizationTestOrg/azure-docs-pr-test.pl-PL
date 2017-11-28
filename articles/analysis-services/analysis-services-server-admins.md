---
title: "Administratorzy serwera aaaManage w usług Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Administratorzy serwera toomanage dla serwera usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="3ad0b-103">Administratorzy serwerów zarządzania</span><span class="sxs-lookup"><span data-stu-id="3ad0b-103">Manage server administrators</span></span>
<span data-ttu-id="3ad0b-104">Administratorzy serwera musi być z prawidłowym użytkownikiem lub grupą w hello Azure Active Directory (Azure AD) dla dzierżawcy hello, w których hello znajduje się serwer.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="3ad0b-105">Można użyć **Administratorzy usług analizy** w bloku kontroli powitania serwera w portalu Azure lub właściwości serwera w administratorom serwerów toomanage SSMS.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="3ad0b-106">tooadd administratorom serwerów przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3ad0b-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="3ad0b-107">W bloku kontroli powitania serwera, kliknij przycisk **Administratorzy usług analizy**.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="3ad0b-108">W hello  **\<nazwa_serwera > — Administratorzy usług analizy** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="3ad0b-109">W hello **dodać administratorom serwerów** bloku, wybierz kont użytkowników z usługi Azure AD lub zaprosić użytkowników zewnętrznych za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administratorzy serwera w portalu Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="3ad0b-111">tooadd administratorom serwerów przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="3ad0b-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="3ad0b-112">Kliknij prawym przyciskiem myszy serwer hello > **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="3ad0b-113">W **właściwości serwera analiz**, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="3ad0b-114">Kliknij przycisk **Dodaj**, a następnie wprowadź adres e-mail powitania dla użytkownika lub grupy w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ad0b-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Dodawanie administratorów serwera w programie SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="3ad0b-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ad0b-116">Next steps</span></span> 
[<span data-ttu-id="3ad0b-117">Uwierzytelnianie i uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="3ad0b-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="3ad0b-118">Zarządzanie ról bazy danych i użytkowników</span><span class="sxs-lookup"><span data-stu-id="3ad0b-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="3ad0b-119">Kontrola dostępu oparta na rolach</span><span class="sxs-lookup"><span data-stu-id="3ad0b-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

