---
title: Plik testowy Sipi | Dokumentacja firmy Microsoft
description: "Testowanie plików toocheck ReadyForTest zależności"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="f627e-103">Plik testowy Sipi</span><span class="sxs-lookup"><span data-stu-id="f627e-103">Sipi test file</span></span>

<span data-ttu-id="f627e-104">Ten samouczek szybkiego startu pomaga zarejestrować aplikację w dzierżawie usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="f627e-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="f627e-105">Po zakończeniu aplikacji są rejestrowane w dzierżawie powitalnych Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="f627e-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f627e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f627e-106">Prerequisites</span></span>

<span data-ttu-id="f627e-107">toobuild aplikację, która akceptuje konsumenta rejestracji i logowania, należy najpierw aplikacji hello tooregister z dzierżawy usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="f627e-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="f627e-108">Utworzyć własną dzierżawę za pomocą hello czynności opisane w temacie [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f627e-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="f627e-109">Musi być zarządzane aplikacje utworzone za pomocą bloku hello Azure AD B2C w portalu Azure hello z hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f627e-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="f627e-110">Po zmodyfikowaniu aplikacji B2C hello przy użyciu programu PowerShell lub innego portalu stają się nieobsługiwane i nie działają usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f627e-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="f627e-111">Zobacz szczegóły w hello [wystąpił błąd aplikacji](#faulted-apps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="f627e-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="f627e-112">Przejdź do ustawień tooB2C</span><span class="sxs-lookup"><span data-stu-id="f627e-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="f627e-113">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) jako Administrator globalny dzierżawy hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="f627e-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="f627e-114">Wybierz następne kroki na podstawie typu aplikacji hello, rejestrowany:</span><span class="sxs-lookup"><span data-stu-id="f627e-114">Choose next steps based on hello application type you are registering:</span></span>
