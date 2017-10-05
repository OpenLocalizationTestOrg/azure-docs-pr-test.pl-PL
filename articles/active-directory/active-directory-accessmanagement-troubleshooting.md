---
title: "Rozwiązywanie problemów z członkostwo dynamiczne w grupach | Dokumentacja firmy Microsoft"
description: "Porady dotyczące rozwiązywania problemów dynamicznego zarządzania członkostwem w grupach w usłudze Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="6be3c-103">Rozwiązywanie problemów z członkostwem dynamicznym w grupach</span><span class="sxs-lookup"><span data-stu-id="6be3c-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="6be3c-104">**Po skonfigurowaniu reguły w grupie, ale aktualizowany nie członkostwa w grupie**</span><span class="sxs-lookup"><span data-stu-id="6be3c-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="6be3c-105">Sprawdź, czy **Włącz delegowane Zarządzanie grupami** mają ustawioną wartość **tak** w **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="6be3c-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="6be3c-106">To ustawienie zostanie wyświetlony tylko wtedy, gdy użytkownik jest zalogowany jako użytkownik, któremu przypisano licencji usługi Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="6be3c-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="6be3c-107">Sprawdź wartości atrybutów użytkownika dla reguły: istnieją użytkownicy, którzy spełniają zasady?</span><span class="sxs-lookup"><span data-stu-id="6be3c-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="6be3c-108">**Po skonfigurowaniu reguły, ale teraz istniejących członków reguły zostaną usunięte**</span><span class="sxs-lookup"><span data-stu-id="6be3c-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="6be3c-109">Jest to oczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="6be3c-109">This is expected behavior.</span></span> <span data-ttu-id="6be3c-110">Istniejących członków grupy są usuwane, gdy reguła jest włączona lub zmienione.</span><span class="sxs-lookup"><span data-stu-id="6be3c-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="6be3c-111">Użytkownicy zwrócił ewaluacyjną reguła są dodawane jako członków do grupy.</span><span class="sxs-lookup"><span data-stu-id="6be3c-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="6be3c-112">**Nie widzę członkostwa zmian natychmiast po Dodawanie lub zmienianie reguły, dlaczego nie?**</span><span class="sxs-lookup"><span data-stu-id="6be3c-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="6be3c-113">Ocenę członkostwa dedykowanych okresowo odbywa się w tle asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="6be3c-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="6be3c-114">Jak długo trwa proces jest określana przez liczbę użytkowników w katalogu i rozmiar grupy utworzone w wyniku reguły.</span><span class="sxs-lookup"><span data-stu-id="6be3c-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="6be3c-115">Zazwyczaj katalogi z małej liczby użytkowników zobaczą zmiany członkostwa w grupie w mniej niż kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6be3c-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="6be3c-116">Katalogi z dużą liczbą użytkowników może potrwać 30 minut lub dłużej, aby wypełnić.</span><span class="sxs-lookup"><span data-stu-id="6be3c-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="6be3c-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6be3c-117">Next steps</span></span>
<span data-ttu-id="6be3c-118">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6be3c-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="6be3c-119">Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6be3c-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="6be3c-120">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6be3c-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6be3c-121">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6be3c-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="6be3c-122">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6be3c-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
