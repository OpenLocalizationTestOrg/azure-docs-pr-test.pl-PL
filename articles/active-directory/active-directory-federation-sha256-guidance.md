---
title: "Zmień algorytm wyznaczania wartości skrótu podpisu dla zaufania jednostki uzależnionej usługi Office 365 | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="e2a6d-104">Zmień algorytm wyznaczania wartości skrótu podpisu dla usługi Office 365 zaufanie jednostki uzależnionej</span><span class="sxs-lookup"><span data-stu-id="e2a6d-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="e2a6d-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e2a6d-105">Overview</span></span>
<span data-ttu-id="e2a6d-106">Active Directory Federation Services (AD FS) podpisuje Microsoft Azure Active Directory w celu zapewnienia nie może zostać zmieniony z jego tokenów.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="e2a6d-107">Podpis może bazować na SHA1 lub SHA256.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="e2a6d-108">Azure Active Directory obsługuje teraz tokeny podpisane przy użyciu algorytmu skrótu SHA256 i zaleca się ustawienie algorytm podpisywania tokenu SHA256 najwyższego poziomu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="e2a6d-109">W tym artykule opisano kroki niezbędne do Ustaw poziom algorytm podpisywania tokenu do bardziej bezpieczne SHA256.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="e2a6d-110">Firma Microsoft zaleca użycie SHA256 jako algorytmu podpisywania tokenów jest bezpieczniejsza niż SHA1, ale wciąż obsługiwaną opcją SHA1.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="e2a6d-111">Zmień algorytm podpisywania tokenu</span><span class="sxs-lookup"><span data-stu-id="e2a6d-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="e2a6d-112">Po ustawieniu algorytm podpisu z jednego z dwóch poniższych procesów usług AD FS podpisuje tokeny dla usługi Office 365 z SHA256 zaufanie jednostki uzależnionej.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="e2a6d-113">Nie trzeba wprowadzać żadnych zmian konfiguracji dodatkowe, a ta zmiana nie ma wpływu na możliwość uzyskania dostępu do usługi Office 365 lub innych aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="e2a6d-114">Konsoli zarządzania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="e2a6d-114">AD FS management console</span></span>
1. <span data-ttu-id="e2a6d-115">Otwórz konsolę zarządzania usług AD FS na podstawowym serwerze usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="e2a6d-116">Rozwiń węzeł usług AD FS, a następnie kliknij przycisk **zaufania jednostek uzależnionych**.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e2a6d-117">Kliknij prawym przyciskiem myszy programu Office 365/Azure zaufania jednostki uzależnionej, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="e2a6d-118">Wybierz **zaawansowane** i wybierz skrótu secure hash algorithm SHA256.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="e2a6d-119">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-119">Click **OK**.</span></span>

![Algorytm podpisywania SHA256--programu MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="e2a6d-121">Polecenia cmdlet programu AD FS programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2a6d-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="e2a6d-122">Na dowolnym serwerze usług AD FS Otwórz program PowerShell w obszarze uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="e2a6d-123">Wartość skrótu secure hash algorithm przy użyciu **Set-AdfsRelyingPartyTrust** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2a6d-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="e2a6d-124">Zobacz temat</span><span class="sxs-lookup"><span data-stu-id="e2a6d-124">Also read</span></span>
* [<span data-ttu-id="e2a6d-125">Napraw zaufania usługi Office 365 z programem Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="e2a6d-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

