---
title: "aaaAzure uwierzytelnianie wieloskładnikowe — jak działa"
description: "Uwierzytelnianie wieloskładnikowe platformy Azure ułatwia zabezpieczenie dostępu toodata i aplikacje, spełniając zapotrzebowanie na prosty proces logowania. Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="3611c-104">Jak działa usługa Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3611c-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="3611c-105">zabezpieczenia Hello weryfikacji dwuetapowej znajduje się w jego warstwowego podejścia.</span><span class="sxs-lookup"><span data-stu-id="3611c-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="3611c-106">Naruszenie wiele czynników uwierzytelniania przedstawiono istotne wyzwanie osobom atakującym.</span><span class="sxs-lookup"><span data-stu-id="3611c-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="3611c-107">Nawet jeśli osoba atakująca zarządza toolearn hello hasło użytkownika, jest bezużyteczny bez również posiadanie hello zaufanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3611c-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Biurowego](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="3611c-109">Uwierzytelnianie wieloskładnikowe platformy Azure ułatwia zabezpieczenie dostępu toodata i aplikacje, spełniając zapotrzebowanie na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="3611c-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="3611c-110">Zawiera dodatkowe zabezpieczenia, gdyż drugiej formy uwierzytelniania i zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe.</span><span class="sxs-lookup"><span data-stu-id="3611c-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="3611c-111">Dostępne metody na potrzeby weryfikacji dwuetapowej</span><span class="sxs-lookup"><span data-stu-id="3611c-111">Methods available for two-step verification</span></span>
<span data-ttu-id="3611c-112">Gdy użytkownik się zaloguje, dodatkowej weryfikacji są wysyłane toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3611c-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="3611c-113">Witaj poniżej przedstawiono listę metod, które mogą być używane dla drugiego weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="3611c-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="3611c-114">Metoda weryfikacji</span><span class="sxs-lookup"><span data-stu-id="3611c-114">Verification Method</span></span> | <span data-ttu-id="3611c-115">Opis</span><span class="sxs-lookup"><span data-stu-id="3611c-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3611c-116">Połączenie telefoniczne</span><span class="sxs-lookup"><span data-stu-id="3611c-116">Phone call</span></span> |<span data-ttu-id="3611c-117">Wywołanie jest umieszczany w zarejestrowany telefon użytkownika tooa.</span><span class="sxs-lookup"><span data-stu-id="3611c-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="3611c-118">Hello użytkownik wprowadza numeru PIN, jeśli to konieczne, a następnie naciska klawisz # hello.</span><span class="sxs-lookup"><span data-stu-id="3611c-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="3611c-119">Wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="3611c-119">Text message</span></span> |<span data-ttu-id="3611c-120">Wiadomość SMS są wysyłane telefon komórkowy tooa użytkownika z sześciocyfrowy kod.</span><span class="sxs-lookup"><span data-stu-id="3611c-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="3611c-121">Witaj użytkownik wprowadza ten kod na powitania strony logowania.</span><span class="sxs-lookup"><span data-stu-id="3611c-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="3611c-122">Powiadomienie aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="3611c-122">Mobile app notification</span></span> |<span data-ttu-id="3611c-123">Smartfon użytkownika tooa wysłaniu żądania weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="3611c-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="3611c-124">Witaj użytkownik wprowadza numeru PIN, jeśli to konieczne, a następnie wybiera **Sprawdź** na powitania aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="3611c-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="3611c-125">Kod weryfikacyjny z aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="3611c-125">Mobile app verification code</span></span> |<span data-ttu-id="3611c-126">aplikacji mobilnej Hello, w którym jest uruchomiony przez użytkownika smartfon, wyświetla kod weryfikacyjny, który zmienia co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="3611c-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="3611c-127">Użytkownik Hello hello najnowszych kodu i wprowadza ją na powitania strony logowania.</span><span class="sxs-lookup"><span data-stu-id="3611c-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="3611c-128">Tokeny OATH innej firmy</span><span class="sxs-lookup"><span data-stu-id="3611c-128">Third-party OATH tokens</span></span> | <span data-ttu-id="3611c-129">Azure aplikacji serwer Multi-Factor Authentication może być skonfigurowany tooaccept metody weryfikacji innych firm.</span><span class="sxs-lookup"><span data-stu-id="3611c-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="3611c-130">Uwierzytelnianie wieloskładnikowe platformy Azure udostępnia metody weryfikacji selectable dla chmurą i z serwera.</span><span class="sxs-lookup"><span data-stu-id="3611c-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="3611c-131">Można wybrać, które metody są dostępne dla użytkowników: połączenie telefoniczne, tekst, powiadomienie aplikacji lub kody aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3611c-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="3611c-132">Aby uzyskać więcej informacji, zobacz [metody weryfikacji počítačů, které](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="3611c-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3611c-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3611c-133">Next steps</span></span>

- <span data-ttu-id="3611c-134">Przeczytaj informacje o różnych hello [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="3611c-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="3611c-135">Wybierz czy toodeploy usługi Azure MFA [w chmurze hello lub lokalnie](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3611c-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="3611c-136">Odczyt odpowiada [— często zadawane pytania](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3611c-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>