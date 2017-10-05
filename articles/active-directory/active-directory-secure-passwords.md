---
title: "Usługi Azure AD do warstwy zabezpieczeń hasła | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak usługi Azure AD wymusza silne hasła i uniemożliwia hasła użytkowników przez przestępców,"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="2c2a0-103">To podejście wielowarstwowych zabezpieczeń hasła usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c2a0-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="2c2a0-104">W tym artykule omówiono najlepsze rozwiązania można wykonać jako użytkownik lub administrator do ochrony usługi Azure Active Directory (Azure AD) Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="2c2a0-105">Administratorzy usług Azure AD można zresetować hasło użytkownika za pomocą wskazówki zawarte w artykule [resetowania hasła dla użytkownika w usłudze Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="2c2a0-106">Użytkownicy mogą resetować swoje hasła przy użyciu wskazówek w następującym artykule w [pomocy nie pamiętam hasła usługi Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="2c2a0-107">Wymagania dotyczące hasła</span><span class="sxs-lookup"><span data-stu-id="2c2a0-107">Password requirements</span></span>

<span data-ttu-id="2c2a0-108">Usługa Azure AD zapewnia następujące popularne podejścia do zabezpieczania haseł:</span><span class="sxs-lookup"><span data-stu-id="2c2a0-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="2c2a0-109">Wymagania dotyczące długości hasła</span><span class="sxs-lookup"><span data-stu-id="2c2a0-109">Password length requirements</span></span>
* <span data-ttu-id="2c2a0-110">Wymagania dotyczące złożoności hasła</span><span class="sxs-lookup"><span data-stu-id="2c2a0-110">Password complexity requirements</span></span>
* <span data-ttu-id="2c2a0-111">Regularne i okresowe wygasanie haseł</span><span class="sxs-lookup"><span data-stu-id="2c2a0-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="2c2a0-112">Aby uzyskać informacje o resetowania w usłudze Azure Active Directory, zobacz temat [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="2c2a0-113">Zabezpieczenia hasła w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c2a0-113">Azure AD password protections</span></span>

<span data-ttu-id="2c2a0-114">Usługi Azure AD i System obsługi kont Microsoft Użyj branży sprawdzonych metod w celu zabezpieczenia bezpiecznych haseł użytkowników i administratora, w tym:</span><span class="sxs-lookup"><span data-stu-id="2c2a0-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="2c2a0-115">Hasła dynamicznie zakazane</span><span class="sxs-lookup"><span data-stu-id="2c2a0-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="2c2a0-116">Inteligentna blokada haseł</span><span class="sxs-lookup"><span data-stu-id="2c2a0-116">Smart Password Lockout</span></span>

<span data-ttu-id="2c2a0-117">Informacji na temat zarządzania hasłami oparte na bieżącej badań, można znaleźć w dokumencie [wskazówki dotyczące hasła](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="2c2a0-118">Hasła dynamicznie zakazane</span><span class="sxs-lookup"><span data-stu-id="2c2a0-118">Dynamically banned passwords</span></span>

<span data-ttu-id="2c2a0-119">Usługi Azure AD i Accounts Microsoft zabezpieczenia ochrony hasłem przez dynamicznie zakaz często używanych haseł.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="2c2a0-120">Zespół ds. usługi Azure ID Identity Protection regularnie analizuje listy zakazanych haseł, zapobiegając stosowaniu powszechnie używanych haseł przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="2c2a0-121">Ta usługa jest dostępna dla klientów usługi Azure AD i usługi konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="2c2a0-122">Podczas tworzenia haseł, jest ważne dla administratorów zachęcić pracowników do wybierz fraz hasła, które obejmują unikatowej kombinacji wartości litery, cyfry, znaki lub słowa.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="2c2a0-123">Takie podejście ułatwia niemal uniemożliwiają hasła użytkownika, którego bezpieczeństwo zostało naruszone ale łatwiejsze do zapamiętania przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="2c2a0-124">Naruszenia hasła</span><span class="sxs-lookup"><span data-stu-id="2c2a0-124">Password breaches</span></span>

<span data-ttu-id="2c2a0-125">Aby pozostać w jednym kroku wcześniejsze przez przestępców zawsze działa firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="2c2a0-126">Zespół ds. usługi Azure AD Identity Protection nieustannie analizuje często używane hasła.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="2c2a0-127">Cyberprzestępcy również często stosują podobne strategie do przeprowadzania ataków, na przykład tworzą [tęczowe tablice](https://en.wikipedia.org/wiki/Rainbow_table) w celu łamania skrótów haseł.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="2c2a0-128">Firma Microsoft stale analizuje [naruszenia danych](https://www.privacyrights.org/data-breaches) w celu utrzymania dynamicznie aktualizowanej listy zakazanych haseł, dzięki której narażone hasła są zakazywane, zanim staną się prawdziwym zagrożeniem dla klientów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="2c2a0-129">Więcej informacji o naszych bieżących działaniach związanych z zabezpieczeniami można znaleźć w raporcie analizy zabezpieczeń firmy Microsoft [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="2c2a0-130">Inteligentna blokada haseł</span><span class="sxs-lookup"><span data-stu-id="2c2a0-130">Smart Password Lockout</span></span>

<span data-ttu-id="2c2a0-131">Gdy usługa Azure AD wykryje próbę złamania hasła użytkownika przez potencjalnego przestępcę, blokujemy konto użytkownika przy użyciu funkcji inteligentnej blokady haseł.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="2c2a0-132">Usługę Azure AD zaprojektowano z myślą o określaniu ryzyka związanego z konkretnymi sesjami logowania.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="2c2a0-133">Następnie przy użyciu najbardziej aktualnych danych zabezpieczeń stosujemy semantyki blokady przestanie zagrożeniami przez.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="2c2a0-134">Jeśli użytkownik jest zablokowany z usługi Azure AD, ich ekran podobny do następującymi:</span><span class="sxs-lookup"><span data-stu-id="2c2a0-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Blokada w usłudze Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="2c2a0-136">W przypadku innych kont Microsoft ich ekranu wygląda podobnie do następującymi:</span><span class="sxs-lookup"><span data-stu-id="2c2a0-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Blokada konta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="2c2a0-138">Aby uzyskać informacje o resetowania w usłudze Azure Active Directory, zobacz temat [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a0-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="2c2a0-139">Jeśli jesteś administratorem usługi Azure AD, możesz użyć usługi [Windows Hello](https://www.microsoft.com/windows/windows-hello), aby całkowicie uniknąć tworzenia tradycyjnych haseł przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2c2a0-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="2c2a0-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c2a0-140">Next steps</span></span>

* [<span data-ttu-id="2c2a0-141">Jak zaktualizować własne hasło</span><span class="sxs-lookup"><span data-stu-id="2c2a0-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* <span data-ttu-id="2c2a0-142">[The fundamentals of Azure identity management](fundamentals-identity.md) (Podstawy zarządzania tożsamościami w usłudze Azure)</span><span class="sxs-lookup"><span data-stu-id="2c2a0-142">[The fundamentals of Azure identity management](fundamentals-identity.md)</span></span>
* [<span data-ttu-id="2c2a0-143">Aktywność resetowania raportów dotyczących hasła</span><span class="sxs-lookup"><span data-stu-id="2c2a0-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


