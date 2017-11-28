---
title: "Rozszerzenie panelu dostępu platformy Azure dla programu Internet Explorer przy użyciu obiektu zasad grupy aaaDeploy | Dokumentacja firmy Microsoft"
description: Jak toouse grupy zasad toodeploy hello programu Internet Explorer dodatek hello Moje aplikacje portalu.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="59a95-103">Jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy</span><span class="sxs-lookup"><span data-stu-id="59a95-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="59a95-104">Ten samouczek pokazuje, jak tooremotely zasad grupy toouse zainstalować hello rozszerzenia Panel dostępu dla programu Internet Explorer na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59a95-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="59a95-105">To rozszerzenie jest wymagane dla programu Internet Explorer, użytkownicy muszą toosign do aplikacji, które są skonfigurowane przy użyciu [opartego na hasłach rejestracji jednokrotnej](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="59a95-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="59a95-106">Zaleca się, że administratorzy automatyzacji wdrażania hello tego rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="59a95-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="59a95-107">W przeciwnym razie użytkownicy mają toodownload i sami zainstalują program hello rozszerzenia, który jest błąd toouser podatnych na błędy i musi mieć uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="59a95-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="59a95-108">Ten samouczek obejmuje jedną metodę automatyzację wdrożenia oprogramowania za pomocą zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="59a95-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="59a95-109">Dowiedz się więcej na temat zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="59a95-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="59a95-110">Witaj rozszerzenia Panel dostępu jest również dostępny do [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) i [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), które wymagają tooinstall uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="59a95-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59a95-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59a95-111">Prerequisites</span></span>
* <span data-ttu-id="59a95-112">Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59a95-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="59a95-113">Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO).</span><span class="sxs-lookup"><span data-stu-id="59a95-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="59a95-114">Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="59a95-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="59a95-115">Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="59a95-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="59a95-116">Krok 1: Tworzenie hello punktu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="59a95-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="59a95-117">Najpierw należy umieścić pakiet Instalatora hello w lokalizacji sieciowej dostępnej dla maszyny hello który ma rozszerzenie hello instalacji tooremotely na.</span><span class="sxs-lookup"><span data-stu-id="59a95-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="59a95-118">toodo, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59a95-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="59a95-119">Zaloguj się jako administrator na serwerze toohello</span><span class="sxs-lookup"><span data-stu-id="59a95-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="59a95-120">W hello **Menedżera serwera** okna, przejdź zbyt**pliki i usługi magazynu**.</span><span class="sxs-lookup"><span data-stu-id="59a95-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![Otwieranie plików i usługi magazynu](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="59a95-122">Przejdź toohello **udziałów** kartę. Następnie kliknij przycisk **zadania** > **nowy udział...**</span><span class="sxs-lookup"><span data-stu-id="59a95-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Otwieranie plików i usługi magazynu](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="59a95-124">Zakończenie hello **Kreator nowego udziału** oraz zestaw uprawnień tooensure, że jest dostępny z komputerów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59a95-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="59a95-125">Dowiedz się więcej na temat udziałów.</span><span class="sxs-lookup"><span data-stu-id="59a95-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="59a95-126">Pobierz powitania po pakiet Instalatora systemu Microsoft Windows (plik .msi): [Extension.msi panelu dostępu](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="59a95-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="59a95-127">Kopiuj hello Instalatora pakietu tooa żądana lokalizacji w udziale hello.</span><span class="sxs-lookup"><span data-stu-id="59a95-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Skopiuj udziału toohello plików .msi hello.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="59a95-129">Sprawdź, czy z komputerów klienckich pakiet Instalatora hello stanie tooaccess z hello udziału.</span><span class="sxs-lookup"><span data-stu-id="59a95-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="59a95-130">Krok 2: Tworzenie hello obiektu zasad grupy</span><span class="sxs-lookup"><span data-stu-id="59a95-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="59a95-131">Zaloguj się na serwerze toohello, który jest hostem instalacji usług domenowych w usłudze Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="59a95-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="59a95-132">W hello Menedżera serwera, przejdź do pozycji zbyt**narzędzia** > **Zarządzanie zasadami grupy**.</span><span class="sxs-lookup"><span data-stu-id="59a95-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![Przejdź tooTools > zarządzania zasadami grupy](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="59a95-134">W okienku po lewej stronie powitania hello **Zarządzanie zasadami grupy** okna, wyświetlić hierarchii jednostki organizacyjnej (OU) i określić, w których zakresie chcesz zasad grupy hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="59a95-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="59a95-135">Na przykład może się okazać toopick małych tooa toodeploy jednostki Organizacyjnej w przypadku kilku użytkowników do testowania lub mogą wybierać najwyższego poziomu jednostki Organizacyjnej toodeploy tooyour całej organizacji.</span><span class="sxs-lookup"><span data-stu-id="59a95-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59a95-136">Czy toocreate, takich jak lub edytować jednostkach organizacyjnych (OU), Przełącz wstecz toohello Menedżera serwera i przejść za**narzędzia** > **użytkownicy usługi Active Directory i komputery**.</span><span class="sxs-lookup"><span data-stu-id="59a95-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="59a95-137">Po wybraniu jednostki Organizacyjnej, kliknij go prawym przyciskiem myszy i wybierz **Utwórz obiekt GPO w tej domenie i umieść tu łącze...**</span><span class="sxs-lookup"><span data-stu-id="59a95-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Utwórz nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="59a95-139">W hello **nowy obiekt zasad grupy** monit, wpisz nazwę dla hello nowego obiektu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="59a95-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Nazwa hello nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="59a95-141">Powitania kliknij prawym przyciskiem myszy obiekt zasad grupy, który został utworzony i wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="59a95-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Edytuj hello nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="59a95-143">Krok 3: Przypisz hello pakietu instalacyjnego</span><span class="sxs-lookup"><span data-stu-id="59a95-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="59a95-144">Określić, czy chcesz na podstawie rozszerzenia hello toodeploy **Konfiguracja komputera** lub **Konfiguracja użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="59a95-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="59a95-145">Korzystając z [Konfiguracja komputera](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), rozszerzenia hello jest zainstalowany na komputerze hello niezależnie od tego, które użytkownicy logują tooit.</span><span class="sxs-lookup"><span data-stu-id="59a95-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="59a95-146">Z [Konfiguracja użytkownika](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), użytkownicy mają rozszerzenia hello zainstalowane dla nich niezależnie od tego, które komputery są zalogowani.</span><span class="sxs-lookup"><span data-stu-id="59a95-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="59a95-147">W okienku po lewej stronie powitania hello **Edytor zarządzania zasadami grupy** okna, przejdź tooeither o następującej ścieżki folderu, w zależności od tego, jakiego typu konfiguracji została wybrana opcja hello:</span><span class="sxs-lookup"><span data-stu-id="59a95-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="59a95-148">Kliknij prawym przyciskiem myszy **instalacji oprogramowania**, a następnie wybierz pozycję **nowy** > **pakietu...**</span><span class="sxs-lookup"><span data-stu-id="59a95-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Tworzenie nowego pakietu instalacyjnego oprogramowania](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="59a95-150">Przejdź toohello folderu udostępnionego, który zawiera pakiet Instalatora hello z [krok 1: Utwórz punkt dystrybucji hello](#step-1-create-the-distribution-point), wybierz plik msi hello i kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="59a95-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="59a95-151">Udział hello znajduje się na tym samym serwerze, sprawdź, za pośrednictwem hello sieci ścieżkę, a nie ścieżkę do pliku lokalnego hello uzyskujesz hello msi.</span><span class="sxs-lookup"><span data-stu-id="59a95-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Wybierz pakiet instalacyjny hello z hello folderu udostępnionego.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="59a95-153">W hello **wdrażanie oprogramowania** monitu, wybierz pozycję **przypisane** dla metody wdrażania.</span><span class="sxs-lookup"><span data-stu-id="59a95-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="59a95-154">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="59a95-154">Then click **OK**.</span></span>
   
    ![Wybierz przypisane, a następnie kliknij przycisk OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="59a95-156">rozszerzenie Hello jest teraz wdrożonej toohello jednostek organizacyjnych, wybrany.</span><span class="sxs-lookup"><span data-stu-id="59a95-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="59a95-157">Dowiedz się, jak Instalacja oprogramowania zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="59a95-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="59a95-158">Krok 4: Włącz automatyczne hello rozszerzenie programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="59a95-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="59a95-159">Ponadto Instalator hello toorunning, każde rozszerzenie programu Internet Explorer musi być jawnie włączone zanim będzie można go używać.</span><span class="sxs-lookup"><span data-stu-id="59a95-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="59a95-160">Wykonaj kroki hello poniżej tooenable hello rozszerzenia Panel dostępu za pomocą zasad grupy:</span><span class="sxs-lookup"><span data-stu-id="59a95-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="59a95-161">W hello **Edytor zarządzania zasadami grupy** Przejdź tooeither z hello następujące ścieżki, w zależności od tego, jakiego typu konfiguracji wybranego w oknie [krok 3: hello Przypisz pakietu instalacyjnego](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="59a95-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="59a95-162">Kliknij prawym przyciskiem myszy **lista dodatków**i wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="59a95-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="59a95-163">![Edytuj listę dodatek.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="59a95-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="59a95-164">W hello **lista dodatków** wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="59a95-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="59a95-165">Następnie w obszarze hello **opcje** kliknij **Pokaż...** .</span><span class="sxs-lookup"><span data-stu-id="59a95-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![Kliknij pozycję Włącz, a następnie kliknij przycisk Pokaż...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="59a95-167">W hello **Pokaż zawartość** okna, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59a95-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="59a95-168">Dla pierwszej kolumny hello (hello **Nazwa wartości** pola), kopiowanie i wklejanie powitania po identyfikator klasy:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="59a95-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="59a95-169">Dla drugiej kolumny hello (hello **wartość** pola), wpisz hello następujące wartości:`1`</span><span class="sxs-lookup"><span data-stu-id="59a95-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="59a95-170">Kliknij przycisk **OK** tooclose hello **Pokaż zawartość** okna.</span><span class="sxs-lookup"><span data-stu-id="59a95-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Wypełnij hello wartości określonych powyżej.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="59a95-172">Kliknij przycisk **OK** tooapply Twoje zmiany i zamknij hello **lista dodatków** okna.</span><span class="sxs-lookup"><span data-stu-id="59a95-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="59a95-173">Witaj rozszerzenia powinno ono włączone dla hello maszyn w hello wybrane jednostki Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="59a95-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="59a95-174">Dowiedz się więcej o korzystaniu z tooenable zasad grupy lub wyłącz dodatki programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="59a95-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="59a95-175">Krok 5 (opcjonalny): wyłączanie "Zapamiętaj hasło" wiersza</span><span class="sxs-lookup"><span data-stu-id="59a95-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="59a95-176">Gdy użytkownicy logowania toowebsites przy użyciu hello rozszerzenia Panel dostępu, program Internet Explorer mogą następujące hello Pokaż Monituj pytaniem "ma toostore hasła?"</span><span class="sxs-lookup"><span data-stu-id="59a95-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="59a95-177">W razie potrzeby tooprevent użytkownikom dostępu do tego wiersza, wykonaj czynności hello tooprevent automatycznego zakończenia od zapamiętywanie haseł:</span><span class="sxs-lookup"><span data-stu-id="59a95-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="59a95-178">W hello **Edytor zarządzania zasadami grupy** okna, ścieżka Przejdź toohello wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="59a95-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="59a95-179">Taka konfiguracja jest dostępna w obszarze tylko **Konfiguracja użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="59a95-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="59a95-180">Znajdź ustawienie hello o nazwie **włączyć funkcję hello automatycznie uzupełniać nazwy użytkownika i hasła w formularzach**.</span><span class="sxs-lookup"><span data-stu-id="59a95-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59a95-181">Poprzednie wersje usługi Active Directory może wyświetlić to ustawienie o nazwie hello **nie należy zezwalać haseł automatycznego zakończenia toosave**.</span><span class="sxs-lookup"><span data-stu-id="59a95-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="59a95-182">Witaj konfiguracji tego ustawienia różni się od hello ustawienia opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="59a95-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Należy pamiętać toolook w tym obszarze Ustawienia użytkownika.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="59a95-184">Kliknij prawym przyciskiem myszy hello powyżej ustawienia, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="59a95-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="59a95-185">W oknie hello **włączyć funkcję hello automatycznie uzupełniać nazwy użytkownika i hasła w formularzach**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="59a95-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Wybierz opcję Wyłącz](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="59a95-187">Kliknij przycisk **OK** tooapply te zmiany i zamknij hello okna.</span><span class="sxs-lookup"><span data-stu-id="59a95-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="59a95-188">Użytkownicy będzie już można toostore stanie swoich poświadczeń lub użyj automatycznego zakończenia tooaccess wcześniej zapisanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="59a95-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="59a95-189">Jednak ta zasada umożliwia toouse toocontinue użytkowników automatycznego zakończenia dla innych typów pól formularza, np. pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="59a95-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="59a95-190">Jeśli zasada ta jest włączona po użytkownik zdecydował toostore niektórych poświadczeń, te zasady będą *nie* wyczyść hello poświadczenia, które zostały już zapisane.</span><span class="sxs-lookup"><span data-stu-id="59a95-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="59a95-191">Krok 6: Testowanie hello wdrożenia</span><span class="sxs-lookup"><span data-stu-id="59a95-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="59a95-192">Wykonaj kroki hello poniżej tooverify, jeśli wdrożenie rozszerzenie hello zakończyło się pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="59a95-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="59a95-193">Jeśli została wdrożona przy użyciu **Konfiguracja komputera**, zaloguj się na komputerze klienckim, który należy toohello jednostek organizacyjnych, które wybrano w [krok 2: tworzenie hello obiektu zasad grupy](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="59a95-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="59a95-194">Jeśli została wdrożona przy użyciu **Konfiguracja użytkownika**, upewnij się, że toosign w jako użytkownik będący członkiem toothat jednostki Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="59a95-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="59a95-195">Może upłynąć kilka znak dodatków dla zasad grupy hello zmiany toofully aktualizacji z tego komputera.</span><span class="sxs-lookup"><span data-stu-id="59a95-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="59a95-196">Aktualizacja hello tooforce, otwórz **wiersza polecenia** okno i hello uruchom następujące polecenie:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="59a95-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="59a95-197">Należy ponownie uruchomić maszynę hello hello instalacji tootake miejsca.</span><span class="sxs-lookup"><span data-stu-id="59a95-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="59a95-198">Rozruchowego może potrwać znacznie więcej czasu niż zwykle podczas rozszerzenia hello instaluje.</span><span class="sxs-lookup"><span data-stu-id="59a95-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="59a95-199">Po ponownym uruchomieniu, otwórz **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="59a95-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="59a95-200">Na powitania prawym górnym rogu okna hello, kliknij przycisk **narzędzia** (hello koło zębate ikonę), a następnie wybierz **Zarządzanie dodatkami**.</span><span class="sxs-lookup"><span data-stu-id="59a95-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Przejdź tooTools > Zarządzanie dodatkami](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="59a95-202">W hello **Zarządzanie dodatkami** okna, sprawdź, że hello **rozszerzenia Panel dostępu** został zainstalowany, a jego **stan** została ustawiona zbyt**włączone**.</span><span class="sxs-lookup"><span data-stu-id="59a95-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![Upewnij się, że hello rozszerzenia Panel dostępu jest zainstalowany i włączony.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="59a95-204">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="59a95-204">Related Articles</span></span>
* [<span data-ttu-id="59a95-205">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59a95-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="59a95-206">Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59a95-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="59a95-207">Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="59a95-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

