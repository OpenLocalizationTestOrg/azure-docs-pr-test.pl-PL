---
title: aaaManage ustawienia weryfikacji dwuetapowej | Dokumentacja firmy Microsoft
description: "Zarządzanie, jak używasz usługi Azure Multi-Factor Authentication, włącznie ze zmianami swoje informacje kontaktowe i konfigurowanie urządzenia."
services: multi-factor-authentication
keywords: "Klient uwierzytelniania wieloskładnikowego, problem z uwierzytelnianiem, identyfikator korelacji"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="46742-104">Zarządzanie ustawieniami na potrzeby weryfikacji dwuetapowej</span><span class="sxs-lookup"><span data-stu-id="46742-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="46742-105">Ten artykuł zawiera odpowiedzi na pytania dotyczące ustawień tooupdate uwierzytelnianie dwuetapowe weryfikacji lub Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="46742-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="46742-106">Jeśli występują problemy dotyczące logowania konta tooyour, zapoznaj się zbyt[wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md) dla pomocy w rozwiązywaniu problemów.</span><span class="sxs-lookup"><span data-stu-id="46742-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="46742-107">Gdzie toofind hello ustawienia strony</span><span class="sxs-lookup"><span data-stu-id="46742-107">Where toofind hello settings page</span></span>
<span data-ttu-id="46742-108">W zależności od tego, jak firma skonfigurowane uwierzytelnianie wieloskładnikowe Azure istnieje kilka miejsc, w którym można zmienić ustawienia, takie jak numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="46742-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="46742-109">Jeśli administrator IT wysłane z określonym adresem URL lub weryfikacji dwuetapowej toomanage kroki, wykonaj te instrukcje.</span><span class="sxs-lookup"><span data-stu-id="46742-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="46742-110">W przeciwnym razie hello instrukcjami powinny działać na każdy inny.</span><span class="sxs-lookup"><span data-stu-id="46742-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="46742-111">Jeśli wykonaj następujące kroki, ale nie widzisz hello tych samych opcji, które oznacza, że konto służbowe dostosowanego własnych portalu.</span><span class="sxs-lookup"><span data-stu-id="46742-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="46742-112">Poproś administratora portalu Azure Multi-Factor Authentication tooyour łącze hello.</span><span class="sxs-lookup"><span data-stu-id="46742-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="46742-113">Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="46742-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="46742-114">Wybierz nazwę konta w prawym górnym hello, a następnie wybierz **profilu**.</span><span class="sxs-lookup"><span data-stu-id="46742-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="46742-115">Wybierz **dodatkowej weryfikacji zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="46742-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="46742-117">ładuje Hello dodatkowe zabezpieczenia weryfikacji strony z ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="46742-117">hello Additional security verification page loads with your settings.</span></span>

    ![Biurowego](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="46742-119">Mają toochange mój numer telefonu lub dodać dodatkowej numer</span><span class="sxs-lookup"><span data-stu-id="46742-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="46742-120">Jest ważne tooconfigure numer telefonu uwierzytelniania dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="46742-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="46742-121">Ponieważ na serwerze podstawowym phone liczba i aplikacji mobilnej są prawdopodobnie na powitania sam telefonu, numeru telefonu dodatkowej hello jest jedynym sposobem hello, będzie możliwe tooget do swojego konta Jeśli telefon zostanie utracony lub skradziony.</span><span class="sxs-lookup"><span data-stu-id="46742-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="46742-122">Jeśli nie masz dostępu tooyour głównego numeru telefonu i potrzebujesz pomocy w tooyour konta, zobacz nasze tematy pomocy w [wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="46742-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="46742-123">**toochange Twojego podstawowy numer telefonu:**</span><span class="sxs-lookup"><span data-stu-id="46742-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="46742-124">Na stronie weryfikacji dodatkowe zabezpieczenia hello zaznacz pole tekstowe hello bieżący numer telefonu i edytować za pomocą nowy numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="46742-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="46742-125">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="46742-125">Select **Save**.</span></span>  
3. <span data-ttu-id="46742-126">Jeśli jest to numer hello używany dla Twojego preferowaną opcję weryfikacji, masz tooverify hello nowy numer, zanim będzie można go zapisać.</span><span class="sxs-lookup"><span data-stu-id="46742-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="46742-127">**tooadd numeru telefonu dodatkowej:**</span><span class="sxs-lookup"><span data-stu-id="46742-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="46742-128">Na stronie weryfikacji dodatkowe zabezpieczenia hello hello pole wyboru obok zbyt**numer telefonu uwierzytelniania alternatywny.**</span><span class="sxs-lookup"><span data-stu-id="46742-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="46742-129">Wprowadź numer telefonu pomocniczy w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="46742-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="46742-130">Wybierz **zapisać** i zakończeniu zmiany.</span><span class="sxs-lookup"><span data-stu-id="46742-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="46742-131">Żądaj weryfikacji dwuetapowej ponownie na urządzeniu, które zostały oznaczone jako zaufany</span><span class="sxs-lookup"><span data-stu-id="46742-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="46742-132">W zależności od ustawienia organizacji może być stwierdzający, pole wyboru "nie pytaj ponownie o **X** dni" po wykonaniu weryfikacji dwuetapowej w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="46742-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="46742-133">Jeśli to pole wyboru i utraty urządzenia lub podejrzenie, że Twoje konto jest zagrożone należy przywrócić tooall weryfikacji dwuetapowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="46742-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="46742-134">Na stronie weryfikacji dodatkowe zabezpieczenia hello zaznacz **przywracania usługi Multi-Factor authentication na wcześniej zaufanych urządzeniach**.</span><span class="sxs-lookup"><span data-stu-id="46742-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="46742-135">Witaj następnym zalogowaniu się na dowolnym urządzeniu będzie tooperform zostanie wyświetlony monit o weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="46742-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="46742-136">Jak wyczyścić Authenticator firmy Microsoft z urządzeniem stary i Przenieś tooa nową?</span><span class="sxs-lookup"><span data-stu-id="46742-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="46742-137">Po odinstalowaniu aplikacji hello z urządzenia lub resetowania urządzenia hello aktywacji hello na zapleczu hello nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="46742-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="46742-138">Aby uzyskać więcej informacji, zobacz [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="46742-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46742-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="46742-139">Next steps</span></span>
* <span data-ttu-id="46742-140">Uzyskać porady dotyczące rozwiązywania problemów i pomoc na temat [wystąpił problem w trakcie weryfikacji dwuetapowej](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="46742-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="46742-141">Konfigurowanie [hasła aplikacji](multi-factor-authentication-end-user-app-passwords.md) dla wszystkich aplikacji, które nie obsługują weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="46742-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
