---
title: "Azure Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości - określenie wymagań synchronizacji katalogu | Dokumentacja firmy Microsoft"
description: "Określenie, jakie wymagania niezbędne do synchronizowania wszystkich użytkowników między on = lokalnych i w chmurze dla przedsiębiorstw."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="3c72d-103">Określenie wymagań synchronizacji katalogu</span><span class="sxs-lookup"><span data-stu-id="3c72d-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="3c72d-104">Synchronizacja jest udostępnianie tożsamości w chmurze na podstawie ich tożsamości lokalnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3c72d-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="3c72d-105">Czy zsynchronizowane konta będzie używany do uwierzytelniania lub uwierzytelnianie federacyjne, użytkownicy będą nadal musi być tożsamości w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c72d-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="3c72d-106">Ta tożsamość należy utrzymanie i okresowo aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="3c72d-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="3c72d-107">Aktualizacje mogą mieć wiele form, od zmian tytuł do zmiany hasła.</span><span class="sxs-lookup"><span data-stu-id="3c72d-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="3c72d-108">Rozpocznij od szacowania organizacji lokalnej tożsamości rozwiązanie i użytkownika wymagań.</span><span class="sxs-lookup"><span data-stu-id="3c72d-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="3c72d-109">Ocena ważne jest, aby zdefiniować wymagania techniczne dotyczące sposobu tworzenia i obsługiwane w chmurze tożsamości użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3c72d-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="3c72d-110">W przypadku większości organizacji usługi Active Directory działa lokalnie i będą katalog lokalny, który użytkownicy będą przez synchronizowane z, jednak w niektórych przypadkach nie będzie wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="3c72d-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="3c72d-111">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="3c72d-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3c72d-112">Masz jeden las usługi AD, wielu lub Brak?</span><span class="sxs-lookup"><span data-stu-id="3c72d-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="3c72d-113">Ile katalogów usługi Azure AD będzie można być synchronizowanie?</span><span class="sxs-lookup"><span data-stu-id="3c72d-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="3c72d-114">Używasz filtrowania?</span><span class="sxs-lookup"><span data-stu-id="3c72d-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="3c72d-115">Masz wiele serwerów usługi Azure AD Connect planowana?</span><span class="sxs-lookup"><span data-stu-id="3c72d-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="3c72d-116">Obecnie masz synchronizacji narzędzia lokalnej?</span><span class="sxs-lookup"><span data-stu-id="3c72d-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="3c72d-117">Jeśli tak, czy użytkownicy, jeśli użytkownicy mają wirtualnego katalogu/integracji tożsamości?</span><span class="sxs-lookup"><span data-stu-id="3c72d-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="3c72d-118">Masz wszelkie inne katalogu lokalnego, które mają być synchronizowane (np. katalogu LDAP, bazy danych działu HR, itp.)?</span><span class="sxs-lookup"><span data-stu-id="3c72d-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="3c72d-119">Zamierzasz realizacji dowolnej usługi GALSync?</span><span class="sxs-lookup"><span data-stu-id="3c72d-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="3c72d-120">Co to jest bieżący stan nazwy UPN w organizacji?</span><span class="sxs-lookup"><span data-stu-id="3c72d-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="3c72d-121">Masz innego katalogu, który uwierzytelniania użytkowników?</span><span class="sxs-lookup"><span data-stu-id="3c72d-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="3c72d-122">Firma używa programu Microsoft Exchange?</span><span class="sxs-lookup"><span data-stu-id="3c72d-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="3c72d-123">Są one plan o wdrożeniu hybrydowym programu exchange?</span><span class="sxs-lookup"><span data-stu-id="3c72d-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="3c72d-124">Teraz, gdy masz pomysł o wymaganiach synchronizacji, należy określić, które narzędzie jest poprawne tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="3c72d-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="3c72d-125">Firma Microsoft udostępnia kilka narzędzi integracji katalogów i synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="3c72d-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="3c72d-126">Zobacz [Tabela porównawcza narzędzi integracji katalogu tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-tools-comparison.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3c72d-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="3c72d-127">Teraz, gdy masz wymagań synchronizacji i narzędzie, które będą w tym celu w firmie, należy ocenić aplikacje, które używają tych usług katalogowych.</span><span class="sxs-lookup"><span data-stu-id="3c72d-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="3c72d-128">Ocena ważne jest, aby zdefiniować wymagania techniczne do integrowania tych aplikacji w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c72d-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="3c72d-129">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="3c72d-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3c72d-130">Zostaną przeniesione następujące aplikacje w chmurze i użyć katalogu?</span><span class="sxs-lookup"><span data-stu-id="3c72d-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="3c72d-131">Czy istnieją specjalne atrybuty, które muszą zostać zsynchronizowane w chmurze, więc tych aplikacji można używać ich pomyślnie?</span><span class="sxs-lookup"><span data-stu-id="3c72d-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="3c72d-132">Te aplikacje będą potrzebne do zapisania ponownie korzystać z uwierzytelniania w chmurze?</span><span class="sxs-lookup"><span data-stu-id="3c72d-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="3c72d-133">Te aplikacje będzie live lokalnego, podczas gdy użytkownicy uzyskują dostęp do ich przy użyciu tożsamości chmury?</span><span class="sxs-lookup"><span data-stu-id="3c72d-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="3c72d-134">Należy również określić synchronizacji katalogów wymagań i ograniczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3c72d-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="3c72d-135">Ocena ważne jest, aby uzyskać listę wymagań, które będą potrzebne w celu tworzenia i zarządzania tożsamościami użytkowników w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c72d-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="3c72d-136">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="3c72d-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3c72d-137">Której zostaną umieszczone serwera synchronizacji?</span><span class="sxs-lookup"><span data-stu-id="3c72d-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="3c72d-138">Będzie on zostać przyłączone do domeny?</span><span class="sxs-lookup"><span data-stu-id="3c72d-138">Will it be domain joined?</span></span>
* <span data-ttu-id="3c72d-139">Serwer zostanie umieszczony w sieci z ograniczeniami za zaporą, takich jak strefą DMZ?</span><span class="sxs-lookup"><span data-stu-id="3c72d-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="3c72d-140">Użytkownik będzie mógł otworzyć porty zapory wymagane do obsługi synchronizacji?</span><span class="sxs-lookup"><span data-stu-id="3c72d-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="3c72d-141">Czy organizacja ma plan odzyskiwania po awarii dla serwera synchronizacji?</span><span class="sxs-lookup"><span data-stu-id="3c72d-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="3c72d-142">Masz konto z odpowiednie uprawnienia do wszystkich lasów, które chcesz zsynchronizować z?</span><span class="sxs-lookup"><span data-stu-id="3c72d-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="3c72d-143">Jeśli firma nie znasz odpowiedzi na to pytanie, zapoznaj się z sekcją "Uprawnień do synchronizacji haseł" w artykule [zainstalować usługi Azure do synchronizacji usługi Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) i ustalić, jeśli masz już konto z odpowiednimi uprawnieniami lub jeśli chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="3c72d-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="3c72d-144">Jeśli masz synchronizacji mutli lasu jest serwer synchronizacji można uzyskać w każdym lesie?</span><span class="sxs-lookup"><span data-stu-id="3c72d-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="3c72d-145">Upewnij się zanotować wszystkie odpowiedzi i zrozumieć ich uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="3c72d-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="3c72d-146">[Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) będą przekazywane dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="3c72d-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="3c72d-147">Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.</span><span class="sxs-lookup"><span data-stu-id="3c72d-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3c72d-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c72d-148">Next steps</span></span>
[<span data-ttu-id="3c72d-149">Określić wymagania dotyczące uwierzytelniania wieloskładnikowego</span><span class="sxs-lookup"><span data-stu-id="3c72d-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="3c72d-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3c72d-150">See also</span></span>
[<span data-ttu-id="3c72d-151">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="3c72d-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

