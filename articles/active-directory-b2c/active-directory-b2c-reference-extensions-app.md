---
title: "Aplikacja rozszerzenia — usługa Azure AD B2C | Dokumentacja firmy Microsoft"
description: Przywracanie hello w b2c aplikacji rozszerzenia
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
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="f9958-103">Usługa Azure AD B2C: Rozszerzeń aplikacji</span><span class="sxs-lookup"><span data-stu-id="f9958-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="f9958-104">Podczas tworzenia katalogu usługi Azure AD B2C aplikacja o nazwie `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` jest tworzony automatycznie wewnątrz hello nowego katalogu.</span><span class="sxs-lookup"><span data-stu-id="f9958-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="f9958-105">Tej aplikacji, hello określonego tooas **b2c rozszerzeń aplikacji**, jest widoczny w *rejestracji aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="f9958-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="f9958-106">Jest on używany przez hello Azure AD B2C usługi toostore informacje o użytkownikach i atrybuty niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="f9958-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="f9958-107">Usunięcie aplikacji hello Azure AD B2C nie będzie działać prawidłowo, i będzie mieć wpływ na środowisko produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="f9958-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9958-108">Nie należy usuwać hello w b2c aplikacji rozszerzenia, chyba że planujesz tooimmediately delete dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f9958-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="f9958-109">Jeśli aplikacja hello pozostaje usunięte przez dłużej niż 30 dni, informacje o użytkowniku zostaną trwale utracone.</span><span class="sxs-lookup"><span data-stu-id="f9958-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="f9958-110">Weryfikowanie, aplikacja rozszerzenia hello jest obecny</span><span class="sxs-lookup"><span data-stu-id="f9958-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="f9958-111">występuje tooverify, który hello b2c rozszerzeń aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f9958-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="f9958-112">W dzierżawie usługi Azure AD B2C, kliknij **więcej usług** w menu nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="f9958-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="f9958-113">Wyszukaj i Otwórz **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f9958-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="f9958-114">Wyszukaj aplikację, która rozpoczyna się od **b2c rozszerzeń aplikacji**</span><span class="sxs-lookup"><span data-stu-id="f9958-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="f9958-115">Odzyskaj hello rozszerzeń aplikacji</span><span class="sxs-lookup"><span data-stu-id="f9958-115">Recover hello extensions app</span></span>

<span data-ttu-id="f9958-116">Jeśli przypadkowo usunięte hello w b2c aplikacji rozszerzeń, masz toorecover 30 dni go.</span><span class="sxs-lookup"><span data-stu-id="f9958-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="f9958-117">Możesz przywrócić aplikacji hello przy użyciu interfejsu API programu Graph hello:</span><span class="sxs-lookup"><span data-stu-id="f9958-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="f9958-118">Przeglądaj zbyt[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="f9958-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="f9958-119">Zaloguj się w witrynie toohello jako administratora globalnego dla katalogu usługi Azure AD B2C hello interesujące aplikacja hello usunięte toorestore dla.</span><span class="sxs-lookup"><span data-stu-id="f9958-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="f9958-120">Wystawiać HTTP GET dla adresu URL hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` z interfejsu api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="f9958-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="f9958-121">Upewnij się, że tooreplace `{tenantName}` nazwą Twojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f9958-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="f9958-122">Ta operacja spowoduje wyświetlenie listy wszystkich aplikacji hello, które zostały usunięte w ramach hello w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="f9958-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="f9958-123">Znajdź aplikacji hello liście hello gdzie hello nazwa rozpoczyna się od "ruch aplikacji b2c rozszerzenia" i skopiuj jej `objectid` wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="f9958-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="f9958-124">Wystawiać POST protokołu HTTP dla adresu URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="f9958-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="f9958-125">Zastąp hello `{OBJECTID}` część adresu URL hello z hello `objectid` hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="f9958-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="f9958-126">Powinny teraz być zbyt[aplikacja hello przywrócić](#verifying-that-the-extensions-app-is-present) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9958-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f9958-127">Aplikację można przywrócić tylko, jeśli został on usunięty w hello ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="f9958-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="f9958-128">Jeśli został on więcej niż 30 dni, dane zostaną trwale utracone.</span><span class="sxs-lookup"><span data-stu-id="f9958-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="f9958-129">Aby uzyskać pomoc pliku biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f9958-129">For more assistance, file a support ticket.</span></span>
