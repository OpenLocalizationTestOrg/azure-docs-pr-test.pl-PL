---
title: "aaaEnabling dostępu zdalnego we wdrożeniach Azure w programie Eclipse"
description: "Dowiedz się, jak dostęp zdalny tooenable wdrożeń platformy Azure przy użyciu hello Azure zestawu narzędzi dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="89f82-103">Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse</span><span class="sxs-lookup"><span data-stu-id="89f82-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="89f82-104">toohelp Rozwiązywanie problemów z wdrożeń, można włączyć i używać dostępu zdalnego tooconnect toohello hostowania maszyn wirtualnych wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="89f82-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="89f82-105">Witaj funkcje dostępu zdalnego zależy od hello protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="89f82-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="89f82-106">Po opublikowaniu go tooAzure lub jeśli Eclipse korzystają z systemu operacyjnego, można skonfigurować dostęp zdalny, przed opublikowaniem tooAzure, można skonfigurować dostęp zdalny dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="89f82-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="89f82-107">Należy pamiętać, że konieczne będzie klient usług pulpitu zdalnego, który jest zgodny z systemem operacyjnym w wdrożenia kolejności tooconnect tooyour maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89f82-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="89f82-108">Jak tooenable dostępu zdalnego, aby wdrożyć tooAzure</span><span class="sxs-lookup"><span data-stu-id="89f82-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="89f82-109">tooenable dostępu zdalnego przed wdrożeniem programu tooAzure aplikacji należy toobe uruchamianie Eclipse w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="89f82-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="89f82-110">Witaj poniższy obraz przedstawia hello **dostępu zdalnego** okna dialogowego właściwości używany tooenable dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="89f82-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="89f82-111">Istnieją dwa sposoby toodisplay hello **dostępu zdalnego** okno dialogowe właściwości:</span><span class="sxs-lookup"><span data-stu-id="89f82-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="89f82-112">Kliknij przycisk hello **zaawansowane** łącze w hello **dostępu zdalnego** sekcji hello **publikowania tooAzure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89f82-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="89f82-113">Otwórz hello **właściwości** okna dialogowego projektu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89f82-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="89f82-114">Podczas tworzenia nowego projektu wdrożenia usługi Azure hello projektu nie będzie miał dostępu zdalnego domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="89f82-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="89f82-115">Jednak łatwo można włączyć dostęp zdalny, określając hello nazwy użytkownika i hasła w hello **publikowania tooAzure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89f82-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="89f82-116">Hello hasła dostępu zdalnego jest szyfrowane za pomocą certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="89f82-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="89f82-117">Jeśli nie używasz dostarczyć własny certyfikat szyfrowania hello korzysta z certyfikatu z podpisem własnym dostarczone z hello Azure dodatek dla programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="89f82-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="89f82-118">Certyfikat z podpisem własnym jest hello **cert** folderu projektu platformy Azure, przechowywane zarówno jako plik certyfikatu publicznego (SampleRemoteAccessPublic.cer) i jako wymiany informacji osobistych (PFX) (pliku certyfikatu SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="89f82-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="89f82-119">ostatnie Hello zawiera hello klucza prywatnego dla certyfikatu hello i ma domyślne hasło, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="89f82-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="89f82-120">Jednak ponieważ hasło jest publiczny wiedzy, powinien być używany certyfikat domyślny hello tylko w przypadku uczenia celów, nie w przypadku wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="89f82-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="89f82-121">Tak innych niż do uczenia celów, jeśli chcesz tooenabled sesji zdalnych wdrożeń, należy kliknąć opcję hello **zaawansowane** łącze w hello **publikowania tooAzure** toospecify okna dialogowego własne certyfikat.</span><span class="sxs-lookup"><span data-stu-id="89f82-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="89f82-122">Należy pamiętać, że musisz mieć wersję PFX hello tooupload hello certyfikatu tooyour hostowanej usługi w ramach hello portalu zarządzania Azure, tak że Azure może odszyfrować hasła użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="89f82-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="89f82-123">Witaj pozostałej części samouczka hello pokazuje, jak dostęp zdalny tooenable dla projektu wdrożenia usługi Azure, która została początkowo utworzona dostęp zdalny wyłączony.</span><span class="sxs-lookup"><span data-stu-id="89f82-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="89f82-124">Do celów tego samouczka utworzymy nowy certyfikat z podpisem własnym, a jego plik PFX będzie miał hasła wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89f82-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="89f82-125">Istnieje również opcja hello przy użyciu certyfikatu wystawionego przez urząd certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="89f82-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="89f82-126">Jak tooenable dostępu zdalnego po wdrożeniu tooAzure</span><span class="sxs-lookup"><span data-stu-id="89f82-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="89f82-127">dostęp zdalny tooenable po wdrożeniu tooAzure, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="89f82-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="89f82-128">Zaloguj się do portalu zarządzania Azure hello przy użyciu konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89f82-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="89f82-129">Na liście **usługi w chmurze**, wybierz usługi w chmurze wdrożone</span><span class="sxs-lookup"><span data-stu-id="89f82-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="89f82-130">Na stronie sieci web usługi chmury hello, kliknij przycisk hello **Konfiguruj** łącza</span><span class="sxs-lookup"><span data-stu-id="89f82-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="89f82-131">Na dole hello hello na stronie konfiguracji, kliknij przycisk hello **zdalnego** łącza</span><span class="sxs-lookup"><span data-stu-id="89f82-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="89f82-132">Kiedy wyświetli się okno podręczne okno dialogowe hello:</span><span class="sxs-lookup"><span data-stu-id="89f82-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="89f82-133">Określ hello rolę dla której ma zostać tooenable dostępu zdalnego</span><span class="sxs-lookup"><span data-stu-id="89f82-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="89f82-134">Kliknij przycisk tooselect hello **Włącz pulpit zdalny** wyboru</span><span class="sxs-lookup"><span data-stu-id="89f82-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="89f82-135">Określ nazwę użytkownika i hasło mają toouse dla dostępu zdalnego</span><span class="sxs-lookup"><span data-stu-id="89f82-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="89f82-136">Wybierz hello toouse certyfikatu</span><span class="sxs-lookup"><span data-stu-id="89f82-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="89f82-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89f82-137">Click **OK**</span></span> 

<span data-ttu-id="89f82-138">Zostanie wyświetlony komunikat informujący, że zmiany konfiguracji jest w toku, co może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="89f82-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="89f82-139">Po zakończeniu hello zmianę konfiguracji, wykonaj kroki hello hello **toolog w zdalnie** sekcji w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="89f82-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="89f82-140">W jaki sposób tooenable zdalnego dostępu do pakietu</span><span class="sxs-lookup"><span data-stu-id="89f82-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="89f82-141">W okienku Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy projekt platformy Azure, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="89f82-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="89f82-142">W hello **właściwości** okna dialogowego, rozwiń węzeł **Azure** w okienku po lewej stronie powitania i kliknij przycisk **dostępu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="89f82-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="89f82-143">W hello **dostępu zdalnego** okna dialogowego, upewnij się, **Włącz wszystkie role tooaccept połączeń pulpitu zdalnego przy użyciu tych poświadczeń logowania** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="89f82-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="89f82-144">Określ nazwę użytkownika dla hello Podłączanie pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="89f82-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="89f82-145">Określ i Potwierdź hasło hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89f82-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="89f82-146">Witaj użytkownika nazwę i hasło wartości w tym oknie dialogowym będą używane podczas tworzenia połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="89f82-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="89f82-147">(Należy zauważyć, że jest to oddzielnych haseł z hasła do pliku PFX).</span><span class="sxs-lookup"><span data-stu-id="89f82-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="89f82-148">Określ datę wygaśnięcia hello hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89f82-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="89f82-149">Kliknij przycisk **nowy** toocreate nowego certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="89f82-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="89f82-150">(Można również należy wybierać certyfikat z obszaru roboczego lub pliku systemu za pośrednictwem hello **obszaru roboczego** lub **FileSystem** przyciski, odpowiednio, ale dla celów tego samouczka, utworzymy nową certyfikat).</span><span class="sxs-lookup"><span data-stu-id="89f82-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="89f82-151">W hello **nowego świadectwa** okna dialogowego, określ i Potwierdź hasło hello użyjesz dla pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="89f82-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="89f82-152">Zaakceptuj wartość hello **nazwa (CN)**, lub użyj nazwy niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="89f82-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="89f82-153">Określ hello ścieżka i nazwa pliku którym zostanie zapisany nowy certyfikat hello w postaci cer.</span><span class="sxs-lookup"><span data-stu-id="89f82-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="89f82-154">Dla tego kroku i hello następnego kroku, możesz użyć hello **cert** folderu projektu platformy Azure, ale w przypadku wolnego toochoose innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="89f82-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="89f82-155">Do celów tego samouczka, użyjemy **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="89f82-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="89f82-156">(Tworzenie hello **c:\mycert** tooproceeding poprzedniego folderu lub użyj istniejącego folderu, w razie potrzeby.)</span><span class="sxs-lookup"><span data-stu-id="89f82-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="89f82-157">Określ hello ścieżka i nazwa pliku którym zostanie zapisany hello nowego certyfikatu i klucza prywatnego, w postaci pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="89f82-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="89f82-158">Do celów tego samouczka, użyjemy **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="89f82-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="89f82-159">Twoje **nowego świadectwa** okna dialogowego powinna wyglądać podobnie następujące toohello (Zaktualizuj hello ścieżki folderu, jeśli nie używasz **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="89f82-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="89f82-160">Kliknij przycisk **OK** tooclose hello **nowego świadectwa** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89f82-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="89f82-161">Twoje **dostępu zdalnego** okna dialogowego powinna wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="89f82-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="89f82-162">Kliknij przycisk **OK** tooclose hello **dostępu zdalnego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89f82-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="89f82-163">Aplikacja jest ponownie kompilowana, hello kompilacji zestawu dla wdrożenia toocloud.</span><span class="sxs-lookup"><span data-stu-id="89f82-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="89f82-164">toolog w zdalnie</span><span class="sxs-lookup"><span data-stu-id="89f82-164">toolog in remotely</span></span>
<span data-ttu-id="89f82-165">Gdy wystąpienie roli jest gotowy, może zdalnie zalogować toohello maszyny wirtualnej, który jest hostem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89f82-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="89f82-166">Jeśli używasz programu Eclipse w systemach Windows i wybranych hello **wdrożyć uruchomienia pulpitu zdalnego na** opcja podczas tooAzure Twojego wdrożenia, zostanie wyświetlona Podłączanie pulpitu zdalnego ekran logowania po uruchomieniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="89f82-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="89f82-167">Po wyświetleniu monitu o hello nazwy użytkownika i hasła, wprowadź wartości hello, określone dla użytkownika zdalnego hello i będą mogli toolog w.</span><span class="sxs-lookup"><span data-stu-id="89f82-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="89f82-168">Inny sposób toolog w zdalnie odbywa się za pośrednictwem hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portalu zarządzania Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="89f82-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="89f82-169">W ramach hello **usługi w chmurze** widok hello portalu zarządzania Azure, kliknij pozycję usługi w chmurze, kliknij przycisk **wystąpień**, kliknij przycisk określonego wystąpienia, a następnie kliknij przycisk hello **Connect**przycisku.</span><span class="sxs-lookup"><span data-stu-id="89f82-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="89f82-170">Witaj **Connect** przycisk pojawia się następujący hello na pasku poleceń hello:</span><span class="sxs-lookup"><span data-stu-id="89f82-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="89f82-171">Po kliknięciu przycisku hello **Connect** przycisku będzie tooopen zostanie wyświetlony monit o plik RDP.</span><span class="sxs-lookup"><span data-stu-id="89f82-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="89f82-172">Otwórz plik hello i postępuj zgodnie z monitami hello.</span><span class="sxs-lookup"><span data-stu-id="89f82-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="89f82-173">(Możesz można także zapisać komputera lokalnego tooyour pliku, a następnie uruchom plik hello przez dwukrotne kliknięcie dziennika tooremote w tooyour maszyny wirtualnej bez konieczności toofirst Przejdź w portalu zarządzania hello.)</span><span class="sxs-lookup"><span data-stu-id="89f82-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="89f82-174">Po wyświetleniu monitu o hello nazwy użytkownika i hasła, wprowadź wartości hello, określone dla użytkownika zdalnego hello i będą mogli toolog w.</span><span class="sxs-lookup"><span data-stu-id="89f82-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="89f82-175">Jeśli w systemie operacyjnym z systemem innym niż Windows, należy toouse klienta pulpitu zdalnego, który jest zgodny z systemem operacyjnym i wykonaj tooconfigure kroki powitania klienta z ustawieniami hello w pliku RDP hello.</span><span class="sxs-lookup"><span data-stu-id="89f82-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="89f82-176">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="89f82-176">See Also</span></span>
<span data-ttu-id="89f82-177">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89f82-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="89f82-178">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89f82-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="89f82-179">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89f82-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="89f82-180">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="89f82-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
