---
title: aaaProblem tworzenia aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Jak tootroubleshoot problemy tworzenia aplikacji serwera Proxy aplikacji w portalu usługi Azure AD administratora hello"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="9b146-103">Problem z tworzeniem aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b146-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="9b146-104">Poniżej przedstawiono niektóre typowe problemy hello krój osoby podczas tworzenia nowej aplikacji serwera proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b146-104">Below are some of hello common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="9b146-105">Zalecane dokumenty</span><span class="sxs-lookup"><span data-stu-id="9b146-105">Recommended documents</span></span> 

<span data-ttu-id="9b146-106">Zobacz toolearn więcej informacji na temat tworzenia aplikacji serwera Proxy aplikacji za pośrednictwem portalu administracyjnego hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9b146-106">toolearn more about creating an Application Proxy application through hello Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="9b146-107">Jeśli są następujące kroki hello w tym dokumencie i uzyskiwania błąd podczas tworzenia aplikacji hello, zobacz szczegóły błędu hello informacji i sugestie dotyczące sposobu toofix hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b146-107">If you are following hello steps in that document and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="9b146-108">Większość komunikaty o błędach obejmują sugerowanej poprawki.</span><span class="sxs-lookup"><span data-stu-id="9b146-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-toocheck"></a><span data-ttu-id="9b146-109">Określone informacje toocheck</span><span class="sxs-lookup"><span data-stu-id="9b146-109">Specific things toocheck</span></span>

<span data-ttu-id="9b146-110">Sprawdź tooavoid typowych błędów:</span><span class="sxs-lookup"><span data-stu-id="9b146-110">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="9b146-111">Administratorzy z toocreate uprawnienia aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b146-111">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="9b146-112">wewnętrzny adres URL Hello jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="9b146-112">hello internal URL is unique</span></span>

-   <span data-ttu-id="9b146-113">zewnętrzny adres URL Hello jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="9b146-113">hello external URL is unique</span></span>

-   <span data-ttu-id="9b146-114">Witaj adresy URL rozpoczyna się od http lub https i kończyć się "/"</span><span class="sxs-lookup"><span data-stu-id="9b146-114">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="9b146-115">adres URL Hello powinna być nazwą domeny, a nie adres IP</span><span class="sxs-lookup"><span data-stu-id="9b146-115">hello URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="9b146-116">komunikat o błędzie Hello powinien być wyświetlany w prawym górnym rogu hello podczas tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9b146-116">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="9b146-117">Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="9b146-117">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Wiersz powiadomień](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="9b146-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b146-119">Next steps</span></span>
[<span data-ttu-id="9b146-120">Włącz serwer Proxy aplikacji w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="9b146-120">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
