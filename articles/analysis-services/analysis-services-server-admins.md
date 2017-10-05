---
title: "Zarządzanie Administratorzy serwera w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać Administratorzy serwera dla serwera usług Analysis Services na platformie Azure."
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="d1dc5-103">Administratorzy serwerów zarządzania</span><span class="sxs-lookup"><span data-stu-id="d1dc5-103">Manage server administrators</span></span>
<span data-ttu-id="d1dc5-104">Administratorzy serwera musi być prawidłowa nazwa użytkownika lub grupy w usłudze Azure Active Directory (Azure AD) dla dzierżawcy, w której znajduje się serwer.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="d1dc5-105">Można użyć **Administratorzy usług analizy** w bloku kontroli serwera w portalu Azure lub właściwości serwera w programie SSMS administratorom serwerów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="d1dc5-106">Aby dodać administratorom serwerów przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d1dc5-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="d1dc5-107">W bloku formantu serwera, kliknij przycisk **Administratorzy usług analizy**.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="d1dc5-108">W  **\<nazwa_serwera > — Administratorzy usług analizy** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="d1dc5-109">W **dodać administratorom serwerów** bloku, wybierz kont użytkowników z usługi Azure AD lub zaprosić użytkowników zewnętrznych za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administratorzy serwera w portalu Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="d1dc5-111">Aby dodać administratorom serwerów przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="d1dc5-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="d1dc5-112">Kliknij prawym przyciskiem myszy serwer > **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="d1dc5-113">W **właściwości serwera analiz**, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="d1dc5-114">Kliknij przycisk **Dodaj**, a następnie wprowadź adres e-mail dla użytkownika lub grupy w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1dc5-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Dodawanie administratorów serwera w programie SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="d1dc5-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1dc5-116">Next steps</span></span> 
[<span data-ttu-id="d1dc5-117">Uwierzytelnianie i uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="d1dc5-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="d1dc5-118">Zarządzanie ról bazy danych i użytkowników</span><span class="sxs-lookup"><span data-stu-id="d1dc5-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="d1dc5-119">Kontrola dostępu oparta na rolach</span><span class="sxs-lookup"><span data-stu-id="d1dc5-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

