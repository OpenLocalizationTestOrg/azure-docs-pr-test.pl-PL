---
title: "Zabezpieczanie zasobów w chmurze za pomocą usługi Azure MFA i usług AD FS | Microsoft Docs"
description: "Ta strona dotyczy usługi Azure Multi-Factor Authentication i zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA i usług AD FS w chmurze."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS
Jeśli Twoja organizacja jest sfederowana z użyciem usługi Azure Active Directory, możesz użyć usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services (AD FS) do zabezpieczenia zasobów używanych przez usługę Azure AD. Aby zabezpieczyć zasoby usługi Azure Active Directory za pomocą usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services, postępuj zgodnie z poniższymi procedurami.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS
Aby zabezpieczyć zasób w chmurze, skonfiguruj regułę oświadczeń, tak aby usługi Active Directory Federation Services emitowały oświadczenie multipleauthn, gdy użytkownik pomyślnie przeprowadzi weryfikację dwuetapową. To oświadczenie jest przekazywane do usługi Azure AD. Wykonaj tę procedurę w celu przejścia przez poszczególne kroki:


1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie wybierz pozycję **Relacje zaufania jednostek zależnych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Przekazywanie lub filtrowanie oświadczenia przychodzącego**, a następnie kliknij przycisk **Dalej**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nadaj regule nazwę. 
7. Wybierz wartość **Odwołania metod uwierzytelniania** jako typ oświadczenia przychodzącego.
8. Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.
    ![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Kliknij przycisk **Zakończ**. Zamknij konsolę zarządzania usługami AD FS.

## <a name="trusted-ips-for-federated-users"></a>Zaufane adresy IP dla użytkowników federacyjnych
Zaufane adresy IP umożliwiają administratorom pomijanie weryfikacji dwuetapowej w przypadku określonych adresów IP lub użytkowników federacyjnych, którzy wysyłają żądania z firmowej sieci intranet. Poniższe sekcje zawierają instrukcje dotyczące konfigurowania zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych i pomijania weryfikacji dwuetapowej w przypadku żądań pochodzących od użytkowników federacyjnych z sieci intranet. Osiąga się to przez skonfigurowanie usług AD FS pod kątem używania szablonu przekazywania lub szablonu filtrowania oświadczeń przychodzących za pomocą typu oświadczeń wewnętrznej sieci firmowej.

W tym przykładzie użyto usługi Office 365 w celu pokazania obsługi relacji zaufania jednostek zależnych.

### <a name="configure-the-ad-fs-claims-rules"></a>Konfigurowanie reguł oświadczeń usług AD FS
W pierwszej kolejności należy skonfigurować oświadczenia usług AD FS. Utwórz dwie reguły oświadczeń — jedną dla typu oświadczenia wewnętrznej sieci firmowej, a drugą na potrzeby umożliwienia stałego zalogowania użytkowników.

1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie wybierz pozycję **Relacje zaufania jednostek zależnych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę.**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Przekazywanie lub filtrowanie oświadczenia przychodzącego**, a następnie kliknij przycisk **Dalej**.
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. W polu Nazwa reguły oświadczenia wpisz nazwę reguły, np. WewnSiećFirm.
7. Dla pola Typ oświadczenia przychodzącego wybierz z listy rozwijanej pozycję **Wewnątrz sieci firmowej**.
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Kliknij przycisk **Finish** (Zakończ).
9. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.
10. W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Wysyłanie oświadczeń przy użyciu reguły niestandardowej**, a następnie kliknij przycisk **Dalej**.
11. W polu Nazwa reguły oświadczenia wprowadź tekst *Nie wylogowuj użytkowników*.
12. W polu Reguła niestandardowa wprowadź kod:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Kliknij przycisk **Zakończ**.
14. Kliknij przycisk **Zastosuj**.
15. Kliknij przycisk **OK**.
16. Zamknij przystawkę zarządzania usługami AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Konfigurowanie zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych
Po skonfigurowaniu oświadczeń można przystąpić do konfigurowania zaufanych adresów IP.

1. Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).
2. W obszarze po lewej stronie kliknij pozycję **Active Directory**.
3. W sekcji Katalog wybierz katalog, w którym chcesz skonfigurować zaufane adresy IP.
4. W wybranym katalogu kliknij pozycję **Konfiguruj**.
5. W sekcji uwierzytelniania wieloskładnikowego kliknij pozycję **Zarządzaj ustawieniami usługi**.
6. Na stronie Ustawienia usługi w obszarze zaufanych adresów IP wybierz pozycję **Pomiń uwierzytelnianie wieloskładnikowe w przypadku żądań od użytkowników federacyjnych w moim intranecie**.  

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Kliknij pozycję **Zapisz**.
8. Po zastosowaniu aktualizacji kliknij pozycję **Zamknij**.

Gotowe. Od tej pory federacyjni użytkownicy usługi Office 365 muszą używać usługi MFA, tylko jeśli ich oświadczenia pochodzą spoza firmowego intranetu.
