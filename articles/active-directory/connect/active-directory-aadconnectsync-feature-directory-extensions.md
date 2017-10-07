---
title: "Synchronizacja programu Azure AD Connect: rozszerzenia katalogów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano funkcję rozszerzeń katalogu hello w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="e99fb-103">Synchronizacja programu Azure AD Connect: rozszerzenia katalogów</span><span class="sxs-lookup"><span data-stu-id="e99fb-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="e99fb-104">Rozszerzenia katalogów pozwala tooextend hello schematu w usłudze Azure AD przy użyciu własnego atrybutów z lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e99fb-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="e99fb-105">Ta funkcja umożliwia aplikacji biznesowych toobuild korzystanie z atrybutów kontynuować toomanage lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="e99fb-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="e99fb-106">Te atrybuty mogą być używane za pośrednictwem [rozszerzeń katalogu Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) lub [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e99fb-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="e99fb-107">Widać hello atrybuty dostępne przy użyciu [explorer Azure AD Graph](https://graphexplorer.cloudapp.net) i [Eksplorator Microsoft Graph](https://graphexplorer2.azurewebsites.net/) odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e99fb-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="e99fb-108">Obecnie nie obciążenie usługi Office 365 wykorzystuje te atrybuty.</span><span class="sxs-lookup"><span data-stu-id="e99fb-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="e99fb-109">Konfigurowanie dodatkowych atrybutów, które chcesz toosynchronize w ścieżce ustawienia niestandardowe powitania w Kreatorze instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="e99fb-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="e99fb-110">![Kreator rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="e99fb-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="e99fb-111">Hello instalacji zawiera następujące atrybuty, które są prawidłowe kandydatów hello:</span><span class="sxs-lookup"><span data-stu-id="e99fb-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="e99fb-112">Typy obiektów użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="e99fb-112">User and Group object types</span></span>
* <span data-ttu-id="e99fb-113">Atrybuty jednowartościowe: String, Boolean, Integer, dane binarne</span><span class="sxs-lookup"><span data-stu-id="e99fb-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="e99fb-114">Atrybuty wielowartościowe: ciąg, dane binarne</span><span class="sxs-lookup"><span data-stu-id="e99fb-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="e99fb-115">Witaj listę atrybutów jest do odczytu z pamięci podręcznej schematu hello utworzony podczas instalacji programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e99fb-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="e99fb-116">Jeśli rozszerzono schemat usługi Active Directory hello przy użyciu dodatkowych atrybutów, następnie hello [schematu musi zostać odświeżona](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) przed te nowe atrybuty są widoczne.</span><span class="sxs-lookup"><span data-stu-id="e99fb-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="e99fb-117">Obiektu w usłudze Azure AD mogą mieć atrybutów rozszerzeń katalogu too100.</span><span class="sxs-lookup"><span data-stu-id="e99fb-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="e99fb-118">Witaj maksymalna długość wynosi 250 znaków.</span><span class="sxs-lookup"><span data-stu-id="e99fb-118">hello max length is 250 characters.</span></span> <span data-ttu-id="e99fb-119">Jeśli wartość atrybutu jest dłuższy, następnie zostanie obcięta przez hello aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e99fb-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="e99fb-120">Podczas instalacji programu Azure AD Connect aplikacja jest zarejestrowany, których te atrybuty są dostępne.</span><span class="sxs-lookup"><span data-stu-id="e99fb-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="e99fb-121">Tę aplikację w portalu Azure hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="e99fb-121">You can see this application in hello Azure portal.</span></span>  
![Aplikacja rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="e99fb-123">Te atrybuty są teraz dostępne za pośrednictwem wykresu:</span><span class="sxs-lookup"><span data-stu-id="e99fb-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="e99fb-125">atrybuty Hello są poprzedzane prefiksem rozszerzenia\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="e99fb-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="e99fb-126">Witaj AppClientId ma hello samą wartość dla wszystkich atrybutów w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e99fb-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e99fb-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e99fb-127">Next steps</span></span>
<span data-ttu-id="e99fb-128">Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e99fb-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e99fb-129">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e99fb-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
