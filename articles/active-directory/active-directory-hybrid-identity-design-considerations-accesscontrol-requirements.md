---
title: "Azure Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących kontroli dostępu | Dokumentacja firmy Microsoft"
description: "Obejmuje tożsamości i ustalenie wymagań dotyczących dostępu do zasobów dla użytkowników w środowisku hybrydowym."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e8bbb-103">Określić wymagania dotyczące rozwiązania z tożsamością hybrydową kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="e8bbb-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e8bbb-104">Gdy organizacji projektuje ich rozwiązania z tożsamością hybrydową mogą również wykorzystać korzystając z okazji, aby przejrzeć wymagania dotyczące dostępu do zasobów, które są planowane był dostępny dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="e8bbb-105">Dostęp do danych granic wszystkich czterech filarach tożsamości, które są:</span><span class="sxs-lookup"><span data-stu-id="e8bbb-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="e8bbb-106">Administracja</span><span class="sxs-lookup"><span data-stu-id="e8bbb-106">Administration</span></span>
* <span data-ttu-id="e8bbb-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="e8bbb-107">Authentication</span></span>
* <span data-ttu-id="e8bbb-108">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="e8bbb-108">Authorization</span></span>
* <span data-ttu-id="e8bbb-109">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="e8bbb-109">Auditing</span></span>

<span data-ttu-id="e8bbb-110">W poniższych sekcjach następuje obejmie uwierzytelnianie i autoryzację w bardziej szczegółowe informacje, administracji i inspekcji są częścią cyklu życia tożsamości hybrydowej.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="e8bbb-111">Odczyt [określić zadań zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) Aby uzyskać więcej informacji o tych funkcjach.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="e8bbb-112">Odczyt [czterech filarach tożsamości — zarządzania tożsamościami w wieku hybrydowego się](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) uzyskać więcej informacji o każdej z nich tych słupków.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="e8bbb-113">Uwierzytelnianie i autoryzacja</span><span class="sxs-lookup"><span data-stu-id="e8bbb-113">Authentication and authorization</span></span>
<span data-ttu-id="e8bbb-114">Istnieją różne scenariusze uwierzytelniania i autoryzacji, te scenariusze będzie mieć określone wymagania, które muszą być spełnione przez rozwiązania z tożsamością hybrydową, które firma zamierza przyjąć.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="e8bbb-115">Scenariusze obejmujące Business-to-Business komunikacji (B2B) można dodać dodatkowe żądania dla administratorów IT, ponieważ będzie musiał upewnij się, że metoda uwierzytelniania i autoryzacji, używane przez organizację może komunikować się z ich partnerów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="e8bbb-116">Podczas procesu projektowania wymagania w zakresie uwierzytelniania i autoryzacji upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="e8bbb-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="e8bbb-117">Zostanie organizacji uwierzytelniania i autoryzacji tylko użytkownicy znajdujący się w ich tożsamości systemu zarządzania?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="e8bbb-118">Czy jest planowane dla scenariusze B2B?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="e8bbb-119">Jeśli tak, znasz już protokołów (SAML, OAuth, protokołu Kerberos, tokeny lub certyfikatów) będzie służyć do nawiązania połączenia zarówno firmy?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="e8bbb-120">Czy rozwiązania z tożsamością hybrydową, który ma przyjąć obsługi tych protokołów?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="e8bbb-121">Innym ważnym wziąć pod uwagę jest której zostaną umieszczone w repozytorium uwierzytelniania, który będzie używany przez użytkowników i partnerów i modelu administracyjnego do użycia.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="e8bbb-122">Należy wziąć pod uwagę następujące opcje dwa podstawowe:</span><span class="sxs-lookup"><span data-stu-id="e8bbb-122">Consider the following two core options:</span></span>

