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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0c031-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c031-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0c031-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="0c031-104">Before you begin</span></span>
<span data-ttu-id="0c031-105">Upewnij się, przeprowadzisz [zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="0c031-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="0c031-106">Zadanie 2 — wyeksportować hello bezpiecznego tooa certyfikatu LDAP. Plik PFX</span><span class="sxs-lookup"><span data-stu-id="0c031-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="0c031-107">Przed rozpoczęciem tego zadania upewnij się, hello bezpiecznego LDAP certyfikat został uzyskany z publicznego urzędu certyfikacji, lub został utworzony certyfikat z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="0c031-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="0c031-108">Wykonaj następujące kroki hello, tooexport hello LDAPS certyfikatu tooa. Plik PFX.</span><span class="sxs-lookup"><span data-stu-id="0c031-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="0c031-109">Naciśnij klawisz hello **Start** przycisk i typ **R**. W hello **Uruchom** okno dialogowe, typ **mmc** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c031-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Uruchom konsolę MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="0c031-111">Na powitania **Kontrola konta użytkownika** monit, kliknij przycisk **tak** toolaunch MMC (Microsoft Management Console) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0c031-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="0c031-112">Z hello **pliku** menu, kliknij przycisk **Dodaj/Usuń przystawkę...** .</span><span class="sxs-lookup"><span data-stu-id="0c031-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Dodawanie przystawki tooMMC konsoli](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="0c031-114">W hello **Dodawanie lub usuwanie przystawek** okno dialogowe, wybierz opcję hello **certyfikaty** przystawki i kliknij przycisk hello **Dodaj >** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c031-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Dodaj konsoli tooMMC przystawki Certyfikaty](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="0c031-116">W hello **certyfikatów przystawki** kreatora wybierz **konto komputera** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0c031-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Dodaj przystawkę Certyfikaty dla konta komputera](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="0c031-118">Na powitania **Wybieranie komputera** wybierz **komputer lokalny: (komputer hello uruchomiona ta konsola jest)** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="0c031-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Dodaj przystawkę Certyfikaty — komputer select](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="0c031-120">W hello **Dodawanie lub usuwanie przystawek** okna dialogowego, kliknij przycisk **OK** tooadd hello certyfikatów przystawki tooMMC.</span><span class="sxs-lookup"><span data-stu-id="0c031-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Dodaj certyfikaty przystawki tooMMC — Zakończono](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="0c031-122">W oknie konsoli MMC powitania kliknij tooexpand **katalog główny konsoli**.</span><span class="sxs-lookup"><span data-stu-id="0c031-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="0c031-123">Powinny pojawić się załadować hello przystawki Certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="0c031-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="0c031-124">Kliknij przycisk **certyfikaty (komputer lokalny)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="0c031-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="0c031-125">Kliknij przycisk tooexpand hello **osobistych** węzeł, a następnie hello **certyfikaty** węzła.</span><span class="sxs-lookup"><span data-stu-id="0c031-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Otwórz osobistym magazynie certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="0c031-127">Powinny pojawić się hello samopodpisany certyfikat, który utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="0c031-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="0c031-128">Można sprawdzić właściwości hello hello certyfikatu tooensure hello odcisk palca dopasowań, którzy zgłosili w systemie windows PowerShell hello podczas tworzenia certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="0c031-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="0c031-129">Wybierz hello certyfikatu z podpisem własnym i **kliknij prawym przyciskiem myszy**.</span><span class="sxs-lookup"><span data-stu-id="0c031-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="0c031-130">Witaj menu kliknij prawym przyciskiem myszy i wybierz polecenie **wszystkie zadania** i wybierz **Eksportuj...** .</span><span class="sxs-lookup"><span data-stu-id="0c031-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Eksportowanie certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="0c031-132">W hello **Kreatora eksportu certyfikatów**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0c031-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Kreator eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="0c031-134">Na powitania **eksportowanie klucza prywatnego** wybierz pozycję **tak, Eksportuj klucz prywatny hello**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0c031-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Eksportowanie klucza prywatnego certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="0c031-136">Należy wyeksportować klucz prywatny hello wraz z hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0c031-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="0c031-137">Jeśli podasz PFX, który nie zawiera hello klucza prywatnego dla certyfikatu hello Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="0c031-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="0c031-138">Na powitania **Format pliku eksportu** wybierz pozycję **wymiana informacji osobistych — PKCS #12 (. PFX)** jak format pliku hello hello wyeksportowanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0c031-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Format pliku eksportu certyfikatu](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="0c031-140">Tylko "hello". Format pliku PFX jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="0c031-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="0c031-141">Nie Eksportuj hello toohello certyfikatu. Format pliku CER.</span><span class="sxs-lookup"><span data-stu-id="0c031-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="0c031-142">Na powitania **zabezpieczeń** strona, wybierz hello **hasło** opcję i wprowadź hello tooprotect hasła. Plik PFX.</span><span class="sxs-lookup"><span data-stu-id="0c031-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="0c031-143">Zapamiętaj to hasło, ponieważ jest ono potrzebne w hello następnego zadania.</span><span class="sxs-lookup"><span data-stu-id="0c031-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="0c031-144">Kliknij przycisk **dalej** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="0c031-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="0c031-145">Hasło do eksportowania certyfikatów</span><span class="sxs-lookup"><span data-stu-id="0c031-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="0c031-146">Zanotuj to hasło.</span><span class="sxs-lookup"><span data-stu-id="0c031-146">Make a note of this password.</span></span> <span data-ttu-id="0c031-147">Należy podczas włączania bezpiecznego protokołu LDAP dla tej domeny zarządzanej w [zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="0c031-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="0c031-148">Na powitania **tooExport pliku** Określ hello nazwę pliku i lokalizację, gdzie chcesz tooexport hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0c031-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Ścieżka do eksportowania certyfikatów](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="0c031-150">Na powitania po stronie, kliknij przycisk **Zakończ** pliku PFX tooa tooexport hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0c031-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="0c031-151">Po wyeksportowaniu certyfikatu hello powinno zostać wyświetlone okno dialogowe potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="0c031-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Wyeksportuj certyfikat gotowe](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="0c031-153">Następny krok</span><span class="sxs-lookup"><span data-stu-id="0c031-153">Next step</span></span>
[<span data-ttu-id="0c031-154">Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello</span><span class="sxs-lookup"><span data-stu-id="0c031-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
