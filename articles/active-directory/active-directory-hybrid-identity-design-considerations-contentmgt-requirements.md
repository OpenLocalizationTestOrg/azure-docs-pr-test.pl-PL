---
title: "Azure Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących zarządzania zawartością | Dokumentacja firmy Microsoft"
description: "Zapewnia wgląd w sposób określenie wymagań w zakresie zarządzania zawartością firmy. Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z aplikacji, której używa. Należy do odróżnienia zawartość została utworzona przy użyciu poświadczeń osobistego od komputerów utworzone przy użyciu poświadczeń firmowych. Rozwiązania tożsamości powinny mieć możliwość interakcji z chmurą services, aby umożliwić nie zakłóca pracy użytkownika końcowego podczas zapewnienia prywatności i zwiększenia ochrony przed wyciekiem danych."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="a4d84-106">Określenie wymagań dotyczących zarządzania zawartością dla rozwiązania z tożsamością hybrydową</span><span class="sxs-lookup"><span data-stu-id="a4d84-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="a4d84-107">Zapoznanie się z wymaganiami zarządzania zawartością w firmie może bezpośrednio wpływa na na decyzję dotyczącą rozwiązania hybrydowe tożsamości do użycia.</span><span class="sxs-lookup"><span data-stu-id="a4d84-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="a4d84-108">Rosnąca liczba wiele urządzeń i możliwość przynoszą własne urządzenia użytkowników ([BYOD](http://aka.ms/byodcg)), firmy muszą chronić własnych danych, ale jego również należy zachowane prywatność użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a4d84-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="a4d84-109">Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z aplikacji, której używa.</span><span class="sxs-lookup"><span data-stu-id="a4d84-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="a4d84-110">Należy do odróżnienia zawartość została utworzona przy użyciu poświadczeń osobistego od komputerów utworzone przy użyciu poświadczeń firmowych.</span><span class="sxs-lookup"><span data-stu-id="a4d84-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="a4d84-111">Rozwiązania tożsamości powinny mieć możliwość interakcji z chmurą services, aby umożliwić nie zakłóca pracy użytkownika końcowego podczas zapewnienia prywatności i zwiększenia ochrony przed wyciekiem danych.</span><span class="sxs-lookup"><span data-stu-id="a4d84-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="a4d84-112">Rozwiązania tożsamości będą wykorzystywane przez inną kontrolę techniczną w celu zapewnienia zarządzania zawartością, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="a4d84-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="a4d84-113">**Opcji zabezpieczeń, które będą wykorzystaniu systemu zarządzania tożsamościami**</span><span class="sxs-lookup"><span data-stu-id="a4d84-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="a4d84-114">Ogólnie rzecz biorąc wymagania dotyczące zarządzania zawartością będzie korzystać z systemu zarządzania tożsamościami w następujących obszarach:</span><span class="sxs-lookup"><span data-stu-id="a4d84-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="a4d84-115">Ochrona prywatności: identyfikacji użytkownika, który jest właścicielem zasobu i stosowania kontrole w celu zachowania integralności.</span><span class="sxs-lookup"><span data-stu-id="a4d84-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="a4d84-116">Klasyfikacja danych: identyfikacji użytkownika lub grupy i poziom dostępu do obiektu zgodnie z ich klasyfikację.</span><span class="sxs-lookup"><span data-stu-id="a4d84-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="a4d84-117">Ochrona wycieku danych: wyłączną odpowiedzialność za ochronę danych, aby uniknąć wycieków kontroli bezpieczeństwa należy wchodzić w interakcje z systemu tożsamości w celu weryfikowania tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4d84-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="a4d84-118">To ważne jest również cel dziennik inspekcji.</span><span class="sxs-lookup"><span data-stu-id="a4d84-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="a4d84-119">Odczyt [klasyfikacji danych pod kątem gotowości do chmury](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) Aby uzyskać więcej informacji na temat najlepszych rozwiązań i wytyczne dotyczące klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="a4d84-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="a4d84-120">Podczas planowania rozwiązania z tożsamością hybrydową upewnij się, że zgodnie z wymaganiami organizacji są odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="a4d84-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="a4d84-121">Czy firma dysponuje kontroli zabezpieczeń w celu wymuszenia prywatność danych</span><span class="sxs-lookup"><span data-stu-id="a4d84-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="a4d84-122">Jeśli tak, będzie tych opcji zabezpieczeń można zintegrować z rozwiązania z tożsamością hybrydową, które zamierzasz wdrożyć usługę?</span><span class="sxs-lookup"><span data-stu-id="a4d84-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a4d84-123">Czy firma korzysta klasyfikacji danych?</span><span class="sxs-lookup"><span data-stu-id="a4d84-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="a4d84-124">Jeśli tak, jest możliwość integracji z rozwiązania z tożsamością hybrydową, które zamierzasz wdrożyć usługę bieżące rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="a4d84-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a4d84-125">Czy firma ma obecnie wszystkie rozwiązania do wycieku danych?</span><span class="sxs-lookup"><span data-stu-id="a4d84-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="a4d84-126">Jeśli tak, jest możliwość integracji z rozwiązania z tożsamością hybrydową, które zamierzasz wdrożyć usługę bieżące rozwiązanie?</span><span class="sxs-lookup"><span data-stu-id="a4d84-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a4d84-127">Czy firma musi inspekcji dostępu do zasobów?</span><span class="sxs-lookup"><span data-stu-id="a4d84-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="a4d84-128">Jeśli tak, jakiego typu zasobów?</span><span class="sxs-lookup"><span data-stu-id="a4d84-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="a4d84-129">Jeśli tak, jakie informacje są niezbędne?</span><span class="sxs-lookup"><span data-stu-id="a4d84-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="a4d84-130">Jeśli tak, gdy dziennik inspekcji muszą znajdować się?</span><span class="sxs-lookup"><span data-stu-id="a4d84-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="a4d84-131">Lokalnie lub w chmurze?</span><span class="sxs-lookup"><span data-stu-id="a4d84-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="a4d84-132">Czy firma musi szyfrowania żadnych wiadomości e-mail zawierających poufne dane (numerów PESEL, numerów kart kredytowych, itp.)?</span><span class="sxs-lookup"><span data-stu-id="a4d84-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="a4d84-133">Czy firma musi szyfrować wszystkie dokumenty/zawartości udostępnione zewnętrznymi partnerami biznesowymi?</span><span class="sxs-lookup"><span data-stu-id="a4d84-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="a4d84-134">Czy firma potrzebuje wymuszanie zasad firmowych na określonych rodzajów wiadomości e-mail (nie ma wszystkich odpowiedzi, nie przekazuj)?</span><span class="sxs-lookup"><span data-stu-id="a4d84-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="a4d84-135">Upewnij się zanotować wszystkie odpowiedzi i zrozumieć ich uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="a4d84-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="a4d84-136">[Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane dostępne opcje oraz zalety/wady każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="a4d84-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="a4d84-137">Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.</span><span class="sxs-lookup"><span data-stu-id="a4d84-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a4d84-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4d84-138">Next steps</span></span>
[<span data-ttu-id="a4d84-139">Określenie wymagań dotyczących kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="a4d84-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a4d84-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a4d84-140">See Also</span></span>
[<span data-ttu-id="a4d84-141">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="a4d84-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