* <span data-ttu-id="e8bbb-123">Scentralizowane: w tym modelu poświadczeń użytkownika, zasady i Administracja może być scentralizowanie lokalne lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="e8bbb-124">Hybrydowe: w tym modelu poświadczeń użytkownika, zasady i administrowanie będzie scentralizowanie lokalne i replikowane w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="e8bbb-125">Model, który przyjmuje organizacji różnią się zgodnie z ich wymaganiami biznesowymi chcesz odpowiedzieć na następujące pytania, aby zidentyfikować której będą znajdować się system zarządzania tożsamościami i trybu administratora do użycia:</span><span class="sxs-lookup"><span data-stu-id="e8bbb-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="e8bbb-126">Twoja organizacja ma obecnie Zarządzanie tożsamościami lokalnej?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="e8bbb-127">Jeśli tak, czy planują schowaj?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="e8bbb-128">Czy istnieją wszystkie rozporządzenia lub wymaganiami dotyczącymi zgodności czy organizacji wykonaj określają, że gdy system zarządzania tożsamościami powinien znajdować się?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="e8bbb-129">Twoja organizacja używa logowania jednokrotnego dla aplikacji znajdujących się lokalnie lub w chmurze?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="e8bbb-130">Jeśli tak, przyjęcia modelu tożsamości hybrydowej wpływa na ten proces?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="e8bbb-131">Kontrola dostępu</span><span class="sxs-lookup"><span data-stu-id="e8bbb-131">Access Control</span></span>
<span data-ttu-id="e8bbb-132">Uwierzytelnianie i autoryzacja są podstawowe elementy umożliwiające dostęp do firmowych danych za pośrednictwem weryfikacji użytkownika, należy również kontrolować poziom dostępu Ci użytkownicy będą mieć i ma poziom dostępu administratorów za pośrednictwem zasoby, które zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="e8bbb-133">Rozwiązania z tożsamością hybrydową musi mieć możliwość zapewnienia szczegółowej dostęp do zasobów, delegowania i kontrolę dostępu na podstawie ról.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="e8bbb-134">Upewnij się, że poniższe pytanie są odbierane dotyczące kontroli dostępu:</span><span class="sxs-lookup"><span data-stu-id="e8bbb-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="e8bbb-135">Czy firma ma więcej niż jednego użytkownika z podwyższonym poziomem uprawnień, aby zarządzać systemem tożsamości?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="e8bbb-136">Jeśli tak, czy każdy użytkownik potrzebuje poziomu dostępu?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="e8bbb-137">Czy firma musi delegować dostęp do użytkowników w celu zarządzania określone zasoby?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="e8bbb-138">Jeśli tak, jak często dzieje się tak?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="e8bbb-139">Czy firma musi integracji możliwości kontroli dostępu między lokalnymi i w chmurze zasobów?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="e8bbb-140">Czy firma potrzebuje do ograniczania dostępu do zasobów zgodnie z niektóre warunki?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="e8bbb-141">Czy firma dysponuje dowolnej aplikacji, która wymaga niestandardowych kontroli dostępu do niektórych zasobów?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="e8bbb-142">Jeśli tak, czy aplikacje lokalizację (lokalnie lub w chmurze)?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="e8bbb-143">Jeśli tak, gdzie są te docelowych zasobów (lokalnie lub w chmurze)?</span><span class="sxs-lookup"><span data-stu-id="e8bbb-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="e8bbb-144">Upewnij się zanotować wszystkie odpowiedzi i zrozumieć ich uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="e8bbb-145">[Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane dostępne opcje oraz zalety/wady każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="e8bbb-146">Udzielenie odpowiedzi na te pytania wybierzesz opcji najlepiej odpowiadała potrzebom biznesowym użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e8bbb-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e8bbb-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8bbb-147">Next steps</span></span>
[<span data-ttu-id="e8bbb-148">Określenie wymagań dotyczących odpowiedzi na zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e8bbb-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="e8bbb-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e8bbb-149">See Also</span></span>
[<span data-ttu-id="e8bbb-150">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="e8bbb-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

