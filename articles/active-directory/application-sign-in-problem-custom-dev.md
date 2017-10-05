---
title: Problemy przy logowaniu do aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft
description: "Typowe rrors, który może być przyczyną nie będą mogli zalogować się do aplikacji utworzonych w usłudze Azure AD"
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="44fc0-103">Problemy przy logowaniu do aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="44fc0-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="44fc0-104">Istnieje kilka błędów, które mogą być przyczyną nie będą mogli zalogować się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fc0-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="44fc0-105">Jest to problem podczas potyczki osób Przyczyna największych błędnie skonfigurowane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fc0-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="44fc0-106">Błędy związane z nieprawidłowej konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="44fc0-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="44fc0-107">Sprawdź, czy konfiguracje w portalu odpowiada mieć w Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fc0-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="44fc0-108">W szczególności porównaj identyfikator klienta/aplikacji, adresy URL odpowiedzi, klucze kluczy tajnych klienta i identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fc0-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="44fc0-109">Porównywanie zasobów jest żądanie dostępu do kodu przy użyciu uprawnień skonfigurowanych w **wymagane zasoby** kartę, aby upewnić się, że tylko żądania zasobów skonfigurowano.</span><span class="sxs-lookup"><span data-stu-id="44fc0-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="44fc0-110">Zobacz [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) dla podobnych jakichkolwiek problemów.</span><span class="sxs-lookup"><span data-stu-id="44fc0-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44fc0-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44fc0-111">Next steps</span></span>

[<span data-ttu-id="44fc0-112">Przewodnik dewelopera usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fc0-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="44fc0-113">Integrowanie aplikacji z usługą Azure AD i zgody</span><span class="sxs-lookup"><span data-stu-id="44fc0-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="44fc0-114">Permissioning dla usługi Azure AD w wersji 2.0 i zgody zbieżność aplikacji</span><span class="sxs-lookup"><span data-stu-id="44fc0-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="44fc0-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="44fc0-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
