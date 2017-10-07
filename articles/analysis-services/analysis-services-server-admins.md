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
# <a name="manage-server-administrators"></a>Administratorzy serwerów zarządzania
Administratorzy serwera musi być z prawidłowym użytkownikiem lub grupą w hello Azure Active Directory (Azure AD) dla dzierżawcy hello, w których hello znajduje się serwer. Można użyć **Administratorzy usług analizy** w bloku kontroli powitania serwera w portalu Azure lub właściwości serwera w administratorom serwerów toomanage SSMS. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>tooadd administratorom serwerów przy użyciu portalu Azure
1. W bloku kontroli powitania serwera, kliknij przycisk **Administratorzy usług analizy**.
2. W hello  **\<nazwa_serwera > — Administratorzy usług analizy** bloku, kliknij przycisk **Dodaj**.
3. W hello **dodać administratorom serwerów** bloku, wybierz kont użytkowników z usługi Azure AD lub zaprosić użytkowników zewnętrznych za pomocą adresu e-mail.

    ![Administratorzy serwera w portalu Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>tooadd administratorom serwerów przy użyciu narzędzia SSMS
1. Kliknij prawym przyciskiem myszy serwer hello > **właściwości**.
2. W **właściwości serwera analiz**, kliknij przycisk **zabezpieczeń**.
3. Kliknij przycisk **Dodaj**, a następnie wprowadź adres e-mail powitania dla użytkownika lub grupy w usługi Azure AD.
   
    ![Dodawanie administratorów serwera w programie SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Następne kroki 
[Uwierzytelnianie i uprawnienia użytkownika](analysis-services-manage-users.md)  
[Zarządzanie ról bazy danych i użytkowników](analysis-services-database-users.md)  
[Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md)  

