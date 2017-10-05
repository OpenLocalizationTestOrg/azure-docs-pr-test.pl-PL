---
title: Problem z tworzeniem aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Jak rozwiązywać problemy dotyczące tworzenia aplikacji serwera Proxy aplikacji w portalu usługi Azure AD administratora"
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="edab3-103">Problem z tworzeniem aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="edab3-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="edab3-104">Poniżej przedstawiono niektóre typowe problemy krój osoby podczas tworzenia nowej aplikacji serwera proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="edab3-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="edab3-105">Zalecane dokumenty</span><span class="sxs-lookup"><span data-stu-id="edab3-105">Recommended documents</span></span> 

<span data-ttu-id="edab3-106">Aby dowiedzieć się więcej na temat tworzenia aplikacji serwera Proxy aplikacji za pośrednictwem portalu administratora, zobacz [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="edab3-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="edab3-107">Jeśli są następujące kroki w tym dokumencie i uzyskiwania błąd podczas tworzenia aplikacji, zobacz szczegóły błędu, aby uzyskać informacje i sugestie dotyczące sposobu usunięcia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="edab3-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="edab3-108">Większość komunikaty o błędach obejmują sugerowanej poprawki.</span><span class="sxs-lookup"><span data-stu-id="edab3-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="edab3-109">Określone czynności do wykonania</span><span class="sxs-lookup"><span data-stu-id="edab3-109">Specific things to check</span></span>

<span data-ttu-id="edab3-110">Aby uniknąć typowych błędów, sprawdzić:</span><span class="sxs-lookup"><span data-stu-id="edab3-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="edab3-111">Administratorzy z uprawnieniami do tworzenia aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="edab3-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="edab3-112">Wewnętrzny adres URL jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="edab3-112">The internal URL is unique</span></span>

-   <span data-ttu-id="edab3-113">Zewnętrzny adres URL jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="edab3-113">The external URL is unique</span></span>

-   <span data-ttu-id="edab3-114">Adresy URL rozpoczynać się od http lub https i kończyć się "/"</span><span class="sxs-lookup"><span data-stu-id="edab3-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="edab3-115">Adres URL powinien być nazwą domeny, a nie adres IP</span><span class="sxs-lookup"><span data-stu-id="edab3-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="edab3-116">Komunikat o błędzie powinien być wyświetlany w prawym górnym rogu podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="edab3-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="edab3-117">Możesz również wybrać ikonę powiadomienia, aby wyświetlić komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="edab3-117">You can also select the notification icon to see the error messages.</span></span>

   ![Wiersz powiadomień](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="edab3-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="edab3-119">Next steps</span></span>
[<span data-ttu-id="edab3-120">Włącz serwer Proxy aplikacji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="edab3-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
