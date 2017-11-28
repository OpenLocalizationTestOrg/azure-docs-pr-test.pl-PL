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
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="1987a-103">Informacje o wersji dla publicznej wersji zapoznawczej usługi Azure Active Directory B2C zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="1987a-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="1987a-104">Witaj zestaw funkcji niestandardowych zasad jest teraz dostępna w wersji ewaluacyjnej w publicznej wersji zapoznawczej dla wszystkich usługi Azure Active Directory B2C (Azure AD B2C) klientów.</span><span class="sxs-lookup"><span data-stu-id="1987a-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="1987a-105">Ten zestaw funkcji jest przeznaczona dla deweloperów zaawansowane tożsamości tworzenia hello najbardziej złożonych rozwiązań tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1987a-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="1987a-106">Obecnie ten zestaw funkcji wymaga deweloperzy tooconfigure hello Framework obsługi tożsamości bezpośrednio za pomocą edycji pliku XML.</span><span class="sxs-lookup"><span data-stu-id="1987a-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="1987a-107">Ta metoda konfiguracji jest wydajny i złożone.</span><span class="sxs-lookup"><span data-stu-id="1987a-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="1987a-108">Zaawansowane deweloperzy tożsamości za pomocą hello Framework obsługi tożsamości należy zaplanować tooinvest pewien czas ukończenia przewodników i odczytywanie dokumentów odwołania.</span><span class="sxs-lookup"><span data-stu-id="1987a-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="1987a-109">Funkcje zawarte w tym publicznej wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="1987a-109">Features included in this public preview</span></span>
<span data-ttu-id="1987a-110">Witaj wprowadzeniu nowych funkcji wprowadzonych w wersji zapoznawczej hello deweloperzy mogą wykonywać hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="1987a-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="1987a-111">Tworzenie i przekazywanie niestandardowe uwierzytelnianie użytkownika podróże za pomocą niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="1987a-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="1987a-112">Opisano krok po kroku jako wymiany podróże użytkownika od dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1987a-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="1987a-113">Zdefiniuj rozgałęzień warunkowych w podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1987a-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="1987a-114">Integracja usług korzystających z interfejsu API REST w podróży użytkownika z uwierzytelniania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="1987a-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="1987a-115">Dodaj federacji z dostawców tożsamości, zgodnych z hello standardowe OpenIDConnect.</span><span class="sxs-lookup"><span data-stu-id="1987a-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="1987a-116">Dodaj federacji z dostawców tożsamości, zgodnymi z protokołem toohello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1987a-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="1987a-117">Warunki hello publicznej wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="1987a-117">Terms of hello public preview</span></span>

* <span data-ttu-id="1987a-118">Firma Microsoft zachęca toouse hello nowe funkcje wyłącznie do celów ewaluacyjnych.</span><span class="sxs-lookup"><span data-stu-id="1987a-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="1987a-119">Nowe funkcje nie są przeznaczone do użytku w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="1987a-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="1987a-120">Umowy dotyczące poziomu usług (SLA) nie należy stosować toohello nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="1987a-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="1987a-121">Żądania pomocy technicznej można złożyć za pośrednictwem kanałów regularne pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="1987a-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="1987a-122">Brak bez uzgodnionej daty dla ogólnej dostępności.</span><span class="sxs-lookup"><span data-stu-id="1987a-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="1987a-123">Nasze uznania z dowolnej przyczyny Microsoft może Flaga i odrzucić lub ograniczyć scenariuszy i podróże użytkownika, które wykraczają poza zakres hello hello Azure AD B2C produktu karty tooserve jako platformę zarządzania (CIAM) tożsamości i dostępu klienta.</span><span class="sxs-lookup"><span data-stu-id="1987a-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="1987a-124">Obowiązki deweloperów zestaw funkcji zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="1987a-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="1987a-125">Konfiguracja zasad ręczne przyznaje toohello niższego poziomu dostępu podstawowej platformy Azure AD B2C i powoduje tworzenie hello framework unikatowy zaufania można swobodnie dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="1987a-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="1987a-126">Możliwych kombinacji dostawców tożsamości niestandardowej, relacje zaufania, integracji z usługami zewnętrznych i przepływy pracy krok po kroku umieścić większe wymagania na powitania zaawansowane deweloperom korzystanie z nich.</span><span class="sxs-lookup"><span data-stu-id="1987a-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="1987a-127">toofully korzyści z publicznej wersji zapoznawczej hello, zaleca się, że deweloperów korzystających z zestawu funkcji niestandardowych zasad hello odpowiednia toohello następujące wytyczne:</span><span class="sxs-lookup"><span data-stu-id="1987a-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="1987a-128">Zapoznanie się z języka konfiguracji hello hello aparat obsługi tożsamości i klucz/klucze tajne zarządzania.</span><span class="sxs-lookup"><span data-stu-id="1987a-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="1987a-129">Przejmowanie na własność scenariuszy i niestandardowej integracji.</span><span class="sxs-lookup"><span data-stu-id="1987a-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="1987a-130">Testowanie metodyczny scenariusza.</span><span class="sxs-lookup"><span data-stu-id="1987a-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="1987a-131">Wykonaj rozwoju oprogramowania i przejściowych najlepszych rozwiązań z co najmniej jeden programowanie i środowiska testowego i jednego środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1987a-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="1987a-132">Aktualne informacje o nowych rozwiązań z hello dostawców tożsamości i usług, które można zintegrować z.</span><span class="sxs-lookup"><span data-stu-id="1987a-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="1987a-133">Na przykład śledzenie pracy w kluczy tajnych i planowanych i nieplanowanych zmiany toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="1987a-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="1987a-134">Konfigurowanie aktywnego monitorowania i monitorowanie czasu reakcji hello środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1987a-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="1987a-135">Aktualizuj adresy e-mail kontaktów i pozostać reakcji toohello Microsoft live witryny zespołu w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1987a-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="1987a-136">Podejmowania działań odpowiednim czasie, gdy zaleca toodo Witaj, Microsoft live witryny zespołu.</span><span class="sxs-lookup"><span data-stu-id="1987a-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="1987a-137">Te funkcje mogą ostatecznie dołączone wbudowane zasady usługi Azure AD, dzięki czemu deweloperzy tooall dostęp.</span><span class="sxs-lookup"><span data-stu-id="1987a-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1987a-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1987a-138">Next steps</span></span>
<span data-ttu-id="1987a-139">[Wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1987a-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
