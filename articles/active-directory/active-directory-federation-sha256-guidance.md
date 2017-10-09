---
title: "Algorytm wyznaczania wartości skrótu podpisu aaaChange dla zaufania jednostki uzależnionej usługi Office 365 | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera wskazówki dotyczące zmieniania algorytm SHA relacja zaufania federacji z usługą Office 365"
keywords: "SHA1, SHA256, usługi O365, federacyjnych, aadconnect, usług AD FS, usługi ad fs, sha zmian relacji zaufania federacji, zaufanie jednostki uzależnionej"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="38a46-104">Zmień algorytm wyznaczania wartości skrótu podpisu dla usługi Office 365 zaufanie jednostki uzależnionej</span><span class="sxs-lookup"><span data-stu-id="38a46-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="38a46-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="38a46-105">Overview</span></span>
<span data-ttu-id="38a46-106">Active Directory Federation Services (AD FS) podpisuje jego tooensure usługi Azure Active Directory tooMicrosoft tokenów nie może być naruszona z.</span><span class="sxs-lookup"><span data-stu-id="38a46-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="38a46-107">Podpis może bazować na SHA1 lub SHA256.</span><span class="sxs-lookup"><span data-stu-id="38a46-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="38a46-108">Usługa Azure Active Directory obsługuje teraz tokeny podpisane przy użyciu algorytmu skrótu SHA256 i zaleca się ustawienie hello podpisywania tokenu algorytmu tooSHA256 hello najwyższy poziom zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="38a46-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="38a46-109">W tym artykule opisano kroki hello potrzebne toohello algorytm podpisywania tokenu hello tooset lepiej zabezpieczyć poziom SHA256.</span><span class="sxs-lookup"><span data-stu-id="38a46-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="38a46-110">Firma Microsoft zaleca użycie SHA256 jako hello algorytmu podpisywania tokenów jest bezpieczniejsza niż SHA1, ale wciąż obsługiwaną opcją SHA1.</span><span class="sxs-lookup"><span data-stu-id="38a46-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="38a46-111">Zmień algorytm podpisywania tokenu hello</span><span class="sxs-lookup"><span data-stu-id="38a46-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="38a46-112">Po ustawieniu hello algorytm podpisu z jednym z dwóch procesów hello poniżej, usługi AD FS podpisuje hello tokeny dla usługi Office 365 z SHA256 zaufanie jednostki uzależnionej.</span><span class="sxs-lookup"><span data-stu-id="38a46-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="38a46-113">Nie ma potrzeby toomake wszelkie dodatkowe zmiany, a ta zmiana nie ma wpływu na Twoje tooaccess możliwości usługi Office 365 lub innych aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a46-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="38a46-114">Konsoli zarządzania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="38a46-114">AD FS management console</span></span>
1. <span data-ttu-id="38a46-115">Otwórz konsolę zarządzania FS hello AD na powitania głównej usługi AD FS serwera.</span><span class="sxs-lookup"><span data-stu-id="38a46-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="38a46-116">Rozwiń węzeł, hello AD FS, a następnie kliknij przycisk **zaufania jednostek uzależnionych**.</span><span class="sxs-lookup"><span data-stu-id="38a46-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="38a46-117">Kliknij prawym przyciskiem myszy programu Office 365/Azure zaufania jednostki uzależnionej, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="38a46-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="38a46-118">Wybierz hello **zaawansowane** kartę i wybierz hello skrótu secure hash algorithm SHA256.</span><span class="sxs-lookup"><span data-stu-id="38a46-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="38a46-119">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="38a46-119">Click **OK**.</span></span>

![Algorytm podpisywania SHA256--programu MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="38a46-121">Polecenia cmdlet programu AD FS programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="38a46-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="38a46-122">Na dowolnym serwerze usług AD FS Otwórz program PowerShell w obszarze uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="38a46-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="38a46-123">Zestaw hello skrótu secure hash algorithm przy użyciu hello **Set-AdfsRelyingPartyTrust** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38a46-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="38a46-124">Zobacz temat</span><span class="sxs-lookup"><span data-stu-id="38a46-124">Also read</span></span>
* [<span data-ttu-id="38a46-125">Napraw zaufania usługi Office 365 z programem Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="38a46-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

