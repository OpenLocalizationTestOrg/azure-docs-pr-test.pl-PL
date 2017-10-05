---
title: "Skonfigurować bezpiecznego protokołu LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="19549-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="19549-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="19549-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="19549-104">Before you begin</span></span>
<span data-ttu-id="19549-105">Upewnij się, przeprowadzisz [zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="19549-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="19549-106">Zadanie 2 — wyeksportowany certyfikat bezpiecznego LDAP. Plik PFX</span><span class="sxs-lookup"><span data-stu-id="19549-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="19549-107">Przed rozpoczęciem tego zadania upewnij się, czy bezpiecznego certyfikat LDAP został uzyskany z publicznego urzędu certyfikacji lub utworzono certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="19549-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="19549-108">Wykonaj poniższe kroki, aby wyeksportować certyfikat LDAPS do. Plik PFX.</span><span class="sxs-lookup"><span data-stu-id="19549-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="19549-109">Naciśnij klawisz **Start** przycisk i typ **R**. W **Uruchom** okno dialogowe, typ **mmc** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19549-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Uruchamianie konsoli MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="19549-111">Na **Kontrola konta użytkownika** monit, kliknij przycisk **tak** na uruchamianie konsoli MMC (Microsoft Management Console) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="19549-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="19549-112">Z **pliku** menu, kliknij przycisk **Dodaj/Usuń przystawkę...** .</span><span class="sxs-lookup"><span data-stu-id="19549-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Dodawanie przystawki do konsoli MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="19549-114">W **Dodawanie lub usuwanie przystawek** okno dialogowe, wybierz opcję **certyfikaty** przystawki, a następnie kliknij przycisk **Dodaj >** przycisku.</span><span class="sxs-lookup"><span data-stu-id="19549-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Dodawanie przystawki Certyfikaty do konsoli MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="19549-116">W **certyfikatów przystawki** kreatora wybierz **konto komputera** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="19549-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Dodaj przystawkę Certyfikaty dla konta komputera](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="19549-118">Na **Wybieranie komputera** wybierz **komputer lokalny: (komputer ten jest uruchomiona konsola)** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="19549-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Dodaj przystawkę Certyfikaty — komputer select](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="19549-120">W **Dodawanie lub usuwanie przystawek** okna dialogowego, kliknij przycisk **OK** Aby dodać przystawkę Certyfikaty do programu MMC.</span><span class="sxs-lookup"><span data-stu-id="19549-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Dodawanie przystawki Certyfikaty do programu MMC — Zakończono](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="19549-122">W oknie konsoli MMC kliknij, aby rozwinąć **katalog główny konsoli**.</span><span class="sxs-lookup"><span data-stu-id="19549-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="19549-123">Powinna zostać wyświetlona przystawki Certyfikaty załadowane.</span><span class="sxs-lookup"><span data-stu-id="19549-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="19549-124">Kliknij przycisk **certyfikaty (komputer lokalny)** aby rozwinąć.</span><span class="sxs-lookup"><span data-stu-id="19549-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="19549-125">Kliknij, aby rozwinąć **osobistych** węzeł, a następnie **certyfikaty** węzła.</span><span class="sxs-lookup"><span data-stu-id="19549-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Otwórz osobistym magazynie certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="19549-127">Certyfikat z podpisem własnym utworzonego powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="19549-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="19549-128">Można zbadać właściwości certyfikatu, aby upewnić się, że odcisk palca jest zgodna z wersją zgłoszone w systemie windows PowerShell, podczas tworzenia certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="19549-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="19549-129">Wybierz certyfikat z podpisem własnym i **kliknij prawym przyciskiem myszy**.</span><span class="sxs-lookup"><span data-stu-id="19549-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="19549-130">Wybierz z menu kliknij prawym przyciskiem myszy **wszystkie zadania** i wybierz **Eksportuj...** .</span><span class="sxs-lookup"><span data-stu-id="19549-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Eksportowanie certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="19549-132">W **Kreatora eksportu certyfikatów**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="19549-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Kreator eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="19549-134">Na **eksportowanie klucza prywatnego** wybierz pozycję **tak, Eksportuj klucz prywatny**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="19549-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Eksportowanie klucza prywatnego certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="19549-136">Należy wyeksportować klucz prywatny wraz z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="19549-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="19549-137">Jeśli podasz PFX, który nie zawiera klucza prywatnego dla certyfikatu, włączanie bezpiecznego protokołu LDAP do domeny zarządzanej nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="19549-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="19549-138">Na **Format pliku eksportu** wybierz pozycję **wymiana informacji osobistych — PKCS #12 (. PFX)** jako format pliku dla wyeksportowanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="19549-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Format pliku eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="19549-140">Tylko. Format pliku PFX jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="19549-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="19549-141">Nie Eksportuj certyfikat. Format pliku CER.</span><span class="sxs-lookup"><span data-stu-id="19549-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="19549-142">Na **zabezpieczeń** wybierz pozycję **hasło** opcję i wpisz hasło, aby chronić. Plik PFX.</span><span class="sxs-lookup"><span data-stu-id="19549-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="19549-143">Zapamiętaj to hasło, ponieważ jest ono potrzebne w następnego zadania.</span><span class="sxs-lookup"><span data-stu-id="19549-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="19549-144">Kliknij przycisk **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="19549-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="19549-145">Hasło do eksportowania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="19549-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="19549-146">Zanotuj to hasło.</span><span class="sxs-lookup"><span data-stu-id="19549-146">Make a note of this password.</span></span> <span data-ttu-id="19549-147">Należy podczas włączania bezpiecznego protokołu LDAP dla tej domeny zarządzanej w [zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="19549-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="19549-148">Na **Eksport pliku** Określ nazwę pliku i lokalizację, w której chcesz wyeksportować certyfikat.</span><span class="sxs-lookup"><span data-stu-id="19549-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Ścieżka do eksportowania certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="19549-150">Na następnej stronie kliknij **Zakończ** można wyeksportować certyfikat do pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="19549-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="19549-151">Jeśli certyfikat został wyeksportowany powinno zostać wyświetlone okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="19549-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Wyeksportuj certyfikat gotowe](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="19549-153">Następny krok</span><span class="sxs-lookup"><span data-stu-id="19549-153">Next step</span></span>
[<span data-ttu-id="19549-154">Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej</span><span class="sxs-lookup"><span data-stu-id="19549-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
