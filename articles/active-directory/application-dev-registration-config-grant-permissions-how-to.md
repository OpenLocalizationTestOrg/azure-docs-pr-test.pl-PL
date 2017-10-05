---
title: "Jak można udzielić uprawnienia do aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft"
description: "Jak można przyznać uprawnień dostępu do aplikacji utworzonych niestandardowych za pomocą portalu usługi Azure AD lub parametr adresu URL"
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
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="e412f-103">Jak można udzielić uprawnienia do aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e412f-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="e412f-104">Jeśli chcesz udzielić zgody preemptively w aplikacji lub są uruchomione, wystąpił błąd, który nie wyrażono zgodę dla aplikacji, spróbuj te czynności.</span><span class="sxs-lookup"><span data-stu-id="e412f-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="e412f-105">Jak wykonać zgody administratora aplikacji</span><span class="sxs-lookup"><span data-stu-id="e412f-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="e412f-106">Skutkuje to udzielania zgody do aplikacji dla wszystkich użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="e412f-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="e412f-107">Przejdź do **rejestracji aplikacji** bloku jako **administratora globalnego**, następnie wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="e412f-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="e412f-108">Wybierz **wymagane uprawnienia**, a na koniec trafienie **udzielanie uprawnień** u góry bloku.</span><span class="sxs-lookup"><span data-stu-id="e412f-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="e412f-109">Alternatywnie można utworzyć żądania *login.microsoftonline.com* z configs Twojej aplikacji i Dołącz na *& Monituj = admin\_zgody*.</span><span class="sxs-lookup"><span data-stu-id="e412f-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="e412f-110">Po zarejestrowaniu się przy użyciu poświadczeń administratora usługi, aplikacji udzielono zgody dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e412f-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="e412f-111">Jak wymusić zgody użytkownika dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="e412f-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="e412f-112">Dołącz do uwierzytelniania żądań *& Monituj = zgody* co wymaga zgody zawsze uwierzytelniają użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="e412f-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e412f-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e412f-113">Next steps</span></span>

[<span data-ttu-id="e412f-114">Integrowanie aplikacji AzureAD i zgody</span><span class="sxs-lookup"><span data-stu-id="e412f-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="e412f-115">Permissioning dla AzureAD w wersji 2.0 i zgody zbieżność aplikacji</span><span class="sxs-lookup"><span data-stu-id="e412f-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="e412f-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="e412f-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
