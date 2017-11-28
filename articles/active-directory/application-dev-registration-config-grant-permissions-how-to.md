---
title: aaaHow toogrant uprawnienia tooa opracowany niestandardowych aplikacji | Dokumentacja firmy Microsoft
description: "Jak toogrant tooyour uprawnienia niestandardowe rozwiniętych hello aplikacji przy użyciu portalu usługi Azure AD lub parametr adresu URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="841ca-103">Jak toogrant tooa uprawnienia niestandardowe opracowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="841ca-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="841ca-104">Zgody toogrant preemptively w aplikacji lub wystąpił błąd działają, że nie wyrażono zgodę tooan aplikacji, spróbuj te czynności.</span><span class="sxs-lookup"><span data-stu-id="841ca-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="841ca-105">Jak tooperform zgody administratora aplikacji</span><span class="sxs-lookup"><span data-stu-id="841ca-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="841ca-106">To ustawienie działa hello udzielania zgody toohello aplikacji dla wszystkich użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="841ca-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="841ca-107">Przejdź toohello **rejestracji aplikacji** bloku jako **administratora globalnego**, a następnie wybierz pozycję aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="841ca-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="841ca-108">Wybierz **wymagane uprawnienia**, a na koniec trafienie hello **udzielanie uprawnień** u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="841ca-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="841ca-109">Alternatywnie można konstruować żądanie zbyt*login.microsoftonline.com* z configs Twojej aplikacji i Dołącz na *& Monituj = admin\_zgody*.</span><span class="sxs-lookup"><span data-stu-id="841ca-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="841ca-110">Po zarejestrowaniu się przy użyciu poświadczeń administratora, aplikacja hello udzielono zgody dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="841ca-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="841ca-111">Jak tooforce zgody użytkownika dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="841ca-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="841ca-112">Dołącz do uwierzytelniania żądań *& Monituj = zgody* który żądania tooconsent użytkowników końcowych za każdym razem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="841ca-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="841ca-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="841ca-113">Next steps</span></span>

[<span data-ttu-id="841ca-114">Integrowanie aplikacji i zgody tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="841ca-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="841ca-115">Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji</span><span class="sxs-lookup"><span data-stu-id="841ca-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="841ca-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="841ca-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
