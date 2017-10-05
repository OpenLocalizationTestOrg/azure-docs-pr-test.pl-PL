---
title: "Rejestrowanie aplikacji z punktem końcowym v2.0 usługi Azure AD przy użyciu portalu | Dokumentacja firmy Microsoft"
description: "Jak zarejestrować aplikację w firmie Microsoft za włączanie logowania i uzyskiwanie dostępu do usług firmy Microsoft przy użyciu punktu końcowego v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="c8467-103">Jak zarejestrować aplikację z punktem końcowym v2.0</span><span class="sxs-lookup"><span data-stu-id="c8467-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="c8467-104">Do tworzenia aplikacji, która akceptuje zarówno zarządzanych kont usług, jak i usługi Azure AD logowanie, musisz najpierw zarejestrować aplikację w firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8467-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="c8467-105">W tej chwili nie można używać żadnych istniejących aplikacji, które mogą wiązać Ciebie z usługi Azure AD lub MSA — należy utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="c8467-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="c8467-106">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="c8467-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="c8467-107">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c8467-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="c8467-108">Odwiedź portal rejestracji aplikacji firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="c8467-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="c8467-109">Przede wszystkim najpierw - przejdź do [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="c8467-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="c8467-110">Jest to nowy portal rejestracji aplikacji, gdzie zarządzalnych aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8467-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="c8467-111">Zaloguj się przy użyciu albo osobistego lub służbowe konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8467-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="c8467-112">Jeśli nie masz albo utworzyć nowe konto osobiste.</span><span class="sxs-lookup"><span data-stu-id="c8467-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="c8467-113">Teraz, nie potrwa długo — poczekamy tutaj.</span><span class="sxs-lookup"><span data-stu-id="c8467-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="c8467-114">Zrobić?</span><span class="sxs-lookup"><span data-stu-id="c8467-114">Done?</span></span> <span data-ttu-id="c8467-115">Powinny teraz można patrzy listę aplikacji firmy Microsoft, który jest prawdopodobnie puste.</span><span class="sxs-lookup"><span data-stu-id="c8467-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="c8467-116">Ta funkcja pozwala zmienić.</span><span class="sxs-lookup"><span data-stu-id="c8467-116">Let's change that.</span></span>

<span data-ttu-id="c8467-117">Kliknij przycisk **Dodaj aplikację**i nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="c8467-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="c8467-118">Portalu przypisze globalnie unikatowy identyfikator aplikacji, który będzie potrzebny później w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8467-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="c8467-119">Jeśli aplikacja zawiera składnik po stronie serwera wymaga tokenów dostępu dla wywołania interfejsów API (wziąć pod uwagę: Office, Azure lub własnego interfejsu API sieci web), należy utworzyć **klucz tajny aplikacji** również w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c8467-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="c8467-120">Następnie dodaj platformy, które będą korzystać z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8467-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="c8467-121">W przypadku aplikacji sieci web, podaj **identyfikator URI przekierowania** wysyłania komunikatów do logowania.</span><span class="sxs-lookup"><span data-stu-id="c8467-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="c8467-122">Dla aplikacji mobilnych skopiuj domyślny przekierowania uri utworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c8467-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="c8467-123">Opcjonalnie można dostosować wygląd i działanie strony logowania w sekcji profilu.</span><span class="sxs-lookup"><span data-stu-id="c8467-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="c8467-124">Upewnij się, że **zapisać** przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="c8467-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="c8467-125">Po utworzeniu aplikacji przy użyciu [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), aplikacja zostanie zarejestrowana w domu dzierżawy konta, którego używasz do logowania się do portalu.</span><span class="sxs-lookup"><span data-stu-id="c8467-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="c8467-126">Oznacza to, że nie można zarejestrować aplikację w dzierżawie usługi Azure AD za pomocą osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8467-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="c8467-127">Jeśli chcesz jawnie zarejestrować aplikację w określonym dzierżawcy, zaloguj się przy użyciu konta pierwotnie utworzone w tej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="c8467-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="c8467-128">Tworzenie aplikacji szybki start</span><span class="sxs-lookup"><span data-stu-id="c8467-128">Build a quick start app</span></span>
<span data-ttu-id="c8467-129">Teraz, gdy masz aplikacji firmy Microsoft, można wykonać jedną z naszych samouczków szybkiego startu v2.0.</span><span class="sxs-lookup"><span data-stu-id="c8467-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="c8467-130">Poniżej przedstawiono kilka zaleceń:</span><span class="sxs-lookup"><span data-stu-id="c8467-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

