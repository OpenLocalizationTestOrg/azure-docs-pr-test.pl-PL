---
title: "aaaTroubleshooting członkostwo dynamiczne w grupach | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="95cfb-103">Rozwiązywanie problemów z członkostwem dynamicznym w grupach</span><span class="sxs-lookup"><span data-stu-id="95cfb-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="95cfb-104">**Po skonfigurowaniu reguły w grupie, ale aktualizowany nie członkostwa w grupie hello**</span><span class="sxs-lookup"><span data-stu-id="95cfb-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="95cfb-105">Sprawdź, że hello **Włącz delegowane Zarządzanie grupami** ustawioną zbyt**tak** w hello **Konfiguruj** kartę. To ustawienie zostanie wyświetlony tylko wtedy, gdy użytkownik jest zalogowany jako użytkownik toowhom licencji usługi Azure Active Directory Premium jest przypisana.</span><span class="sxs-lookup"><span data-stu-id="95cfb-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="95cfb-106">Sprawdź wartości atrybutów użytkownika w regule hello hello: istnieją użytkownicy, którzy spełniają zasady hello?</span><span class="sxs-lookup"><span data-stu-id="95cfb-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="95cfb-107">**Po skonfigurowaniu reguły, ale teraz hello istniejących członków hello reguły zostaną usunięte**</span><span class="sxs-lookup"><span data-stu-id="95cfb-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="95cfb-108">Jest to oczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="95cfb-108">This is expected behavior.</span></span> <span data-ttu-id="95cfb-109">Istniejących członków grupy hello są usuwane, gdy reguła jest włączona lub zmienione.</span><span class="sxs-lookup"><span data-stu-id="95cfb-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="95cfb-110">Użytkownicy Hello zwrócił ewaluacyjną reguła hello są dodawane jako elementy członkowskie grupy toohello.</span><span class="sxs-lookup"><span data-stu-id="95cfb-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="95cfb-111">**Nie widzę członkostwa zmian natychmiast po Dodawanie lub zmienianie reguły, dlaczego nie?**</span><span class="sxs-lookup"><span data-stu-id="95cfb-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="95cfb-112">Ocenę członkostwa dedykowanych okresowo odbywa się w tle asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="95cfb-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="95cfb-113">Jak długo trwa proces hello jest określana przez hello liczbę użytkowników w rozmiar katalogu i hello hello grupy utworzone w wyniku hello reguły.</span><span class="sxs-lookup"><span data-stu-id="95cfb-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="95cfb-114">Zazwyczaj katalogi z małej liczby użytkowników zobaczą zmiany członkostwa w grupie hello mniej niż za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="95cfb-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="95cfb-115">Katalogi z dużą liczbą użytkowników może potrwać 30 minut lub dłużej toopopulate.</span><span class="sxs-lookup"><span data-stu-id="95cfb-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="95cfb-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95cfb-116">Next steps</span></span>
<span data-ttu-id="95cfb-117">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95cfb-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="95cfb-118">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95cfb-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="95cfb-119">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95cfb-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="95cfb-120">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95cfb-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="95cfb-121">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95cfb-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
