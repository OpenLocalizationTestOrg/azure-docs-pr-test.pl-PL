---
title: "Synchronizacja programu Azure AD Connect: rozszerzenia katalogów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano funkcję rozszerzeń katalogu w programie Azure AD Connect."
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="c488c-103">Synchronizacja programu Azure AD Connect: rozszerzenia katalogów</span><span class="sxs-lookup"><span data-stu-id="c488c-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="c488c-104">Rozszerzenia katalogów umożliwia rozszerzanie schematu w usłudze Azure AD przy użyciu własnego atrybutów z lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c488c-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="c488c-105">Ta funkcja umożliwia tworzenie aplikacji biznesowych, korzystanie z atrybutów, można nadal zarządzać lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="c488c-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="c488c-106">Te atrybuty mogą być używane za pośrednictwem [rozszerzeń katalogu Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) lub [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="c488c-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="c488c-107">Widać atrybuty dostępne przy użyciu [explorer Azure AD Graph](https://graphexplorer.cloudapp.net) i [Eksplorator Microsoft Graph](https://graphexplorer2.azurewebsites.net/) odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c488c-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="c488c-108">Obecnie nie obciążenie usługi Office 365 wykorzystuje te atrybuty.</span><span class="sxs-lookup"><span data-stu-id="c488c-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="c488c-109">Możesz skonfigurować dodatkowych atrybutów, które chcesz synchronizować w ścieżce ustawienia niestandardowe w Kreatorze instalacji.</span><span class="sxs-lookup"><span data-stu-id="c488c-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="c488c-110">![Kreator rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="c488c-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="c488c-111">Instalacja zawiera następujące atrybuty, które są kandydatami prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="c488c-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="c488c-112">Typy obiektów użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="c488c-112">User and Group object types</span></span>
* <span data-ttu-id="c488c-113">Atrybuty jednowartościowe: String, Boolean, Integer, dane binarne</span><span class="sxs-lookup"><span data-stu-id="c488c-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="c488c-114">Atrybuty wielowartościowe: ciąg, dane binarne</span><span class="sxs-lookup"><span data-stu-id="c488c-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="c488c-115">Lista atrybutów jest do odczytu z pamięci podręcznej schematu, utworzony podczas instalacji programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c488c-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="c488c-116">Jeśli rozszerzono schemat usługi Active Directory przy użyciu dodatkowych atrybutów, a następnie [schematu musi zostać odświeżona](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) przed te nowe atrybuty są widoczne.</span><span class="sxs-lookup"><span data-stu-id="c488c-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="c488c-117">Obiektu w usłudze Azure AD mogą mieć maksymalnie 100 atrybuty rozszerzenia katalogu.</span><span class="sxs-lookup"><span data-stu-id="c488c-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="c488c-118">Maksymalna długość wynosi 250 znaków.</span><span class="sxs-lookup"><span data-stu-id="c488c-118">The max length is 250 characters.</span></span> <span data-ttu-id="c488c-119">Jeśli wartość atrybutu jest dłuższy, następnie zostanie obcięta przez aparat synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="c488c-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="c488c-120">Podczas instalacji programu Azure AD Connect aplikacja jest zarejestrowany, których te atrybuty są dostępne.</span><span class="sxs-lookup"><span data-stu-id="c488c-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="c488c-121">Można wyświetlić tę aplikację w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c488c-121">You can see this application in the Azure portal.</span></span>  
![Aplikacja rozszerzenia schematu](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="c488c-123">Te atrybuty są teraz dostępne za pośrednictwem wykresu:</span><span class="sxs-lookup"><span data-stu-id="c488c-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="c488c-125">Atrybuty są poprzedzane prefiksem rozszerzenia\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="c488c-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="c488c-126">AppClientId ma taką samą wartość dla wszystkich atrybutów w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c488c-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c488c-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c488c-127">Next steps</span></span>
<span data-ttu-id="c488c-128">Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c488c-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="c488c-129">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c488c-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
