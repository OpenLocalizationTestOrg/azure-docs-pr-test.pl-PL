---
title: "Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse"
description: "Dowiedz się, jak włączyć dostęp zdalny dla wdrożeń platformy Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="42afe-103">Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse</span><span class="sxs-lookup"><span data-stu-id="42afe-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="42afe-104">Do rozwiązywania problemów wdrożeń, można włączyć i używać dostępu zdalnego do nawiązania połączenia hostowania wdrożenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="42afe-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="42afe-105">Funkcje dostępu zdalnego polega na protokołu RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="42afe-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="42afe-106">Dostęp zdalny można skonfigurować dla danego wdrożenia po opublikowano na platformie Azure, lub jeśli Eclipse korzystają z systemu operacyjnego, można skonfigurować dostęp zdalny przed publikowanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="42afe-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="42afe-107">Należy pamiętać, że konieczne będzie klient usług pulpitu zdalnego, który jest zgodny z systemu operacyjnego w celu nawiązania połączenia z wdrożenia maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42afe-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="42afe-108">Jak włączyć dostęp zdalny, przed wdrożeniem na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="42afe-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="42afe-109">Aby włączyć dostęp zdalny, przed wdrożeniem aplikacji na platformie Azure, musi działać w środowisku Eclipse w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="42afe-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="42afe-110">Poniższy obraz przedstawia **dostępu zdalnego** okna dialogowego właściwości włączania dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="42afe-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="42afe-111">Istnieją dwa sposoby wyświetlania **dostępu zdalnego** okno dialogowe właściwości:</span><span class="sxs-lookup"><span data-stu-id="42afe-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="42afe-112">Kliknij przycisk **zaawansowane** łącze w **dostępu zdalnego** sekcji **publikowania na platformie Azure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42afe-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="42afe-113">Otwórz **właściwości** okna dialogowego projektu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42afe-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="42afe-114">Podczas tworzenia nowego projektu wdrożenia usługi Azure projektu nie będzie miał dostępu zdalnego domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="42afe-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="42afe-115">Jednak łatwo można włączyć dostęp zdalny, określając nazwę użytkownika i hasło w **publikowania na platformie Azure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42afe-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="42afe-116">Hasła dostępu zdalnego jest szyfrowane za pomocą certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="42afe-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="42afe-117">Jeśli nie używasz dostarczyć własny certyfikat szyfrowania korzysta z certyfikatu z podpisem własnym dostarczone z wtyczki Azure dla programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="42afe-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="42afe-118">Certyfikat z podpisem własnym jest **cert** folderu projektu platformy Azure, przechowywane zarówno jako plik certyfikatu publicznego (SampleRemoteAccessPublic.cer) i jako wymiany informacji osobistych (PFX) (pliku certyfikatu SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="42afe-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="42afe-119">Zawiera klucz prywatny certyfikatu i ma domyślne hasło, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="42afe-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="42afe-120">Jednak ponieważ hasło jest publiczny wiedzy, powinien być używany certyfikat domyślny tylko w przypadku uczenia celów, nie w przypadku wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="42afe-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="42afe-121">Dlatego inne niż do uczenia celów, jeśli chcesz włączyć sesji zdalnych wdrożeń, należy kliknąć opcję **zaawansowane** łącze w **publikowania na platformie Azure** okna dialogowego, aby określić własny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="42afe-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="42afe-122">Należy pamiętać, że musisz przekazać wersja PFX certyfikatu w usłudze hostowanej w portalu zarządzania Azure, tak że Azure może odszyfrować hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42afe-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="42afe-123">W pozostałej części samouczka przedstawiono sposób włączania dostępu zdalnego dla projektu wdrożenia usługi Azure, która została początkowo utworzona dostęp zdalny wyłączony.</span><span class="sxs-lookup"><span data-stu-id="42afe-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="42afe-124">Do celów tego samouczka utworzymy nowy certyfikat z podpisem własnym, a jego plik PFX będzie miał hasła wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42afe-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="42afe-125">Istnieje również możliwość z użyciem certyfikatu wydanego przez urząd certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="42afe-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="42afe-126">Jak włączyć dostęp zdalny, po wdrożeniu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="42afe-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="42afe-127">Aby włączyć dostęp zdalny, po wdrożeniu na platformie Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="42afe-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="42afe-128">Zaloguj się do portalu zarządzania platformy Azure przy użyciu konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="42afe-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="42afe-129">Na liście **usługi w chmurze**, wybierz usługi w chmurze wdrożone</span><span class="sxs-lookup"><span data-stu-id="42afe-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="42afe-130">Na stronie sieci web usługi chmury kliknij **Konfiguruj** łącza</span><span class="sxs-lookup"><span data-stu-id="42afe-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="42afe-131">W dolnej części strony konfiguracji, kliknij polecenie **zdalnego** łącza</span><span class="sxs-lookup"><span data-stu-id="42afe-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="42afe-132">Kiedy wyświetli się okno podręczne okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="42afe-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="42afe-133">Określ rolę, dla której ma być włączyć dostęp zdalny</span><span class="sxs-lookup"><span data-stu-id="42afe-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="42afe-134">Kliknij, aby wybrać **Włącz pulpit zdalny** wyboru</span><span class="sxs-lookup"><span data-stu-id="42afe-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="42afe-135">Określ nazwę użytkownika i hasło, którego chcesz użyć dla dostępu zdalnego</span><span class="sxs-lookup"><span data-stu-id="42afe-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="42afe-136">Wybierz certyfikat do użycia</span><span class="sxs-lookup"><span data-stu-id="42afe-136">Select the certificate to use</span></span>

6. <span data-ttu-id="42afe-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="42afe-137">Click **OK**</span></span> 

<span data-ttu-id="42afe-138">Zostanie wyświetlony komunikat informujący, że zmiany konfiguracji jest w toku, co może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="42afe-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="42afe-139">Po zmianie konfiguracji została ukończona, postępuj zgodnie z instrukcjami **zdalnego logowania** sekcji w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="42afe-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="42afe-140">Jak włączyć dostęp zdalny do pakietu</span><span class="sxs-lookup"><span data-stu-id="42afe-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="42afe-141">W okienku Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy projekt platformy Azure, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="42afe-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="42afe-142">W **właściwości** okna dialogowego, rozwiń węzeł **Azure** w okienku po lewej stronie i kliknij przycisk **dostępu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="42afe-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="42afe-143">W **dostępu zdalnego** okna dialogowego, upewnij się, **Włącz wszystkie role do akceptowania połączeń pulpitu zdalnego przy użyciu tych poświadczeń logowania** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="42afe-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="42afe-144">Określ nazwę użytkownika dla połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="42afe-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="42afe-145">Określ i Potwierdź hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42afe-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="42afe-146">Wartości nazwy i hasła użytkownika w tym oknie dialogowym będą używane podczas tworzenia połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="42afe-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="42afe-147">(Należy zauważyć, że jest to oddzielnych haseł z hasła do pliku PFX).</span><span class="sxs-lookup"><span data-stu-id="42afe-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="42afe-148">Określ datę wygaśnięcia konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42afe-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="42afe-149">Kliknij przycisk **nowy** można utworzyć nowego certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="42afe-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="42afe-150">(Można również należy wybierać certyfikat z obszaru roboczego lub pliku systemu za pośrednictwem **obszaru roboczego** lub **FileSystem** przyciski, odpowiednio, ale dla celów tego samouczka, utworzymy nową certyfikat).</span><span class="sxs-lookup"><span data-stu-id="42afe-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="42afe-151">W **nowego świadectwa** okna dialogowego, określ i Potwierdź hasło będzie używany dla pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="42afe-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="42afe-152">Zaakceptuj wartość podana dla **nazwa (CN)**, lub użyj nazwy niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="42afe-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="42afe-153">Określ ścieżkę i nazwę, którym zostanie zapisany nowy certyfikat w formie cer.</span><span class="sxs-lookup"><span data-stu-id="42afe-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="42afe-154">Ten krok i następnego kroku, możesz użyć **cert** folderu projektu platformy Azure, ale jest wolny wybrać inną lokalizację.</span><span class="sxs-lookup"><span data-stu-id="42afe-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="42afe-155">Do celów tego samouczka, użyjemy **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="42afe-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="42afe-156">(Tworzenie **c:\mycert** folderu przed kontynuowaniem lub użyj istniejącego folderu, w razie potrzeby.)</span><span class="sxs-lookup"><span data-stu-id="42afe-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="42afe-157">Określ ścieżkę i nazwę, którym zostanie zapisany nowy certyfikat i jego klucz prywatny, w postaci pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="42afe-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="42afe-158">Do celów tego samouczka, użyjemy **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="42afe-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="42afe-159">Twoje **nowego świadectwa** okna dialogowego powinien wyglądać podobnie do następującego (aktualizacja ścieżki folderu, jeśli nie używasz **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="42afe-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="42afe-160">Kliknij przycisk **OK** zamknąć **nowego świadectwa** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42afe-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="42afe-161">Twoje **dostępu zdalnego** okna dialogowego powinien wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="42afe-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="42afe-162">Kliknij przycisk **OK** zamknąć **dostępu zdalnego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42afe-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="42afe-163">Ponownie aplikacji, za pomocą kompilacji zestawu dla wdrożenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="42afe-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="42afe-164">Aby zalogować się zdalnie</span><span class="sxs-lookup"><span data-stu-id="42afe-164">To log in remotely</span></span>
<span data-ttu-id="42afe-165">Gdy wystąpienie roli jest gotowy, można zdalnie zalogować się do maszyny wirtualnej, który jest hostem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42afe-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="42afe-166">Jeśli używasz programu Eclipse w systemach Windows i wybranych **wdrożyć uruchomienia pulpitu zdalnego na** opcji podczas wdrażania na platformie Azure zostaną wyświetlone Podłączanie pulpitu zdalnego ekran logowania po uruchomieniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="42afe-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="42afe-167">Po wyświetleniu monitu o nazwę użytkownika i hasło, wprowadź wartości określone dla użytkownika zdalnego i będą mogli się zalogować.</span><span class="sxs-lookup"><span data-stu-id="42afe-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="42afe-168">Innym sposobem zdalnego logowania jest za pośrednictwem <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portalu zarządzania Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="42afe-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="42afe-169">W ramach **usługi w chmurze** widok portalu zarządzania Azure, kliknij pozycję usługi w chmurze, kliknij przycisk **wystąpień**, kliknij określonego wystąpienia, a następnie kliknij przycisk **Connect** przycisk.</span><span class="sxs-lookup"><span data-stu-id="42afe-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="42afe-170">**Connect** przycisk pojawia się następujący na pasku poleceń:</span><span class="sxs-lookup"><span data-stu-id="42afe-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="42afe-171">Po kliknięciu przycisku **Connect** przycisku, zostanie wyświetlony monit do otwarcia pliku RDP.</span><span class="sxs-lookup"><span data-stu-id="42afe-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="42afe-172">Otwórz plik i postępuj zgodnie z monitami.</span><span class="sxs-lookup"><span data-stu-id="42afe-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="42afe-173">(Możesz można także zapisać ten plik na komputerze lokalnym, a następnie uruchom plik przez dwukrotne kliknięcie do zdalnego logowania się z maszyną wirtualną bez konieczności najpierw przejść do portalu zarządzania.)</span><span class="sxs-lookup"><span data-stu-id="42afe-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="42afe-174">Po wyświetleniu monitu o nazwę użytkownika i hasło, wprowadź wartości określone dla użytkownika zdalnego i będą mogli się zalogować.</span><span class="sxs-lookup"><span data-stu-id="42afe-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="42afe-175">Jeśli w systemie operacyjnym z systemem innym niż Windows, należy klienta pulpitu zdalnego, który jest zgodny z systemem operacyjnym i wykonaj kroki konfigurowania klienta przy użyciu ustawień w pliku RDP, który został pobrany.</span><span class="sxs-lookup"><span data-stu-id="42afe-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="42afe-176">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="42afe-176">See Also</span></span>
<span data-ttu-id="42afe-177">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="42afe-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="42afe-178">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="42afe-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="42afe-179">[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="42afe-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="42afe-180">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="42afe-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
