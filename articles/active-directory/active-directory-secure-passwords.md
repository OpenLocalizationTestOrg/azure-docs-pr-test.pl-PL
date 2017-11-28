---
title: "aaaAzure AD do warstwy zabezpieczeń hasła | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="0d084-103">Wielowarstwowa podejście tooAzure AD hasło zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="0d084-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="0d084-104">W tym artykule omówiono najlepsze rozwiązania z usługi Azure Active Directory (Azure AD) lub Account Microsoft można wykonać jako użytkownik lub administrator tooprotect.</span><span class="sxs-lookup"><span data-stu-id="0d084-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="0d084-105">Administratorzy usług Azure AD mogą resetować hasła użytkownika przy użyciu wskazówek hello w artykule hello [hello zresetowano hasło użytkownika w usłudze Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0d084-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="0d084-106">Użytkownicy mogą resetować swoje hasła przy użyciu wskazówek hello w artykule hello [pomocy nie pamiętam hasła usługi Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="0d084-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="0d084-107">Wymagania dotyczące hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-107">Password requirements</span></span>

<span data-ttu-id="0d084-108">Usługi Azure AD zawiera następujące typowe hasła toosecuring podejścia hello:</span><span class="sxs-lookup"><span data-stu-id="0d084-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="0d084-109">Wymagania dotyczące długości hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-109">Password length requirements</span></span>
* <span data-ttu-id="0d084-110">Wymagania dotyczące złożoności hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-110">Password complexity requirements</span></span>
* <span data-ttu-id="0d084-111">Regularne i okresowe wygasanie haseł</span><span class="sxs-lookup"><span data-stu-id="0d084-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="0d084-112">Uzyskać informacji na temat resetowania w usłudze Azure Active Directory, zobacz temat hello [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="0d084-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="0d084-113">Zabezpieczenia hasła w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d084-113">Azure AD password protections</span></span>

<span data-ttu-id="0d084-114">Usługi Azure AD i branży sprawdzone używane w systemie konta Microsoft hello zbliża się tooensure zabezpieczenie hasła użytkownika i administratora, w tym:</span><span class="sxs-lookup"><span data-stu-id="0d084-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="0d084-115">Hasła dynamicznie zakazane</span><span class="sxs-lookup"><span data-stu-id="0d084-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="0d084-116">Inteligentna blokada haseł</span><span class="sxs-lookup"><span data-stu-id="0d084-116">Smart Password Lockout</span></span>

<span data-ttu-id="0d084-117">Uzyskać informacji na temat zarządzania hasłami oparte na bieżącej badań, zobacz oficjalny dokument hello [wskazówki dotyczące hasła](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="0d084-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="0d084-118">Hasła dynamicznie zakazane</span><span class="sxs-lookup"><span data-stu-id="0d084-118">Dynamically banned passwords</span></span>

<span data-ttu-id="0d084-119">Usługi Azure AD i Accounts Microsoft zabezpieczenia ochrony hasłem przez dynamicznie zakaz często używanych haseł.</span><span class="sxs-lookup"><span data-stu-id="0d084-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="0d084-120">zespół Azure identyfikator Identity Protection Hello regularnie analizuje listy zabronionych haseł, uniemożliwia wybranie często używanych haseł użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0d084-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="0d084-121">Ta usługa jest dostępna tooAzure AD i klienci usługi konta Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="0d084-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="0d084-122">Podczas tworzenia haseł, jest ważne dla administratorów tooencourage użytkowników toochoose hasło frazy, które obejmują unikatowej kombinacji wartości litery, cyfry, znaki lub słowa.</span><span class="sxs-lookup"><span data-stu-id="0d084-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="0d084-123">Takie podejście ułatwia haseł użytkowników toomake toobe prawie niemożliwe naruszone, ale ułatwia tooremember użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0d084-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="0d084-124">Naruszenia hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-124">Password breaches</span></span>

<span data-ttu-id="0d084-125">Microsoft zawsze działa jeden krok toostay wcześniejsze przez przestępców.</span><span class="sxs-lookup"><span data-stu-id="0d084-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="0d084-126">Zespół usługi Azure AD Identity Protection Hello stale analizuje haseł, które są często używane.</span><span class="sxs-lookup"><span data-stu-id="0d084-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="0d084-127">Przez przestępców również użyć podobne tooinform strategii ich ataki, takie jak tworzenie [siłowe tabeli](https://en.wikipedia.org/wiki/Rainbow_table) dla łamania skrótów haseł.</span><span class="sxs-lookup"><span data-stu-id="0d084-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="0d084-128">Firma Microsoft stale analizuje [naruszeń danych](https://www.privacyrights.org/data-breaches) toomaintain listy aktualizowany dynamicznie zabronione hasła, który zapewnia, że narażone hasła są niedozwolone, zanim staną się rzeczywistych zagrożenia tooAzure AD klientów.</span><span class="sxs-lookup"><span data-stu-id="0d084-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="0d084-129">Aby uzyskać więcej informacji o bieżącym dążenie zabezpieczeń, zobacz hello [raportów analizy zabezpieczeń firmy Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d084-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="0d084-130">Inteligentna blokada haseł</span><span class="sxs-lookup"><span data-stu-id="0d084-130">Smart Password Lockout</span></span>

<span data-ttu-id="0d084-131">Usługi Azure AD wykryje potencjalne toohack w trakcie karne ataków na hasło użytkownika, możemy zablokowanie hello konto użytkownika z inteligentne blokady hasła.</span><span class="sxs-lookup"><span data-stu-id="0d084-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="0d084-132">Zaprojektowano w usłudze Azure AD toodetermine hello ryzyka związanego z określonej sesji.</span><span class="sxs-lookup"><span data-stu-id="0d084-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="0d084-133">Następnie przy użyciu najnowszych danych zabezpieczeń hello stosujemy blokady semantyki toostop przez zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="0d084-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="0d084-134">Jeśli użytkownik jest zablokowany z usługi Azure AD, ich ekranu wygląda podobnie toohello, co który następuje:</span><span class="sxs-lookup"><span data-stu-id="0d084-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Blokada w usłudze Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="0d084-136">Dla innego konta Microsoft ich ekranu wygląda podobnie toohello, co który następuje:</span><span class="sxs-lookup"><span data-stu-id="0d084-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Blokada konta Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="0d084-138">Uzyskać informacji na temat resetowania w usłudze Azure Active Directory, zobacz temat hello [usługi Azure AD samodzielnego resetowania haseł dla specjalistów IT hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="0d084-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="0d084-139">Jeśli jesteś administratorem usługi Azure AD, możesz toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid o użytkownikom tworzenie haseł tradycyjnych całkowicie.</span><span class="sxs-lookup"><span data-stu-id="0d084-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="0d084-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d084-140">Next steps</span></span>

* [<span data-ttu-id="0d084-141">Jak tooupdate własnego hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="0d084-142">Witaj podstawowe informacje na temat zarządzania tożsamość platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d084-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="0d084-143">Aktywność resetowania raportów dotyczących hasła</span><span class="sxs-lookup"><span data-stu-id="0d084-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


