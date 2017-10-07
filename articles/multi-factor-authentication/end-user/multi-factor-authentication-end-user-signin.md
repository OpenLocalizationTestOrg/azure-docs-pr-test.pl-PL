---
title: aaaAzure MFA logowania w trakcie weryfikacji dwuetapowej | Dokumentacja firmy Microsoft
description: "Ta strona pozwoli wskazówki na którym toogo toosee hello różne metody logowania dostępny za pomocą usługi Azure MFA."
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
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="854c1-104">Witaj logowania z usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="854c1-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="854c1-105">Celem tego artykułu Hello jest toowalk za pomocą typowego środowiska logowania.</span><span class="sxs-lookup"><span data-stu-id="854c1-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="854c1-106">Aby uzyskać pomoc dotyczącą zalogować się lub tootroubleshoot problemów, zobacz [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="854c1-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="854c1-107">Jakie będzie środowisko logowania</span><span class="sxs-lookup"><span data-stu-id="854c1-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="854c1-108">Środowisko logowania różni się w zależności od tego, co możesz wybrać toouse jako Twoje czynnika: połączenie telefoniczne, aplikacja uwierzytelniania lub tekstów.</span><span class="sxs-lookup"><span data-stu-id="854c1-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="854c1-109">Wybierz opcję hello, która najlepiej opisuje czynności:</span><span class="sxs-lookup"><span data-stu-id="854c1-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="854c1-110">Jak możesz się zalogować?</span><span class="sxs-lookup"><span data-stu-id="854c1-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="854c1-111">Przy użyciu połączenia telefonicznego toomy telefon komórkowy lub office telefonu</span><span class="sxs-lookup"><span data-stu-id="854c1-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="854c1-112">Przy użyciu telefonu komórkowego toomy tekstu</span><span class="sxs-lookup"><span data-stu-id="854c1-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="854c1-113">Z powiadomienia z aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="854c1-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="854c1-114">Z kodów weryfikacyjnych z aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="854c1-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="854c1-115">Przy użyciu alternatywne metody ponieważ nie można użyć Moje preferowaną metodą w tej chwili</span><span class="sxs-lookup"><span data-stu-id="854c1-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="854c1-116">Logowanie się przy użyciu połączeń telefonicznych</span><span class="sxs-lookup"><span data-stu-id="854c1-116">Signing in with a phone call</span></span>
<span data-ttu-id="854c1-117">Witaj następujących informacji opisano doświadczenia weryfikacji dwuetapowej hello mobile tooyour wywołania lub telefon biurowy.</span><span class="sxs-lookup"><span data-stu-id="854c1-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="854c1-118">Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="854c1-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="854c1-119">Microsoft dzwoni do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="854c1-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="854c1-120">Odpowiedzi hello telefonu i naciśnij klawisz # hello.</span><span class="sxs-lookup"><span data-stu-id="854c1-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="854c1-121">Logowanie się przy użyciu wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="854c1-121">Signing in with a text message</span></span>
<span data-ttu-id="854c1-122">Witaj następujących informacji opisano środowisko weryfikacji dwuetapowej hello telefonu komórkowego tooyour wiadomości tekstowych:</span><span class="sxs-lookup"><span data-stu-id="854c1-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="854c1-123">Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="854c1-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="854c1-124">Firma Microsoft wysyła wiadomość tekstową zawierającą numer kodu.</span><span class="sxs-lookup"><span data-stu-id="854c1-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="854c1-125">Wprowadź kod hello w polu hello na powitania strony logowania.</span><span class="sxs-lookup"><span data-stu-id="854c1-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="854c1-126">Logowanie się przy użyciu aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="854c1-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="854c1-127">Witaj następujące informacje w tym artykule opisano hello środowisko przy użyciu aplikacji Microsoft Authenticator hello do weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="854c1-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="854c1-128">Istnieją dwa sposoby toouse hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="854c1-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="854c1-129">Na urządzeniu może odbierać powiadomienia wypychane, lub możesz otworzyć tooget aplikacji hello kod weryfikacyjny.</span><span class="sxs-lookup"><span data-stu-id="854c1-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="854c1-130">toosign się powiadomienie z aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="854c1-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="854c1-131">Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="854c1-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="854c1-132">Firma Microsoft wysyła aplikacji Microsoft Authenticator toohello powiadomienia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="854c1-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Firma Microsoft wysyła powiadomienia](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="854c1-134">Otwórz hello powiadomień na telefon i wybierz hello **Sprawdź** klucza.</span><span class="sxs-lookup"><span data-stu-id="854c1-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="854c1-135">Jeśli firma wymaga numeru PIN, wprowadź go tutaj.</span><span class="sxs-lookup"><span data-stu-id="854c1-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="854c1-136">Powinny teraz być zalogowano.</span><span class="sxs-lookup"><span data-stu-id="854c1-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="854c1-137">toosign przy użyciu kodu weryfikacyjnego z aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="854c1-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="854c1-138">Jeśli używasz kodów weryfikacyjnych tooget aplikacji Microsoft Authenticator hello, następnie po otwarciu aplikacji hello jest wyświetlana liczba pod nazwą konta.</span><span class="sxs-lookup"><span data-stu-id="854c1-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="854c1-139">Liczba ta zmienia co 30 sekund, aby nie używać hello tę samą liczbę dwa razy.</span><span class="sxs-lookup"><span data-stu-id="854c1-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="854c1-140">Gdy pojawi się monit o kod weryfikacyjny, Otwórz aplikację hello i używać dowolnej wartości są obecnie wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="854c1-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="854c1-141">Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="854c1-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="854c1-142">Microsoft wyświetla monit o podanie kodu weryfikacyjnego.</span><span class="sxs-lookup"><span data-stu-id="854c1-142">Microsoft prompts you for a verification code.</span></span>

  ![Wprowadź kod weryfikacyjny](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="854c1-144">Otwórz aplikację Microsoft Authenticator hello na telefonie i wprowadź kod hello w polu hello, w których logujesz.</span><span class="sxs-lookup"><span data-stu-id="854c1-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="854c1-145">Logowanie się przy użyciu alternatywnych — metoda</span><span class="sxs-lookup"><span data-stu-id="854c1-145">Signing in with an alternate method</span></span>
<span data-ttu-id="854c1-146">Czasami nie masz telefon hello lub urządzenia, które można skonfigurować jako metodę weryfikacji preferowanego.</span><span class="sxs-lookup"><span data-stu-id="854c1-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="854c1-147">Ta sytuacja jest, dlatego zaleca się skonfigurowanie metody wykonywania kopii zapasowej dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="854c1-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="854c1-148">Witaj poniższej sekcji przedstawiono sposób toosign się przy użyciu alternatywna metoda gdy podstawowej metody nie mogą być dostępne.</span><span class="sxs-lookup"><span data-stu-id="854c1-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="854c1-149">Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="854c1-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="854c1-150">Wybierz **użyć innej opcji weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="854c1-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="854c1-151">Widzisz opcji weryfikacji różnych opartych o ile masz Instalatora.</span><span class="sxs-lookup"><span data-stu-id="854c1-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="854c1-152">Wybierz alternatywną metodę i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="854c1-152">Choose an alternate method and sign in.</span></span>

  ![Należy użyć alternatywnej metody](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="854c1-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="854c1-154">Next steps</span></span>

<span data-ttu-id="854c1-155">Jeśli masz problemy z zarejestrowaniem się przy użyciu weryfikacji dwuetapowej, uzyskać więcej informacji o [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="854c1-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="854c1-156">Dowiedz się, jak za[zarządzać ustawieniami weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="854c1-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="854c1-157">Dowiedz się, jak za[wprowadzenie do aplikacji Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) tak, aby można było używać toosign powiadomienia, zamiast teksty i połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="854c1-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
