---
title: Plik testowy Sipi | Dokumentacja firmy Microsoft
description: "Plik testu Aby sprawdzić ReadyForTest zależności"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="1b5e5-103">Plik testowy Sipi</span><span class="sxs-lookup"><span data-stu-id="1b5e5-103">Sipi test file</span></span>

<span data-ttu-id="1b5e5-104">Ten samouczek szybkiego startu pomaga zarejestrować aplikację w dzierżawie usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="1b5e5-105">Kiedy skończysz, Twoja aplikacja będzie zarejestrowana do użycia w dzierżawie usługi Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b5e5-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1b5e5-106">Prerequisites</span></span>

<span data-ttu-id="1b5e5-107">Aby utworzyć aplikację, która akceptuje tworzenie kont i logowanie użytkowników, musisz najpierw zarejestrować aplikację w dzierżawie usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="1b5e5-108">Aby utworzyć własną dzierżawę, wykonaj kroki opisane w temacie [Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b5e5-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="1b5e5-109">Aplikacje utworzone w bloku Azure AD B2C w witrynie Azure Portal muszą być zarządzane z tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="1b5e5-110">Jeśli edytujesz aplikacje B2C przy użyciu programu PowerShell lub innego portalu, stają się one nieobsługiwane i przestają działać w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="1b5e5-111">Szczegóły możesz znaleźć w sekcji [Uszkodzone aplikacje](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="1b5e5-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="1b5e5-112">Przechodzenie do ustawień usługi B2C</span><span class="sxs-lookup"><span data-stu-id="1b5e5-112">Navigate to B2C settings</span></span>

<span data-ttu-id="1b5e5-113">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/) jako administrator globalny dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="1b5e5-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="1b5e5-114">Wybierz następne kroki na podstawie rejestrowanego typu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="1b5e5-114">Choose next steps based on the application type you are registering:</span></span>
