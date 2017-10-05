---
title: "Jak wybrać uprawnienia dla danego interfejsu API | Dokumentacja firmy Microsoft"
description: "Jak znaleźć punkty końcowe uwierzytelniania dla aplikacji niestandardowej podczas tworzenia lub rejestrowania za pomocą usługi Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="74bb8-103">Jak wybrać uprawnienia dla danego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="74bb8-103">How to select permissions for a given API</span></span>

<span data-ttu-id="74bb8-104">Punkty końcowe uwierzytelniania można znaleźć aplikacji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74bb8-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="74bb8-105">Przejdź do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74bb8-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="74bb8-106">W okienku nawigacji po lewej stronie kliknij **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74bb8-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="74bb8-107">Kliknij przycisk **rejestracji aplikacji** i wybierz polecenie **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="74bb8-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="74bb8-108">To otwarcie **punkty końcowe** strony, tak aby wyświetlić listę wszystkich punktów końcowych uwierzytelniania dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="74bb8-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="74bb8-109">Użyj punktu końcowego, które są specyficzne dla protokołu uwierzytelniania, którego używasz, w połączeniu z Identyfikatorem aplikacji sformułować uwierzytelnianie żądań specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="74bb8-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74bb8-110">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74bb8-110">Next steps</span></span>
[<span data-ttu-id="74bb8-111">Przewodnik dewelopera usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74bb8-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
