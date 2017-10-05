---
title: "Rozpoczynanie pracy z usługą Azure AD w projektach Visual Studio WebApi | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę przy użyciu usługi Azure Active Directory w projektach WebApi po nawiązywania połączenia lub utworzenie usługi Azure AD przy użyciu programu Visual Studio połączenia usługi"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="8943d-103">Get Started with Azure Active Directory i programu Visual Studio połączone usługi (WebApi projekty)</span><span class="sxs-lookup"><span data-stu-id="8943d-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8943d-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8943d-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="8943d-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="8943d-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="8943d-106">Wymaganie uwierzytelniania do kontrolerów dostępu</span><span class="sxs-lookup"><span data-stu-id="8943d-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="8943d-107">Wszystkie kontrolery w projekcie zostały adorned z **autoryzacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="8943d-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="8943d-108">Ten atrybut wymaga od użytkownika mają być uwierzytelniani przed uzyskaniem dostępu do interfejsów API zdefiniowany przez te kontrolery.</span><span class="sxs-lookup"><span data-stu-id="8943d-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="8943d-109">Aby umożliwić kontrolerowi można uzyskać dostępu do anonimowo, Usuń ten atrybut z kontrolera.</span><span class="sxs-lookup"><span data-stu-id="8943d-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="8943d-110">Aby ustawić uprawnienia na poziomie bardziej szczegółowego, należy zastosować atrybut do każdej metody, która wymaga uwierzytelnienia, zamiast stosować go do klasy kontrolera.</span><span class="sxs-lookup"><span data-stu-id="8943d-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8943d-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8943d-111">Next steps</span></span>
[<span data-ttu-id="8943d-112">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8943d-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

