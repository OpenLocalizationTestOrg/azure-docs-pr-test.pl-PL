---
title: "Aplikacja rozszerzenia — usługa Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Przywrócenie aplikacji rozszerzeń b2c"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: 17500b572a0e92c1c233c6967840a5b6d96e21cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="bc03f-103">Usługa Azure AD B2C: Rozszerzeń aplikacji</span><span class="sxs-lookup"><span data-stu-id="bc03f-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="bc03f-104">Podczas tworzenia katalogu usługi Azure AD B2C aplikacja o nazwie `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` jest tworzony automatycznie wewnątrz nowego katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc03f-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span></span> <span data-ttu-id="bc03f-105">Ta aplikacja, nazywany **b2c rozszerzeń aplikacji**, jest widoczny w *rejestracji aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="bc03f-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="bc03f-106">Jest on używany przez usługę Azure AD B2C do przechowywania informacji o użytkownikach i atrybuty niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="bc03f-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span></span> <span data-ttu-id="bc03f-107">Usunięcie aplikacji usługi Azure AD B2C nie będzie działać prawidłowo, i będzie mieć wpływ na środowisko produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="bc03f-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc03f-108">Nie należy usuwać aplikacji rozszerzeń b2c, jeśli zamierzasz natychmiast usunąć dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="bc03f-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span></span> <span data-ttu-id="bc03f-109">Jeśli aplikacja pozostaje usunięte przez dłużej niż 30 dni, informacje o użytkowniku zostaną trwale utracone.</span><span class="sxs-lookup"><span data-stu-id="bc03f-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-the-extensions-app-is-present"></a><span data-ttu-id="bc03f-110">Weryfikowanie, czy znajduje się w aplikacji rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="bc03f-110">Verifying that the extensions app is present</span></span>

<span data-ttu-id="bc03f-111">Aby sprawdzić, czy znajduje się w aplikacji rozszerzeń b2c:</span><span class="sxs-lookup"><span data-stu-id="bc03f-111">To verify that the b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="bc03f-112">W dzierżawie usługi Azure AD B2C, kliknij **więcej usług** w menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="bc03f-112">Inside your Azure AD B2C tenant, click on **More services** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="bc03f-113">Wyszukaj i Otwórz **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="bc03f-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="bc03f-114">Wyszukaj aplikację, która rozpoczyna się od **b2c rozszerzeń aplikacji**</span><span class="sxs-lookup"><span data-stu-id="bc03f-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-the-extensions-app"></a><span data-ttu-id="bc03f-115">Odzyskiwanie aplikacji rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="bc03f-115">Recover the extensions app</span></span>

<span data-ttu-id="bc03f-116">Jeśli przypadkowo usunięto aplikacji rozszerzeń b2c, masz 30 dni, aby go odzyskać.</span><span class="sxs-lookup"><span data-stu-id="bc03f-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span></span> <span data-ttu-id="bc03f-117">Możesz przywrócić aplikacji przy użyciu interfejsu API programu Graph:</span><span class="sxs-lookup"><span data-stu-id="bc03f-117">You can restore the app using the Graph API:</span></span>

1. <span data-ttu-id="bc03f-118">Przejdź do [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="bc03f-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="bc03f-119">Zaloguj się do witryny jako administrator globalny katalogu usługi Azure AD B2C, której chcesz przywrócić usuniętego aplikacji dla.</span><span class="sxs-lookup"><span data-stu-id="bc03f-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span></span>
1. <span data-ttu-id="bc03f-120">Wystawiać HTTP GET względem adresu URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` z interfejsu api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="bc03f-120">Issue an HTTP GET against the URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="bc03f-121">Upewnij się zastąpić `{tenantName}` nazwą Twojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="bc03f-121">Make sure to replace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="bc03f-122">Ta operacja spowoduje wyświetlenie listy wszystkich aplikacji, które zostały usunięte w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="bc03f-122">This operation will list all of the applications that have been deleted within the past 30 days.</span></span>
1. <span data-ttu-id="bc03f-123">Znajdź aplikację na liście, których nazwa rozpoczyna się od "ruch aplikacji b2c rozszerzenia" i skopiuj jej `objectid` wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="bc03f-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="bc03f-124">Wystawiać POST protokołu HTTP względem adresu URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="bc03f-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="bc03f-125">Zastąp `{OBJECTID}` część adresu URL z `objectid` z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="bc03f-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span></span> 

<span data-ttu-id="bc03f-126">Teraz powinno być możliwe do [przywróconej aplikacja](#verifying-that-the-extensions-app-is-present) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bc03f-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="bc03f-127">Aplikację można przywrócić tylko, jeśli został on usunięty w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="bc03f-127">An application can only be restored if it has been deleted within the last 30 days.</span></span> <span data-ttu-id="bc03f-128">Jeśli został on więcej niż 30 dni, dane zostaną trwale utracone.</span><span class="sxs-lookup"><span data-stu-id="bc03f-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="bc03f-129">Aby uzyskać pomoc pliku biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="bc03f-129">For more assistance, file a support ticket.</span></span>