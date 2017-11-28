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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="96399-103">Więcej informacji na temat funkcji w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="96399-103">More details about features in preview</span></span>
<span data-ttu-id="96399-104">W tym temacie opisano sposób użycia funkcji obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="96399-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="96399-105">Zapisywanie zwrotne grup</span><span class="sxs-lookup"><span data-stu-id="96399-105">Group writeback</span></span>
<span data-ttu-id="96399-106">Opcja dla zapisu zwrotnego grup w funkcji opcjonalnych służy do zapisywania zwrotnego **grupy usługi Office 365** do lasu za pomocą programu Exchange jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="96399-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="96399-107">To jest grupa, która zawsze jest zarządzany w chmurze.</span><span class="sxs-lookup"><span data-stu-id="96399-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="96399-108">Jeśli masz lokalnego programu Exchange, następnie można napisać ponownie te grupy do lokalnego, wysyłanie i odbieranie wiadomości e-mail z następujących grup użytkowników z skrzynki pocztowej programu Exchange lokalnie.</span><span class="sxs-lookup"><span data-stu-id="96399-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="96399-109">Więcej informacji na temat grupy usługi Office 365 i sposobu ich użycia można znaleźć [tutaj](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="96399-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="96399-110">Grupy usługi Office 365 jest reprezentowany jako grupy dystrybucji w lokalnej instalacji usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="96399-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="96399-111">Z lokalnym programem Exchange server musi być na aktualizację zbiorczą programu Exchange 2013 8 (wydane w marca 2015) lub programów Exchange 2016 rozpoznać ten nowy typ grupy.</span><span class="sxs-lookup"><span data-stu-id="96399-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="96399-112">**Informacje w wersji zapoznawczej**</span><span class="sxs-lookup"><span data-stu-id="96399-112">**Notes during the preview**</span></span>

* <span data-ttu-id="96399-113">Atrybut książki adresu jest obecnie pusta w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="96399-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="96399-114">Bez tego atrybutu grupy nie jest widoczny w globalnej.</span><span class="sxs-lookup"><span data-stu-id="96399-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="96399-115">Najprostszym sposobem wypełniania tego atrybutu jest użycie polecenia cmdlet programu PowerShell usługi Exchange `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="96399-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="96399-116">Tylko lasy ze schematem Exchange są prawidłowe elementy docelowe dla grup.</span><span class="sxs-lookup"><span data-stu-id="96399-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="96399-117">Jeśli Exchange nie został wykryty, zapisu zwrotnego grup nie jest możliwe do włączenia.</span><span class="sxs-lookup"><span data-stu-id="96399-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="96399-118">Tylko jeden las wdrożenia organizacji programu Exchange są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="96399-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="96399-119">Jeśli masz więcej niż jednej organizacji do lokalnego programu Exchange, należy lokalnego rozwiązania usługi GALSync dla tych grup, które mają być widoczne w Twojej innych lasach.</span><span class="sxs-lookup"><span data-stu-id="96399-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="96399-120">Nie obsługuje funkcji zapisywania zwrotnego grup, grup zabezpieczeń lub grup dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="96399-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="96399-121">Subskrypcja usługi Azure AD Premium jest wymagana dla zapisu zwrotnego grup.</span><span class="sxs-lookup"><span data-stu-id="96399-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="96399-122">Zapisywanie zwrotne użytkowników</span><span class="sxs-lookup"><span data-stu-id="96399-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="96399-123">Funkcja zapisywania zwrotnego użytkowników w wersji zapoznawczej został usunięty w sierpnia 2015 aktualizacji do programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="96399-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="96399-124">Jeśli zostanie włączona, należy wyłączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="96399-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="96399-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96399-125">Next steps</span></span>
<span data-ttu-id="96399-126">Kontynuuj Twojej [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="96399-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="96399-127">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="96399-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
