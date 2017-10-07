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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Włącz tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory
W poprzednich zadaniach włączono usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure Active Directory (Azure AD). następne zadanie Hello jest tooenable synchronizacji skrótów poświadczeń wymaganych dla NT LAN Manager (NTLM) i protokołu Kerberos tooAzure uwierzytelniania usług domenowych w usłudze AD. Po skonfigurowaniu synchronizacji poświadczeń użytkowników można zalogować toohello domeny zarządzanej przy użyciu poświadczeń firmowych.

etapy Hello są różne dla kont użytkowników programu vs konta użytkownika tylko do chmury, które są synchronizowane z katalogiem lokalnym za pomocą programu Azure AD Connect.  Jeśli dzierżawy usługi Azure AD ma kombinację chmury tylko użytkownicy i użytkowników z lokalnej usługi AD, należy tooperform obu czynności.

<br>

> [!div class="op_single_selector"]
> * **Konta użytkowników tylko w chmurze**: [synchronizacji haseł dla kont użytkowników tylko w chmurze tooyour domeny zarządzanej](active-directory-ds-getting-started-password-sync.md)
> * **Lokalne konta użytkowników**: [synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej domeny zarządzane AD tooyour](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Zadanie 5: Włączanie domeny zarządzanej tooyour synchronizacji haseł dla kont użytkowników tylko w chmurze
tooauthenticate użytkowników na powitania zarządzanych domeny, usług domenowych Azure Active Directory wymaga poświadczeń skrótów w formacie, który jest odpowiedni dla uwierzytelniania NTLM i Kerberos. Usługi Azure AD nie Generuj lub przechowywać skróty poświadczeń w formacie hello, które są wymagane do uwierzytelniania NTLM lub Kerberos, przed włączeniem usługi Azure Active Directory Domain Services dla dzierżawy. Ze względów bezpieczeństwa usługa Azure AD nie przechowuje również żadnych poświadczeń haseł w postaci zwykłego tekstu. W związku z tym usługi Azure AD nie ma tooautomatically sposób generowania tych skrótów poświadczeń NTLM lub Kerberos na podstawie istniejących poświadczeń użytkowników.

> [!NOTE]
> Jeśli Twoja organizacja ma kont użytkowników tylko w chmurze, użytkowników, którzy potrzebują toouse Azure Active Directory Domain Services zmieniać swoje hasła. Konto użytkownika tylko w chmurze jest konto, który został utworzony w katalogu usługi Azure AD przy użyciu hello portalu Azure lub poleceń cmdlet programu Azure AD PowerShell. Takie konta użytkownika nie są synchronizowane z poziomu katalogu lokalnego.
>
>

Ten proces zmiany haseł powoduje, że poświadczenie hello skrótów, które są wymagane przez usługi Azure Active Directory Domain Services dla toobe uwierzytelnianie Kerberos i NTLM, generowane w usłudze Azure AD. Możesz unieważnić hello haseł dla wszystkich użytkowników w hello dzierżawy, którzy muszą toouse Azure Active Directory Domain Services lub poinstruuj ich toochange haseł.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Włączanie generowania skrótów poświadczeń NTLM i Kerberos dla kont użytkowników tylko w chmurze
Poniżej przedstawiono instrukcje hello potrzebne tooprovide użytkowników, aby mogli oni zmieniać swoje hasła:

1. Przejdź toohello [Panel dostępu usługi Azure AD](http://myapps.microsoft.com) strony dla Twojej organizacji.

    ![Uruchom panel dostępu usługi Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. W hello prawym górnym rogu, kliknij swoją nazwę i wybierz polecenie **profilu** hello menu.

    ![Wybieranie profilu](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Na powitania **profilu** kliknij pozycję **Zmień hasło**.

    ![Kliknięcie pozycji „Zmień hasło”](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Jeśli hello **Zmień hasło** opcja nie jest wyświetlana w oknie Panel dostępu hello, upewnij się, że Twoja organizacja ma skonfigurowaną [Zarządzanie hasłami w usłudze Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. Na powitania **zmiany hasła** wpisz istniejące (stare) hasło, wpisz nowe hasło, a następnie potwierdź je.

    ![Utwórz sieć wirtualną dla Usług domenowych Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Kliknij przycisk **prześlij**.

Kilka minut po zmianie hasła, hello nowe hasło jest nadające się do usług domenowych Azure Active Directory. Po kilku minutach (zazwyczaj około 20 minut,), możesz zalogować się toocomputers będące toohello przyłączone do domeny zarządzanej przy użyciu hello nowo zmienić hasło.

## <a name="related-content"></a>Powiązana zawartość
* [Jak tooupdate własnego hasła](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Wprowadzenie do zarządzania hasłami w usłudze Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Włączanie synchronizacji haseł dzierżawy tooAzure Active Directory Domain Services dla zsynchronizowanej usługi Azure AD](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Administrowanie domeną zarządzaną usług Azure Active Directory Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Dołącz do domeny systemu Windows maszyny wirtualnej tooan zarządzanych usług domenowych Azure Active Directory](active-directory-ds-admin-guide-join-windows-vm.md)
* [Przyłącz do Red Hat Enterprise Linux maszyny wirtualnej tooan zarządzanych usług domenowych Azure Active Directory domeny](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
