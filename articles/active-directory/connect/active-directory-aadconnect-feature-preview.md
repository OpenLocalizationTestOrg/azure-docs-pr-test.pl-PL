---
title: 'Azure AD Connect: Funkcje w wersji zapoznawczej | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano więcej funkcji szczegóły, które są w wersji zapoznawczej w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="acb17-103">Więcej informacji na temat funkcji w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="acb17-103">More details about features in preview</span></span>
<span data-ttu-id="acb17-104">W tym temacie opisano, jak toouse obecnie funkcje w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="acb17-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="acb17-105">Zapisywanie zwrotne grup</span><span class="sxs-lookup"><span data-stu-id="acb17-105">Group writeback</span></span>
<span data-ttu-id="acb17-106">Opcja powitania dla zapisu zwrotnego grup w funkcji opcjonalnych umożliwia toowriteback **grupy usługi Office 365** tooa lasu za pomocą programu Exchange jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="acb17-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="acb17-107">To jest grupa, która zawsze jest zarządzany w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="acb17-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="acb17-108">Jeśli masz lokalnego programu Exchange, następnie można napisać ponownie lokalnych tooon tych grup, wysyłanie i odbieranie wiadomości e-mail z następujących grup użytkowników z skrzynki pocztowej programu Exchange lokalnie.</span><span class="sxs-lookup"><span data-stu-id="acb17-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="acb17-109">Więcej informacji na temat grupy usługi Office 365 i jak toouse je można znaleźć [tutaj](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="acb17-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="acb17-110">Grupy usługi Office 365 jest reprezentowany jako grupy dystrybucji w lokalnej instalacji usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="acb17-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="acb17-111">Z lokalnym programem Exchange server musi być na aktualizację zbiorczą programu Exchange 2013 8 (wydane w marca 2015) lub programów Exchange 2016 toorecognize ten nowy typ grupy.</span><span class="sxs-lookup"><span data-stu-id="acb17-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="acb17-112">**Informacje o wersji zapoznawczej hello**</span><span class="sxs-lookup"><span data-stu-id="acb17-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="acb17-113">Atrybut książki adresu Hello obecnie jest pusta w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="acb17-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="acb17-114">Bez tego atrybutu hello grupy nie jest widoczny w hello usługi GAL.</span><span class="sxs-lookup"><span data-stu-id="acb17-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="acb17-115">Najprostszym sposobem toopopulate Hello ten atrybut to polecenie cmdlet programu PowerShell usługi Exchange hello toouse `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="acb17-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="acb17-116">Tylko lasy ze schematem Exchange hello są prawidłowe elementy docelowe dla grup.</span><span class="sxs-lookup"><span data-stu-id="acb17-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="acb17-117">Jeśli wykryto nie programu Exchange, następnie zapisu zwrotnego grup nie jest możliwe tooenable.</span><span class="sxs-lookup"><span data-stu-id="acb17-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="acb17-118">Tylko jeden las wdrożenia organizacji programu Exchange są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="acb17-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="acb17-119">Jeśli masz więcej niż jednej organizacji do lokalnego programu Exchange, wymagana będzie używane rozwiązanie lokalne usługi GALSync dla tych grup tooappear w sieci w innych lasach.</span><span class="sxs-lookup"><span data-stu-id="acb17-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="acb17-120">funkcji zapisywania zwrotnego grupy Hello nie obsługuje grup zabezpieczeń lub grup dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="acb17-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="acb17-121">Subskrypcja tooAzure AD — wersja Premium jest wymagana dla zapisu zwrotnego grup.</span><span class="sxs-lookup"><span data-stu-id="acb17-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="acb17-122">Zapisywanie zwrotne użytkowników</span><span class="sxs-lookup"><span data-stu-id="acb17-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="acb17-123">Witaj użytkownika funkcja zapisywania zwrotnego w wersji zapoznawczej została usunięta w hello sierpnia 2015 aktualizacja tooAzure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="acb17-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="acb17-124">Jeśli zostanie włączona, należy wyłączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="acb17-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="acb17-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="acb17-125">Next steps</span></span>
<span data-ttu-id="acb17-126">Kontynuuj Twojej [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="acb17-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="acb17-127">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="acb17-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
