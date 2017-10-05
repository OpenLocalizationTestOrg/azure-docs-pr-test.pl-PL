---
title: "Uwierzytelnianie wieloskładnikowe platformy Azure — jak działa"
description: "Usługa Azure Multi-Factor Authentication zabezpiecza dostęp do danych i aplikacji, a jednocześnie spełnia wymagania użytkowników dotyczące prostoty procesu logowania. Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="a3821-104">Jak działa usługa Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="a3821-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="a3821-105">Zabezpieczenia weryfikacji dwuetapowej znajduje się w jego warstwowego podejścia.</span><span class="sxs-lookup"><span data-stu-id="a3821-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="a3821-106">Naruszenie wiele czynników uwierzytelniania przedstawiono istotne wyzwanie osobom atakującym.</span><span class="sxs-lookup"><span data-stu-id="a3821-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="a3821-107">Nawet jeśli osoba atakująca zarządza się hasło użytkownika, jest bezużyteczny bez również dostęp do zaufanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3821-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Biurowego](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="a3821-109">Usługa Azure Multi-Factor Authentication zabezpiecza dostęp do danych i aplikacji, a jednocześnie spełnia wymagania użytkowników dotyczące prostoty procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="a3821-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="a3821-110">Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe.</span><span class="sxs-lookup"><span data-stu-id="a3821-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="a3821-111">Dostępne metody na potrzeby weryfikacji dwuetapowej</span><span class="sxs-lookup"><span data-stu-id="a3821-111">Methods available for two-step verification</span></span>
<span data-ttu-id="a3821-112">Gdy użytkownik się zaloguje, dodatkowej weryfikacji są wysyłane do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3821-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="a3821-113">Poniżej przedstawiono listę metod, które mogą być używane dla drugiego weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="a3821-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="a3821-114">Metoda weryfikacji</span><span class="sxs-lookup"><span data-stu-id="a3821-114">Verification Method</span></span> | <span data-ttu-id="a3821-115">Opis</span><span class="sxs-lookup"><span data-stu-id="a3821-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3821-116">Połączenie telefoniczne</span><span class="sxs-lookup"><span data-stu-id="a3821-116">Phone call</span></span> |<span data-ttu-id="a3821-117">Wywołanie jest umieszczany zarejestrowanego telefonem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3821-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="a3821-118">Użytkownik wprowadza numeru PIN, jeśli to konieczne następnie naciska klawisz #.</span><span class="sxs-lookup"><span data-stu-id="a3821-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="a3821-119">Wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="a3821-119">Text message</span></span> |<span data-ttu-id="a3821-120">Wiadomość SMS są wysyłane na telefon komórkowy użytkownika z sześciocyfrowy kod.</span><span class="sxs-lookup"><span data-stu-id="a3821-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="a3821-121">Na stronie logowania, użytkownik wprowadza tego kodu.</span><span class="sxs-lookup"><span data-stu-id="a3821-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="a3821-122">Powiadomienie aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="a3821-122">Mobile app notification</span></span> |<span data-ttu-id="a3821-123">Żądanie weryfikacji jest wysyłane do smartfon użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3821-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="a3821-124">Użytkownik wprowadza numeru PIN, jeśli to konieczne, a następnie wybiera **Sprawdź** za pomocą aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a3821-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="a3821-125">Kod weryfikacyjny z aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="a3821-125">Mobile app verification code</span></span> |<span data-ttu-id="a3821-126">Aplikacji mobilnej, w którym jest uruchomiony przez użytkownika smartfon, wyświetla kod weryfikacyjny, który zmienia co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="a3821-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="a3821-127">Najnowsze kodu i wstawia go na stronie logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3821-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="a3821-128">Tokeny OATH innej firmy</span><span class="sxs-lookup"><span data-stu-id="a3821-128">Third-party OATH tokens</span></span> | <span data-ttu-id="a3821-129">Azure aplikacji serwer Multi-Factor Authentication mogą być skonfigurowane do akceptowania metody weryfikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="a3821-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="a3821-130">Uwierzytelnianie wieloskładnikowe platformy Azure udostępnia metody weryfikacji selectable dla chmurą i z serwera.</span><span class="sxs-lookup"><span data-stu-id="a3821-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="a3821-131">Można wybrać, które metody są dostępne dla użytkowników: połączenie telefoniczne, tekst, powiadomienie aplikacji lub kody aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3821-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="a3821-132">Aby uzyskać więcej informacji, zobacz [metody weryfikacji počítačů, které](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="a3821-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3821-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3821-133">Next steps</span></span>

- <span data-ttu-id="a3821-134">Przeczytaj informacje o różnych [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="a3821-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="a3821-135">Określ, czy do wdrożenia usługi Azure MFA [w chmurze lub lokalnie](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a3821-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="a3821-136">Odczyt odpowiada [— często zadawane pytania](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a3821-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>