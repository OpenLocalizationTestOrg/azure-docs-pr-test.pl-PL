---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD

## <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, przeprowadzisz [zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Zadanie 2 — wyeksportować hello bezpiecznego tooa certyfikatu LDAP. Plik PFX
Przed rozpoczęciem tego zadania upewnij się, hello bezpiecznego LDAP certyfikat został uzyskany z publicznego urzędu certyfikacji, lub został utworzony certyfikat z podpisem własnym.

Wykonaj następujące kroki hello, tooexport hello LDAPS certyfikatu tooa. Plik PFX.

1. Naciśnij klawisz hello **Start** przycisk i typ **R**. W hello **Uruchom** okno dialogowe, typ **mmc** i kliknij przycisk **OK**.

    ![Uruchom konsolę MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Na powitania **Kontrola konta użytkownika** monit, kliknij przycisk **tak** toolaunch MMC (Microsoft Management Console) jako administrator.
3. Z hello **pliku** menu, kliknij przycisk **Dodaj/Usuń przystawkę...** .

    ![Dodawanie przystawki tooMMC konsoli](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. W hello **Dodawanie lub usuwanie przystawek** okno dialogowe, wybierz opcję hello **certyfikaty** przystawki i kliknij przycisk hello **Dodaj >** przycisku.

    ![Dodaj konsoli tooMMC przystawki Certyfikaty](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. W hello **certyfikatów przystawki** kreatora wybierz **konto komputera** i kliknij przycisk **dalej**.

    ![Dodaj przystawkę Certyfikaty dla konta komputera](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Na powitania **Wybieranie komputera** wybierz **komputer lokalny: (komputer hello uruchomiona ta konsola jest)** i kliknij przycisk **Zakończ**.

    ![Dodaj przystawkę Certyfikaty — komputer select](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. W hello **Dodawanie lub usuwanie przystawek** okna dialogowego, kliknij przycisk **OK** tooadd hello certyfikatów przystawki tooMMC.

    ![Dodaj certyfikaty przystawki tooMMC — Zakończono](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. W oknie konsoli MMC powitania kliknij tooexpand **katalog główny konsoli**. Powinny pojawić się załadować hello przystawki Certyfikaty. Kliknij przycisk **certyfikaty (komputer lokalny)** tooexpand. Kliknij przycisk tooexpand hello **osobistych** węzeł, a następnie hello **certyfikaty** węzła.

    ![Otwórz osobistym magazynie certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Powinny pojawić się hello samopodpisany certyfikat, który utworzyliśmy. Można sprawdzić właściwości hello hello certyfikatu tooensure hello odcisk palca dopasowań, którzy zgłosili w systemie windows PowerShell hello podczas tworzenia certyfikatu hello.
10. Wybierz hello certyfikatu z podpisem własnym i **kliknij prawym przyciskiem myszy**. Witaj menu kliknij prawym przyciskiem myszy i wybierz polecenie **wszystkie zadania** i wybierz **Eksportuj...** .

    ![Eksportowanie certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. W hello **Kreatora eksportu certyfikatów**, kliknij przycisk **dalej**.

    ![Kreator eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Na powitania **eksportowanie klucza prywatnego** wybierz pozycję **tak, Eksportuj klucz prywatny hello**i kliknij przycisk **dalej**.

    ![Eksportowanie klucza prywatnego certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > Należy wyeksportować klucz prywatny hello wraz z hello certyfikatu. Jeśli podasz PFX, który nie zawiera hello klucza prywatnego dla certyfikatu hello Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej nie powiedzie się.
    >
    >
13. Na powitania **Format pliku eksportu** wybierz pozycję **wymiana informacji osobistych — PKCS #12 (. PFX)** jak format pliku hello hello wyeksportowanego certyfikatu.

    ![Format pliku eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Tylko "hello". Format pliku PFX jest obsługiwany. Nie Eksportuj hello toohello certyfikatu. Format pliku CER.
    >
    >
14. Na powitania **zabezpieczeń** strona, wybierz hello **hasło** opcję i wprowadź hello tooprotect hasła. Plik PFX. Zapamiętaj to hasło, ponieważ jest ono potrzebne w hello następnego zadania. Kliknij przycisk **dalej** tooproceed.

    ![Hasło do eksportowania certyfikatów ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Zanotuj to hasło. Należy podczas włączania bezpiecznego protokołu LDAP dla tej domeny zarządzanej w [zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Na powitania **tooExport pliku** Określ hello nazwę pliku i lokalizację, gdzie chcesz tooexport hello certyfikatu.

    ![Ścieżka do eksportowania certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Na powitania po stronie, kliknij przycisk **Zakończ** pliku PFX tooa tooexport hello certyfikatu. Po wyeksportowaniu certyfikatu hello powinno zostać wyświetlone okno dialogowe potwierdzenia.

    ![Wyeksportuj certyfikat gotowe](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Następny krok
[Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
