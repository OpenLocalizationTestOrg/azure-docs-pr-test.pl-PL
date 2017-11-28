---
title: "aaaRegister aplikacji z punktem końcowym v2.0 hello Azure AD przy użyciu portalu hello | Dokumentacja firmy Microsoft"
description: "Jak usługi przy użyciu punktu końcowego v2.0 hello tooregister aplikacji z firmą Microsoft za włączanie logowania i uzyskiwania dostępu do firmy Microsoft"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="5b7a3-103">Jak tooregister aplikacji z punktem końcowym v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="5b7a3-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="5b7a3-104">toobuild aplikację, która akceptuje zarówno zarządzanych kont usług, jak i usługi Azure AD logowanie, musisz najpierw tooregister aplikacji z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="5b7a3-105">W tej chwili nie być możliwe toouse wszelkie istniejące aplikacje mogą wiązać Ciebie z usługi Azure AD lub MSA — należy toocreate brand nową.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="5b7a3-106">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="5b7a3-107">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5b7a3-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="5b7a3-108">Odwiedź portal rejestracji aplikacji Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="5b7a3-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="5b7a3-109">Przede wszystkim za Przejdź najpierw -[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="5b7a3-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="5b7a3-110">Jest to nowy portal rejestracji aplikacji, gdzie zarządzalnych aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="5b7a3-111">Zaloguj się przy użyciu albo osobistego lub służbowe konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="5b7a3-112">Jeśli nie masz albo utworzyć nowe konto osobiste.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="5b7a3-113">Teraz, nie potrwa długo — poczekamy tutaj.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="5b7a3-114">Zrobić?</span><span class="sxs-lookup"><span data-stu-id="5b7a3-114">Done?</span></span> <span data-ttu-id="5b7a3-115">Powinny teraz można patrzy listę aplikacji firmy Microsoft, który jest prawdopodobnie puste.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="5b7a3-116">Ta funkcja pozwala zmienić.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-116">Let's change that.</span></span>

<span data-ttu-id="5b7a3-117">Kliknij przycisk **Dodaj aplikację**i nadaj mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="5b7a3-118">Hello portal przypisze globalnie unikatowy identyfikator aplikacji, który będzie potrzebny później w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="5b7a3-119">Jeśli aplikacja zawiera składnik po stronie serwera wymaga tokenów dostępu dla wywołania interfejsów API (wziąć pod uwagę: Office, Azure lub własnego interfejsu API sieci web), należy toocreate **klucz tajny aplikacji** również w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="5b7a3-120">Następnie dodaj hello platformy, które będą korzystać z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="5b7a3-121">W przypadku aplikacji sieci web, podaj **identyfikator URI przekierowania** wysyłania komunikatów do logowania.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="5b7a3-122">Dla aplikacji mobilnych skopiuj domyślny hello przekierowania uri utworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="5b7a3-123">Opcjonalnie można dostosować hello wygląd i działanie strony logowania w hello profilu.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="5b7a3-124">Upewnij się, że tooclick **zapisać** przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="5b7a3-125">Po utworzeniu aplikacji przy użyciu [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello aplikacja zostanie zarejestrowana w dzierżawie macierzystego hello hello konta Użyj toosign hello portalu.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="5b7a3-126">Oznacza to, że nie można zarejestrować aplikację w dzierżawie usługi Azure AD za pomocą osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="5b7a3-127">Jeśli jawnie tooregister aplikacji w szczególności dzierżawy, zaloguj się przy użyciu konta, które pierwotnie utworzone w tej dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="5b7a3-128">Tworzenie aplikacji szybki start</span><span class="sxs-lookup"><span data-stu-id="5b7a3-128">Build a quick start app</span></span>
<span data-ttu-id="5b7a3-129">Teraz, gdy masz aplikacji firmy Microsoft, można wykonać jedną z naszych samouczków szybkiego startu v2.0.</span><span class="sxs-lookup"><span data-stu-id="5b7a3-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="5b7a3-130">Poniżej przedstawiono kilka zaleceń:</span><span class="sxs-lookup"><span data-stu-id="5b7a3-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

