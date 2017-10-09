---
title: aaaAzure AD v2 Windows Desktop wprowadzenie - Config | Dokumentacja firmy Microsoft
description: "Jak aplikacji .NET pulpitu systemu Windows (XAML) można uzyskać tokenu dostępu i wywołania funkcji API chronione przez punkt końcowy w wersji 2 usługi Azure Active Directory. | Microsoft Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="77a6e-104">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="77a6e-104">Create an application (Express)</span></span>
<span data-ttu-id="77a6e-105">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="77a6e-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="77a6e-106">Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="77a6e-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="77a6e-107">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="77a6e-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="77a6e-108">Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji</span><span class="sxs-lookup"><span data-stu-id="77a6e-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="77a6e-109">Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="77a6e-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="77a6e-110">Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="77a6e-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="77a6e-111">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="77a6e-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="77a6e-112">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji</span><span class="sxs-lookup"><span data-stu-id="77a6e-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="77a6e-113">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="77a6e-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="77a6e-114">Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="77a6e-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="77a6e-115">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="77a6e-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="77a6e-116">Skopiuj identyfikator aplikacji hello identyfikator GUID, przejdź wstecz tooVisual Studio, otwórz `App.xaml.cs` i Zastąp `your_client_id_here` z hello został zarejestrowany identyfikator aplikacji:</span><span class="sxs-lookup"><span data-stu-id="77a6e-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
