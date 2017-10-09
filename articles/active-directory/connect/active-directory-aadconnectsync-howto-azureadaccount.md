---
title: "Synchronizacja programu Azure AD Connect: jak konto usługi toomanage hello Azure AD | Dokumentacja firmy Microsoft"
description: "W tym temacie omówiono, jak konto usługi toorestore hello Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, w jaki sposób tooreset hello hasło dla hello synchronizacji Azure AD Connect konta usługi łącznika"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="249ef-104">Synchronizacja programu Azure AD Connect: jak konto usługi toomanage hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="249ef-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="249ef-105">usługi toobe wolnego powinien Hello konto usługi używane przez hello łącznika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="249ef-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="249ef-106">Jeśli potrzebujesz tooreset swoje poświadczenia, w tym temacie jest dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="249ef-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="249ef-107">Na przykład, jeśli Administrator globalny ma przez pomyłkę resetowania hello hasło konta usługi hello przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="249ef-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="249ef-108">Resetowanie poświadczeń hello</span><span class="sxs-lookup"><span data-stu-id="249ef-108">Reset hello credentials</span></span>
<span data-ttu-id="249ef-109">Jeśli konto usługi hello zdefiniowane na powitania łącznika usługi Azure AD nie można skontaktować się z usługi Azure AD powodu tooauthentication problemów, można zresetować hasła hello.</span><span class="sxs-lookup"><span data-stu-id="249ef-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="249ef-110">Zaloguj się na serwerze synchronizacji Azure AD Connect toohello i uruchom program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="249ef-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="249ef-111">Uruchom polecenie `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="249ef-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="249ef-112">![Addadsyncaadserviceaccount polecenia cmdlet programu PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="249ef-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="249ef-113">Podaj poświadczenia administratora globalnego usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="249ef-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="249ef-114">To polecenie cmdlet resetuje hello hasło dla konta usługi hello i zaktualizować go, zarówno w usłudze Azure AD, jak i w hello aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="249ef-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="249ef-115">Znane problemy można rozwiązać te kroki</span><span class="sxs-lookup"><span data-stu-id="249ef-115">Known issues these steps can solve</span></span>
<span data-ttu-id="249ef-116">W tej sekcji znajduje się lista błędów zgłaszanych przez klientów, które zostały usunięte przez poświadczenia, zresetuj na powitania konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="249ef-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="249ef-117">Zdarzenie 6900</span><span class="sxs-lookup"><span data-stu-id="249ef-117">Event 6900</span></span>  
<span data-ttu-id="249ef-118">Witaj serwer napotkał nieoczekiwany błąd podczas przetwarzania powiadomienia o zmianie hasła:</span><span class="sxs-lookup"><span data-stu-id="249ef-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="249ef-119">AADSTS70002: Błąd podczas sprawdzania poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="249ef-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="249ef-120">AADSTS50054: Stare hasło jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="249ef-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="249ef-121">Zdarzenie 659</span><span class="sxs-lookup"><span data-stu-id="249ef-121">Event 659</span></span>  
<span data-ttu-id="249ef-122">Błąd podczas pobierania konfiguracji synchronizacji zasad haseł.</span><span class="sxs-lookup"><span data-stu-id="249ef-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="249ef-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="249ef-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="249ef-124">AADSTS70002: Błąd podczas sprawdzania poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="249ef-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="249ef-125">AADSTS50054: Stare hasło jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="249ef-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="249ef-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="249ef-126">Next steps</span></span>
<span data-ttu-id="249ef-127">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="249ef-127">**Overview topics**</span></span>

* [<span data-ttu-id="249ef-128">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="249ef-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="249ef-129">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="249ef-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

