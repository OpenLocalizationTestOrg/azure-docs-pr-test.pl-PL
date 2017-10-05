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
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="b0bf4-103">Włączanie synchronizacji haseł w usługach Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b0bf4-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="b0bf4-104">W poprzednich zadaniach włączono usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0bf4-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="b0bf4-105">Kolejnym krokiem jest włączenie synchronizacji skrótów poświadczeń wymaganych do uwierzytelniania NT LAN Manager (NTLM) i Kerberos w usługach Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="b0bf4-106">Po skonfigurowaniu synchronizacji poświadczeń użytkownik może zalogować się do domeny zarządzanej przy użyciu poświadczeń firmowych.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="b0bf4-107">Wykonywane czynności są różne dla kont użytkowników tylko w chmurze i kont użytkowników synchronizowanych z katalogu lokalnego przy użyciu programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="b0bf4-108">Jeśli dzierżawa usługi Azure AD ma kombinację użytkowników tylko w chmurze i użytkowników z lokalnej usługi AD, należy wykonać obie czynności.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="b0bf4-109">**Konta użytkowników tylko w chmurze**: [zsynchronizuj hasła dla kont użytkowników tylko w chmurze do domeny zarządzanej](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="b0bf4-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="b0bf4-110">**Lokalne konta użytkowników**: [zsynchronizuj hasła dla kont użytkowników synchronizowanych z lokalnej usługi AD do domeny zarządzanej](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="b0bf4-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="b0bf4-111">Zadanie 5. Włączanie synchronizacji haseł do domeny zarządzanej dla kont użytkowników tylko w chmurze</span><span class="sxs-lookup"><span data-stu-id="b0bf4-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="b0bf4-112">Usługi Azure Active Directory Domain Services wymagają skrótów poświadczeń w formacie odpowiednim do uwierzytelniania NTLM i Kerberos, aby uwierzytelnić użytkowników w domenie zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="b0bf4-113">Usługa Azure AD nie będzie generować ani przechowywać skrótów poświadczeń w formacie wymaganym podczas uwierzytelniania NTLM i Kerberos, jeśli nie zostaną włączone usługi Azure Active Directory Domain Services dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="b0bf4-114">Ze względów bezpieczeństwa usługa Azure AD nie przechowuje również żadnych poświadczeń haseł w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="b0bf4-115">W związku z tym usługa Azure AD nie ma możliwości automatycznego generowania skrótów poświadczeń protokołu NTLM ani Kerberos w oparciu o istniejące poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="b0bf4-116">Jeśli organizacja ma konta użytkowników tylko w chmurze, użytkownicy, którzy muszą korzystać z usług Azure Active Directory Domain Services, muszą zmienić swoje hasła.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="b0bf4-117">Konto użytkownika tylko w chmurze to konto, które zostało utworzone w katalogu usługi Azure AD przy użyciu witryny Azure Portal lub poleceń cmdlet programu Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="b0bf4-118">Takie konta użytkownika nie są synchronizowane z poziomu katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="b0bf4-119">Ten proces zmiany haseł powoduje generowanie w usłudze Azure AD skrótów poświadczeń wymaganych przez usługi Azure Active Directory Domain Services na potrzeby uwierzytelniania Kerberos i NTLM.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="b0bf4-120">Możesz unieważnić hasła wszystkich użytkowników w dzierżawie, którzy muszą korzystać z usług Azure Active Directory Domain Services, lub poinformować ich o konieczności zmiany haseł.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="b0bf4-121">Włączanie generowania skrótów poświadczeń NTLM i Kerberos dla kont użytkowników tylko w chmurze</span><span class="sxs-lookup"><span data-stu-id="b0bf4-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="b0bf4-122">Poniżej znajdują się instrukcje zmieniania haseł dla użytkowników:</span><span class="sxs-lookup"><span data-stu-id="b0bf4-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="b0bf4-123">Przejdź do strony [panelu dostępu do usługi Azure AD](http://myapps.microsoft.com) dla organizacji.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Uruchamianie panelu dostępu usługi Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="b0bf4-125">W prawym górnym rogu kliknij swoją nazwę i wybierz pozycję **Profil** z menu.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Wybieranie profilu](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="b0bf4-127">Na stronie **Profil** kliknij pozycję **Zmień hasło**.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Kliknięcie pozycji „Zmień hasło”](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="b0bf4-129">Jeśli opcja **Zmień hasło** nie jest wyświetlana w oknie panelu dostępu, upewnij się, że Twoja organizacja ma skonfigurowane [zarządzanie hasłami w usłudze Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b0bf4-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="b0bf4-130">Na stronie **Zmiana hasła** wpisz istniejące hasło (stare), a następnie wpisz nowe hasło i je zatwierdź.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Utwórz sieć wirtualną dla Usług domenowych Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="b0bf4-132">Kliknij przycisk **prześlij**.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-132">Click **submit**.</span></span>

<span data-ttu-id="b0bf4-133">Nowego hasła w usługach Azure Active Directory Domain Services można używać już kilka minut po jego zmianie.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b0bf4-134">Po kilku kolejnych minutach (zazwyczaj po około 20 minutach) przy użyciu nowego hasła będzie można się logować na komputerach dołączonych do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="b0bf4-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="b0bf4-135">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="b0bf4-135">Related Content</span></span>
* [<span data-ttu-id="b0bf4-136">Jak zaktualizować własne hasło</span><span class="sxs-lookup"><span data-stu-id="b0bf4-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="b0bf4-137">Wprowadzenie do zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0bf4-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="b0bf4-138">Włączanie synchronizacji haseł w usługach Azure Active Directory Domain Services dla zsynchronizowanej dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0bf4-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="b0bf4-139">Administrowanie domeną zarządzaną usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b0bf4-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="b0bf4-140">Dołączanie maszyny wirtualnej z systemem Windows do domeny zarządzanej usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b0bf4-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="b0bf4-141">Dołączanie maszyny wirtualnej z systemem Red Hat Enterprise Linux do domeny zarządzanej usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b0bf4-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
