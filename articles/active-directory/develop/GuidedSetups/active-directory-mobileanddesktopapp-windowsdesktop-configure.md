---
title: "Usługi Azure AD v2 Windows Desktop pobieranie rozpoczęte — Config | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="f39b5-104">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="f39b5-104">Create an application (Express)</span></span>
<span data-ttu-id="f39b5-105">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="f39b5-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="f39b5-106">Zarejestrować aplikację za pośrednictwem [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="f39b5-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="f39b5-107">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="f39b5-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="f39b5-108">Upewnij się, że zaznaczono opcję instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f39b5-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="f39b5-109">Postępuj zgodnie z instrukcjami, aby uzyskać identyfikator aplikacji i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="f39b5-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="f39b5-110">Dodaj swoje informacje rejestracyjne aplikacji do rozwiązania (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="f39b5-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="f39b5-111">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="f39b5-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="f39b5-112">Przejdź do [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) do rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="f39b5-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="f39b5-113">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="f39b5-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="f39b5-114">Upewnij się, że jest zaznaczona opcja instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f39b5-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="f39b5-115">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="f39b5-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="f39b5-116">Skopiuj identyfikator GUID w identyfikator aplikacji, wróć do programu Visual Studio, otwórz `App.xaml.cs` i Zastąp `your_client_id_here` z został zarejestrowany identyfikator aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f39b5-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
