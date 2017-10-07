---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących zarządzania zawartością | Dokumentacja firmy Microsoft"
description: "Zapewnia wgląd w sposób toodetermine hello wymagania dotyczące zarządzania zawartością firmy. Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z toohello aplikacji, której używa. Jest ważne toodifferentiate zawartość została utworzona przy użyciu poświadczeń osobistych i hello te utworzone przy użyciu poświadczeń firmowych. Rozwiązanie tożsamości powinno być możliwe toointeract z tooprovide usługi w chmurze nie zakłóca pracy użytkownika końcowego dla toohello podczas zapewnienia prywatności i zwiększenia ochrona powitalnych przed wyciekiem danych."
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="19586-106">Określenie wymagań dotyczących zarządzania zawartością dla rozwiązania z tożsamością hybrydową</span><span class="sxs-lookup"><span data-stu-id="19586-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="19586-107">Wymagania dotyczące zarządzania zawartością hello opis dla Twojej firmy może bezpośrednia decyzję wpływ na które toouse rozwiązania tożsamości hybrydowej.</span><span class="sxs-lookup"><span data-stu-id="19586-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="19586-108">Z hello mnożenie wiele urządzeń i możliwości hello toobring użytkownikom ich własnych urządzeń ([BYOD](http://aka.ms/byodcg)), hello firmy muszą chronić własnych danych, ale jego również należy zachowane prywatność użytkowników.</span><span class="sxs-lookup"><span data-stu-id="19586-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="19586-109">Zazwyczaj gdy użytkownik ma swój własny urządzenia on może być również wiele poświadczeń, które będą naprzemiennych zgodnie z toohello aplikacji, której używa.</span><span class="sxs-lookup"><span data-stu-id="19586-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="19586-110">Jest ważne toodifferentiate zawartość została utworzona przy użyciu poświadczeń osobistych i hello te utworzone przy użyciu poświadczeń firmowych.</span><span class="sxs-lookup"><span data-stu-id="19586-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="19586-111">Rozwiązanie tożsamości powinno być możliwe toointeract z tooprovide usługi w chmurze nie zakłóca pracy użytkownika końcowego dla toohello podczas zapewnienia prywatności i zwiększenia ochrona powitalnych przed wyciekiem danych.</span><span class="sxs-lookup"><span data-stu-id="19586-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="19586-112">Rozwiązania tożsamości będzie można wykorzystywane przez różnych kontroli technicznej w zarządzania zawartością tooprovide kolejności, jak pokazano na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="19586-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="19586-113">**Opcji zabezpieczeń, które będą wykorzystaniu systemu zarządzania tożsamościami**</span><span class="sxs-lookup"><span data-stu-id="19586-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="19586-114">Ogólnie rzecz biorąc wymagania dotyczące zarządzania zawartością będzie korzystać z systemu zarządzania tożsamościami w hello następujące obszary:</span><span class="sxs-lookup"><span data-stu-id="19586-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="19586-115">Prywatność: identyfikacji hello użytkownika, który jest właścicielem zasobu i stosowania hello odpowiednie formanty toomaintain integralności.</span><span class="sxs-lookup"><span data-stu-id="19586-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="19586-116">Klasyfikacja danych: zidentyfikować hello użytkownika lub grupy i poziom dostępu do obiektów tooan zgodnie z klasyfikacją tooits.</span><span class="sxs-lookup"><span data-stu-id="19586-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="19586-117">Ochrona wycieku danych: wyłączną odpowiedzialność za ochronę danych tooavoid wyciek kontroli bezpieczeństwa należy toointeract z hello tożsamości systemu toovalidate hello tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="19586-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="19586-118">To ważne jest również cel dziennik inspekcji.</span><span class="sxs-lookup"><span data-stu-id="19586-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="19586-119">Odczyt [klasyfikacji danych pod kątem gotowości do chmury](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) Aby uzyskać więcej informacji na temat najlepszych rozwiązań i wytyczne dotyczące klasyfikacji danych.</span><span class="sxs-lookup"><span data-stu-id="19586-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="19586-120">Podczas planowania rozwiązania z tożsamością hybrydową upewnij się, że powitania po odpowiedzi na pytania zgodnie z wymaganiami organizacji tooyour:</span><span class="sxs-lookup"><span data-stu-id="19586-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="19586-121">Czy firma dysponuje kontroli bezpieczeństwa w miejscu tooenforce danych prywatności</span><span class="sxs-lookup"><span data-stu-id="19586-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="19586-122">Jeśli tak, te opcje zabezpieczeń będą mogli toointegrate z rozwiązania z tożsamością hybrydową hello czy tooadopt będzie?</span><span class="sxs-lookup"><span data-stu-id="19586-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="19586-123">Czy firma korzysta klasyfikacji danych?</span><span class="sxs-lookup"><span data-stu-id="19586-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="19586-124">Jeśli tak, jest hello bieżącego rozwiązania stanie toointegrate z rozwiązania z tożsamością hybrydową hello czy będzie tooadopt?</span><span class="sxs-lookup"><span data-stu-id="19586-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="19586-125">Czy firma ma obecnie wszystkie rozwiązania do wycieku danych?</span><span class="sxs-lookup"><span data-stu-id="19586-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="19586-126">Jeśli tak, jest hello bieżącego rozwiązania stanie toointegrate z rozwiązania z tożsamością hybrydową hello czy będzie tooadopt?</span><span class="sxs-lookup"><span data-stu-id="19586-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="19586-127">Czy firma potrzebuje tooaudit tooresources dostępu?</span><span class="sxs-lookup"><span data-stu-id="19586-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="19586-128">Jeśli tak, jakiego typu zasobów?</span><span class="sxs-lookup"><span data-stu-id="19586-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="19586-129">Jeśli tak, jakie informacje są niezbędne?</span><span class="sxs-lookup"><span data-stu-id="19586-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="19586-130">Jeśli tak, gdy dziennik inspekcji hello musi znajdować się?</span><span class="sxs-lookup"><span data-stu-id="19586-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="19586-131">Lokalnie lub w chmurze hello?</span><span class="sxs-lookup"><span data-stu-id="19586-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="19586-132">Czy firma potrzebuje tooencrypt żadnych wiadomości e-mail zawierających poufne dane (numerów PESEL, numerów kart kredytowych, itp.)?</span><span class="sxs-lookup"><span data-stu-id="19586-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="19586-133">Czy firma potrzebuje tooencrypt wszystkie dokumenty/zawartości udostępnione zewnętrznymi partnerami biznesowymi?</span><span class="sxs-lookup"><span data-stu-id="19586-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="19586-134">Czy firma potrzebuje tooenforce firmowych zasad na określonych rodzajów wiadomości e-mail (nie ma wszystkich odpowiedzi, nie przekazuj)?</span><span class="sxs-lookup"><span data-stu-id="19586-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="19586-135">Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="19586-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="19586-136">[Definiowanie strategii ochrony danych](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="19586-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="19586-137">Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.</span><span class="sxs-lookup"><span data-stu-id="19586-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="19586-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19586-138">Next steps</span></span>
[<span data-ttu-id="19586-139">Określenie wymagań dotyczących kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="19586-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="19586-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="19586-140">See Also</span></span>
[<span data-ttu-id="19586-141">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="19586-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

