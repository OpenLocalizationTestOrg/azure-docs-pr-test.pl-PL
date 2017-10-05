---
title: Azure MFA logowania w trakcie weryfikacji dwuetapowej | Dokumentacja firmy Microsoft
description: "Ta strona pozwoli wskazówki na gdzie można wyświetlić różnych logowania dostępne metody za pomocą usługi Azure MFA."
keywords: "Uwierzytelnianie użytkownika, logowania, zarejestruj się przy użyciu telefonu komórkowego, zarejestruj się przy użyciu telefonu biurowego"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="3501e-104">Środowisko logowania w usłudze Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3501e-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="3501e-105">Celem tego artykułu jest przeprowadzenie typowe środowiska logowania.</span><span class="sxs-lookup"><span data-stu-id="3501e-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="3501e-106">Aby uzyskać pomoc, z zalogowaniem lub rozwiązywania problemów, zobacz [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="3501e-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="3501e-107">Jakie będzie środowisko logowania</span><span class="sxs-lookup"><span data-stu-id="3501e-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="3501e-108">Środowisko logowania różni się w zależności od wyboru do użycia jako Twoje czynnika: połączenie telefoniczne, aplikacja uwierzytelniania lub tekstów.</span><span class="sxs-lookup"><span data-stu-id="3501e-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="3501e-109">Wybierz opcję, która najlepiej opisuje czynności:</span><span class="sxs-lookup"><span data-stu-id="3501e-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="3501e-110">Jak możesz się zalogować?</span><span class="sxs-lookup"><span data-stu-id="3501e-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="3501e-111">Z telefoniczne Mój telefon komórkowy lub pakietu office</span><span class="sxs-lookup"><span data-stu-id="3501e-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="3501e-112">Tekst na Mój telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="3501e-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="3501e-113">Z powiadomienia z aplikacji Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="3501e-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="3501e-114">Z kodów weryfikacyjnych z aplikacji Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="3501e-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="3501e-115">Przy użyciu alternatywne metody ponieważ nie można użyć Moje preferowaną metodą w tej chwili</span><span class="sxs-lookup"><span data-stu-id="3501e-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="3501e-116">Logowanie się przy użyciu połączeń telefonicznych</span><span class="sxs-lookup"><span data-stu-id="3501e-116">Signing in with a phone call</span></span>
<span data-ttu-id="3501e-117">Poniżej opisano środowisko weryfikacji dwuetapowej przy użyciu wywołania na Twój telefon komórkowy lub pakietu office.</span><span class="sxs-lookup"><span data-stu-id="3501e-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="3501e-118">Zaloguj się do aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="3501e-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="3501e-119">Microsoft dzwoni do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3501e-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="3501e-120">Odbierz połączenie i naciśnij klawisz #.</span><span class="sxs-lookup"><span data-stu-id="3501e-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="3501e-121">Logowanie się przy użyciu wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="3501e-121">Signing in with a text message</span></span>
<span data-ttu-id="3501e-122">Poniżej opisano środowisko weryfikacji dwuetapowej z wiadomość SMS na telefon komórkowy:</span><span class="sxs-lookup"><span data-stu-id="3501e-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="3501e-123">Zaloguj się do aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="3501e-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="3501e-124">Firma Microsoft wysyła wiadomość tekstową zawierającą numer kodu.</span><span class="sxs-lookup"><span data-stu-id="3501e-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="3501e-125">Wprowadź kod w polu dostępnym na stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="3501e-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="3501e-126">Logowanie się przy użyciu aplikacji uwierzytelniania firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3501e-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="3501e-127">Poniższe informacje zawierają opis korzystania z aplikacji Microsoft Authenticator dla weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="3501e-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="3501e-128">Istnieją dwa różne sposoby korzystania z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3501e-128">There are two different ways to use the app.</span></span> <span data-ttu-id="3501e-129">Na urządzeniu może odbierać powiadomienia wypychane, lub możesz otworzyć aplikację, aby kod weryfikacyjny.</span><span class="sxs-lookup"><span data-stu-id="3501e-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="3501e-130">Aby zalogować się przy użyciu powiadomienie z aplikacji Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="3501e-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="3501e-131">Zaloguj się do aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="3501e-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="3501e-132">Microsoft wysyła powiadomienie do aplikacji Microsoft Authenticator na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="3501e-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Firma Microsoft wysyła powiadomienia](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="3501e-134">Otwórz powiadomienie na telefon i wybierz **Sprawdź** klucza.</span><span class="sxs-lookup"><span data-stu-id="3501e-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="3501e-135">Jeśli firma wymaga numeru PIN, wprowadź go tutaj.</span><span class="sxs-lookup"><span data-stu-id="3501e-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="3501e-136">Powinny teraz być zalogowano.</span><span class="sxs-lookup"><span data-stu-id="3501e-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="3501e-137">Aby zalogować się przy użyciu kodu weryfikacyjnego z aplikacji Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="3501e-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="3501e-138">Jeśli używasz aplikacji Microsoft Authenticator uzyskać kodów weryfikacji, następnie po otwarciu aplikacji jest wyświetlana liczba pod nazwą konta.</span><span class="sxs-lookup"><span data-stu-id="3501e-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="3501e-139">Liczba ta zmienia co 30 sekund, aby nie używać tego samego numeru dwa razy.</span><span class="sxs-lookup"><span data-stu-id="3501e-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="3501e-140">Gdy pojawi się monit o kod weryfikacyjny, Otwórz aplikację i używać dowolnej wartości są obecnie wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="3501e-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="3501e-141">Zaloguj się do aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="3501e-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="3501e-142">Microsoft wyświetla monit o podanie kodu weryfikacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3501e-142">Microsoft prompts you for a verification code.</span></span>

  ![Wprowadź kod weryfikacyjny](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="3501e-144">Otwórz aplikację Microsoft Authenticator na telefonie i wprowadź kod w polu, w których logujesz.</span><span class="sxs-lookup"><span data-stu-id="3501e-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="3501e-145">Logowanie się przy użyciu alternatywnych — metoda</span><span class="sxs-lookup"><span data-stu-id="3501e-145">Signing in with an alternate method</span></span>
<span data-ttu-id="3501e-146">Czasami nie masz telefon lub urządzenia, które można skonfigurować jako metodę weryfikacji preferowanego.</span><span class="sxs-lookup"><span data-stu-id="3501e-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="3501e-147">Ta sytuacja jest, dlatego zaleca się skonfigurowanie metody wykonywania kopii zapasowej dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="3501e-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="3501e-148">Poniższej sekcji przedstawiono sposób Zaloguj się przy użyciu alternatywną metodę, gdy podstawowej metody nie mogą być dostępne.</span><span class="sxs-lookup"><span data-stu-id="3501e-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="3501e-149">Zaloguj się do aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="3501e-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="3501e-150">Wybierz **użyć innej opcji weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="3501e-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="3501e-151">Widzisz opcji weryfikacji różnych opartych o ile masz Instalatora.</span><span class="sxs-lookup"><span data-stu-id="3501e-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="3501e-152">Wybierz alternatywną metodę i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="3501e-152">Choose an alternate method and sign in.</span></span>

  ![Należy użyć alternatywnej metody](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="3501e-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3501e-154">Next steps</span></span>

<span data-ttu-id="3501e-155">Jeśli masz problemy z zarejestrowaniem się przy użyciu weryfikacji dwuetapowej, uzyskać więcej informacji o [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="3501e-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="3501e-156">Dowiedz się, jak [zarządzać ustawieniami weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="3501e-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="3501e-157">Dowiedz się, jak [wprowadzenie do aplikacji Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tak, aby powiadomienia można użyć do logowania zamiast teksty i połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="3501e-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 