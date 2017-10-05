---
title: "Usługi Azure Active Directory B2C: Uwagi dla deweloperów przy użyciu zasad niestandardowych | Dokumentacja firmy Microsoft"
description: "Uwagi dla deweloperów na skonfigurowaniu i utrzymywaniu z niestandardowych zasad usługi Azure AD B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="8e21c-103">Informacje o wersji dla publicznej wersji zapoznawczej usługi Azure Active Directory B2C zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="8e21c-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="8e21c-104">Zestaw funkcji niestandardowych zasad jest teraz dostępna w wersji ewaluacyjnej w publicznej wersji zapoznawczej dla wszystkich usługi Azure Active Directory B2C (Azure AD B2C) klientów.</span><span class="sxs-lookup"><span data-stu-id="8e21c-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="8e21c-105">Ten zestaw funkcji jest przeznaczona dla deweloperów zaawansowane tożsamości tworzenia najbardziej złożonych rozwiązań tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8e21c-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="8e21c-106">Obecnie ten zestaw funkcji wymaga deweloperom skonfigurowania struktury obsługi tożsamości bezpośrednio za pomocą edycji pliku XML.</span><span class="sxs-lookup"><span data-stu-id="8e21c-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="8e21c-107">Ta metoda konfiguracji jest wydajny i złożone.</span><span class="sxs-lookup"><span data-stu-id="8e21c-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="8e21c-108">Zaawansowane tożsamości deweloperzy przy użyciu platformy obsługi tożsamości należy zaplanować inwestycji pewien czas ukończenia przewodników i odczytywanie dokumentów odwołania.</span><span class="sxs-lookup"><span data-stu-id="8e21c-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="8e21c-109">Funkcje zawarte w tym publicznej wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="8e21c-109">Features included in this public preview</span></span>
<span data-ttu-id="8e21c-110">Z nowych funkcji wprowadzonych w publicznej wersji zapoznawczej deweloperzy mogą wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="8e21c-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="8e21c-111">Tworzenie i przekazywanie niestandardowe uwierzytelnianie użytkownika podróże za pomocą niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="8e21c-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="8e21c-112">Opisano krok po kroku jako wymiany podróże użytkownika od dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="8e21c-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="8e21c-113">Zdefiniuj rozgałęzień warunkowych w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e21c-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="8e21c-114">Integracja usług korzystających z interfejsu API REST w podróży użytkownika z uwierzytelniania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="8e21c-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="8e21c-115">Dodaj federacji z dostawców tożsamości, zgodnych ze standardowych OpenIDConnect.</span><span class="sxs-lookup"><span data-stu-id="8e21c-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="8e21c-116">Dodaj federacji z dostawców tożsamości, które jest zgodna z protokołu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="8e21c-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="8e21c-117">Warunki publicznej wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="8e21c-117">Terms of the public preview</span></span>

* <span data-ttu-id="8e21c-118">Firma Microsoft zachęca do korzystania z nowych funkcji wyłącznie do celów ewaluacyjnych.</span><span class="sxs-lookup"><span data-stu-id="8e21c-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="8e21c-119">Nowe funkcje nie są przeznaczone do użytku w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="8e21c-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="8e21c-120">Nowe funkcje nie dotyczą umów dotyczących poziomu usług (SLA).</span><span class="sxs-lookup"><span data-stu-id="8e21c-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="8e21c-121">Żądania pomocy technicznej można złożyć za pośrednictwem kanałów regularne pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="8e21c-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="8e21c-122">Brak bez uzgodnionej daty dla ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="8e21c-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="8e21c-123">Nasze uznania z dowolnej przyczyny Microsoft może Flaga i odrzucić lub ograniczyć scenariuszy i podróże użytkownika, które wykraczają poza karty produktu usługi Azure AD B2C do służy jako platforma zarządzania (CIAM) tożsamości i dostępu klienta.</span><span class="sxs-lookup"><span data-stu-id="8e21c-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="8e21c-124">Obowiązki deweloperów zestaw funkcji zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="8e21c-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="8e21c-125">Konfiguracja zasad ręczne udziela dostępu niższego poziomu podstawowej platformy Azure AD B2C i spowoduje powstanie framework unikatowy zaufania można swobodnie dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="8e21c-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="8e21c-126">Możliwych kombinacji dostawców tożsamości niestandardowej, relacje zaufania, integracji z usługami zewnętrznych i przepływy pracy krok po kroku umieścić większa zapotrzebowanie na zaawansowanych deweloperów korzystających z nich.</span><span class="sxs-lookup"><span data-stu-id="8e21c-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="8e21c-127">Aby w pełni skorzystać z publicznej wersji zapoznawczej, zalecamy deweloperom korzystanie z niestandardowych zasad zestaw funkcji jest zgodna z następującymi zasadami:</span><span class="sxs-lookup"><span data-stu-id="8e21c-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="8e21c-128">Zapoznanie się z języka konfiguracji aparat obsługi tożsamości i klucz/klucze tajne zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8e21c-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="8e21c-129">Przejmowanie na własność scenariuszy i niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="8e21c-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="8e21c-130">Testowanie metodyczny scenariusza.</span><span class="sxs-lookup"><span data-stu-id="8e21c-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="8e21c-131">Wykonaj rozwoju oprogramowania i przejściowych najlepszych rozwiązań z co najmniej jeden programowanie i środowiska testowego i jednego środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8e21c-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="8e21c-132">Aktualne informacje o nowych rozwiązań z dostawców tożsamości i usługi, którą można zintegrować z.</span><span class="sxs-lookup"><span data-stu-id="8e21c-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="8e21c-133">Na przykład śledzenie pracy w kluczy tajnych i planowanych i nieplanowanych zmiany w usłudze.</span><span class="sxs-lookup"><span data-stu-id="8e21c-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="8e21c-134">Konfigurowanie aktywnego monitorowania i monitorowanie czasu reakcji środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="8e21c-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="8e21c-135">Aktualizuj adresy e-mail kontaktów i pozostać odbierać wiadomości e-mail na żywo witryny zespołu firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e21c-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="8e21c-136">Podjąć działania odpowiednim przypadku zaleca się, aby to zrobić przez zespół live witryny firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e21c-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="8e21c-137">Te funkcje mogą ostatecznie dołączone wbudowane zasady usługi Azure AD, dzięki czemu łatwiej dostępne dla wszystkich deweloperów.</span><span class="sxs-lookup"><span data-stu-id="8e21c-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e21c-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e21c-138">Next steps</span></span>
<span data-ttu-id="8e21c-139">[Wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8e21c-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
