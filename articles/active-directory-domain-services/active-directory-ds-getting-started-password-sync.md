---
title: "Azure Active Directory Domain Services: Włączanie synchronizacji haseł | Microsoft Docs"
description: "Wprowadzenie do usługi Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="279d5-103">Włącz tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="279d5-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="279d5-104">W poprzednich zadaniach włączono usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="279d5-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="279d5-105">następne zadanie Hello jest tooenable synchronizacji skrótów poświadczeń wymaganych dla NT LAN Manager (NTLM) i protokołu Kerberos tooAzure uwierzytelniania usług domenowych w usłudze AD.</span><span class="sxs-lookup"><span data-stu-id="279d5-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="279d5-106">Po skonfigurowaniu synchronizacji poświadczeń użytkowników można zalogować toohello domeny zarządzanej przy użyciu poświadczeń firmowych.</span><span class="sxs-lookup"><span data-stu-id="279d5-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="279d5-107">etapy Hello są różne dla kont użytkowników programu vs konta użytkownika tylko do chmury, które są synchronizowane z katalogiem lokalnym za pomocą programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="279d5-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="279d5-108">Jeśli dzierżawy usługi Azure AD ma kombinację chmury tylko użytkownicy i użytkowników z lokalnej usługi AD, należy tooperform obu czynności.</span><span class="sxs-lookup"><span data-stu-id="279d5-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="279d5-109">**Konta użytkowników tylko w chmurze**: [synchronizacji haseł dla kont użytkowników tylko w chmurze tooyour domeny zarządzanej](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="279d5-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="279d5-110">**Lokalne konta użytkowników**: [synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej domeny zarządzane AD tooyour](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="279d5-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="279d5-111">Zadanie 5: Włączanie domeny zarządzanej tooyour synchronizacji haseł dla kont użytkowników tylko w chmurze</span><span class="sxs-lookup"><span data-stu-id="279d5-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="279d5-112">tooauthenticate użytkowników na powitania zarządzanych domeny, usług domenowych Azure Active Directory wymaga poświadczeń skrótów w formacie, który jest odpowiedni dla uwierzytelniania NTLM i Kerberos.</span><span class="sxs-lookup"><span data-stu-id="279d5-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="279d5-113">Usługi Azure AD nie Generuj lub przechowywać skróty poświadczeń w formacie hello, które są wymagane do uwierzytelniania NTLM lub Kerberos, przed włączeniem usługi Azure Active Directory Domain Services dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="279d5-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="279d5-114">Ze względów bezpieczeństwa usługa Azure AD nie przechowuje również żadnych poświadczeń haseł w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="279d5-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="279d5-115">W związku z tym usługi Azure AD nie ma tooautomatically sposób generowania tych skrótów poświadczeń NTLM lub Kerberos na podstawie istniejących poświadczeń użytkowników.</span><span class="sxs-lookup"><span data-stu-id="279d5-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="279d5-116">Jeśli Twoja organizacja ma kont użytkowników tylko w chmurze, użytkowników, którzy potrzebują toouse Azure Active Directory Domain Services zmieniać swoje hasła.</span><span class="sxs-lookup"><span data-stu-id="279d5-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="279d5-117">Konto użytkownika tylko w chmurze jest konto, który został utworzony w katalogu usługi Azure AD przy użyciu hello portalu Azure lub poleceń cmdlet programu Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="279d5-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="279d5-118">Takie konta użytkownika nie są synchronizowane z poziomu katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="279d5-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="279d5-119">Ten proces zmiany haseł powoduje, że poświadczenie hello skrótów, które są wymagane przez usługi Azure Active Directory Domain Services dla toobe uwierzytelnianie Kerberos i NTLM, generowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="279d5-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="279d5-120">Możesz unieważnić hello haseł dla wszystkich użytkowników w hello dzierżawy, którzy muszą toouse Azure Active Directory Domain Services lub poinstruuj ich toochange haseł.</span><span class="sxs-lookup"><span data-stu-id="279d5-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="279d5-121">Włączanie generowania skrótów poświadczeń NTLM i Kerberos dla kont użytkowników tylko w chmurze</span><span class="sxs-lookup"><span data-stu-id="279d5-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="279d5-122">Poniżej przedstawiono instrukcje hello potrzebne tooprovide użytkowników, aby mogli oni zmieniać swoje hasła:</span><span class="sxs-lookup"><span data-stu-id="279d5-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="279d5-123">Przejdź toohello [Panel dostępu usługi Azure AD](http://myapps.microsoft.com) strony dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="279d5-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Uruchom panel dostępu usługi Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="279d5-125">W hello prawym górnym rogu, kliknij swoją nazwę i wybierz polecenie **profilu** hello menu.</span><span class="sxs-lookup"><span data-stu-id="279d5-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Wybieranie profilu](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="279d5-127">Na powitania **profilu** kliknij pozycję **Zmień hasło**.</span><span class="sxs-lookup"><span data-stu-id="279d5-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Kliknięcie pozycji „Zmień hasło”](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="279d5-129">Jeśli hello **Zmień hasło** opcja nie jest wyświetlana w oknie Panel dostępu hello, upewnij się, że Twoja organizacja ma skonfigurowaną [Zarządzanie hasłami w usłudze Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="279d5-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="279d5-130">Na powitania **zmiany hasła** wpisz istniejące (stare) hasło, wpisz nowe hasło, a następnie potwierdź je.</span><span class="sxs-lookup"><span data-stu-id="279d5-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Utwórz sieć wirtualną dla Usług domenowych Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="279d5-132">Kliknij przycisk **prześlij**.</span><span class="sxs-lookup"><span data-stu-id="279d5-132">Click **submit**.</span></span>

<span data-ttu-id="279d5-133">Kilka minut po zmianie hasła, hello nowe hasło jest nadające się do usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="279d5-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="279d5-134">Po kilku minutach (zazwyczaj około 20 minut,), możesz zalogować się toocomputers będące toohello przyłączone do domeny zarządzanej przy użyciu hello nowo zmienić hasło.</span><span class="sxs-lookup"><span data-stu-id="279d5-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="279d5-135">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="279d5-135">Related Content</span></span>
* [<span data-ttu-id="279d5-136">Jak tooupdate własnego hasła</span><span class="sxs-lookup"><span data-stu-id="279d5-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="279d5-137">Wprowadzenie do zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="279d5-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="279d5-138">Włączanie synchronizacji haseł dzierżawy tooAzure Active Directory Domain Services dla zsynchronizowanej usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="279d5-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="279d5-139">Administrowanie domeną zarządzaną usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="279d5-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="279d5-140">Dołącz do domeny systemu Windows maszyny wirtualnej tooan zarządzanych usług domenowych Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="279d5-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="279d5-141">Przyłącz do Red Hat Enterprise Linux maszyny wirtualnej tooan zarządzanych usług domenowych Azure Active Directory domeny</span><span class="sxs-lookup"><span data-stu-id="279d5-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
