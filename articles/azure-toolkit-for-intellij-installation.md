---
title: "Instalowanie zestawu narzędzi platformy Azure dla IntelliJ | Dokumentacja firmy Microsoft"
description: "Informacje o instalowaniu zestawu narzędzi Azure for IntelliJ IDEA."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bf11a8580500f78c4a96a02953f221501eeffe6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c060a-103">Instalowanie zestawu narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c060a-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c060a-104">Zestaw narzędzi platformy Azure dla IntelliJ zawiera szablony i funkcje, które umożliwiają łatwe tworzenie, tworzenie, testowanie i wdrażanie aplikacji platformy Azure przy użyciu środowiska programowania IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c060a-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="c060a-105">Zestaw narzędzi platformy Azure dla IntelliJ jest projekt typu Open Source, którego kod źródłowy jest dostępny w ramach licencji MIT z projektu w witrynie GitHub pod adresem URL:</span><span class="sxs-lookup"><span data-stu-id="c060a-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="c060a-106"><https://github.com/Microsoft/Azure-Tools-for-Java></span><span class="sxs-lookup"><span data-stu-id="c060a-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="c060a-107">Istnieją dwie metody instalowania zestawu narzędzi Azure for IntelliJ, w oknie dialogowym Ustawienia i z menu konfigurowanie na ekranie startowym; Obie metody instalacji będzie przedstawiono w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="c060a-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="c060a-108">Aby zainstalować zestaw narzędzi platformy Azure dla IntelliJ w oknie dialogowym Ustawienia</span><span class="sxs-lookup"><span data-stu-id="c060a-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>
1. <span data-ttu-id="c060a-109">Uruchom środowisko IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c060a-109">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="c060a-110">Po otwarciu IntelliJ IDEA, kliknij **pliku**, następnie kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c060a-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
    ![Otwórz okno dialogowe Ustawienia IntelliJ IDEA][01a]
3. <span data-ttu-id="c060a-112">W oknie dialogowym Ustawienia, kliknij przycisk **wtyczek**, a następnie kliknij przycisk **Przeglądaj repozytoria**.</span><span class="sxs-lookup"><span data-stu-id="c060a-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
    ![Okno dialogowe Ustawienia ROZWIĄZANIEM IntelliJ][02a]
4. <span data-ttu-id="c060a-114">W **Przeglądaj repozytoria** oknie dialogowym wpisz "Azure" w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c060a-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="c060a-115">Wyróżnij **narzędzi Azure dla IntelliJ**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="c060a-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Wyszukiwanie Azure Toolkit IntelliJ][03]
   
    <span data-ttu-id="c060a-117">IntelliJ IDEA wyświetli się postęp instalacji w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="c060a-117">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Postęp instalacji][04]
5. <span data-ttu-id="c060a-119">Po zakończeniu instalacji kliknij przycisk **ponowne uruchomienie IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="c060a-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Uruchom ponownie IntelliJ IDEA][05]
6. <span data-ttu-id="c060a-121">Kliknij przycisk **OK** aby zamknąć okno dialogowe Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c060a-121">Click **OK** to close the Settings dialog box.</span></span>
   
    ![Zamknij okno dialogowe Ustawienia ROZWIĄZANIEM IntelliJ][06]
7. <span data-ttu-id="c060a-123">Po wyświetleniu monitu o ponowne uruchomienie IntelliJ IDEA lub odłożyć, kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="c060a-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Uruchom ponownie IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="c060a-125">Aby zainstalować zestaw narzędzi platformy Azure dla IntelliJ z ekranu startowego</span><span class="sxs-lookup"><span data-stu-id="c060a-125">To install the Azure Toolkit for IntelliJ from the start screen</span></span>
1. <span data-ttu-id="c060a-126">Uruchom środowisko IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c060a-126">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="c060a-127">Po wyświetleniu ekranu startowego IntelliJ IDEA kliknij **Konfiguruj**, następnie kliknij przycisk **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="c060a-127">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
    ![Zainstaluj środowisko IntelliJ IDEA wtyczek][01b]
3. <span data-ttu-id="c060a-129">W **wtyczek** okno dialogowe, kliknij przycisk **Przeglądaj repozytoria**.</span><span class="sxs-lookup"><span data-stu-id="c060a-129">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
    ![Przeglądaj IntelliJ IDEA wtyczki repozytoria][02b]
4. <span data-ttu-id="c060a-131">W **Przeglądaj repozytoria** oknie dialogowym wpisz "Azure" w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c060a-131">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="c060a-132">Wyróżnij **narzędzi Azure dla IntelliJ**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="c060a-132">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Wyszukiwanie Azure Toolkit IntelliJ][03]
   
    <span data-ttu-id="c060a-134">IntelliJ IDEA wyświetli się postęp instalacji w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="c060a-134">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Postęp instalacji][04]
5. <span data-ttu-id="c060a-136">Po zakończeniu instalacji kliknij przycisk **ponowne uruchomienie IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="c060a-136">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Uruchom ponownie IntelliJ IDEA][05]
6. <span data-ttu-id="c060a-138">Po wyświetleniu monitu o ponowne uruchomienie IntelliJ IDEA lub odłożyć, kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="c060a-138">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Uruchom ponownie IntelliJ IDEA][07]

## <a name="see-also"></a><span data-ttu-id="c060a-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c060a-140">See Also</span></span>
<span data-ttu-id="c060a-141">Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="c060a-141">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="c060a-142">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c060a-142">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c060a-143">[What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-143">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c060a-144">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-144">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c060a-145">[Sign In Instructions for the Azure Toolkit for Eclipse] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-145">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c060a-146">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c060a-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="c060a-147">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-147">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c060a-148">[What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-148">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c060a-149">*Instalowanie zestawu narzędzi platformy Azure dla IntelliJ (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="c060a-149">*Installing the Azure Toolkit for IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="c060a-150">[Sign In Instructions for the Azure Toolkit for IntelliJ] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-150">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c060a-151">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c060a-151">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="c060a-152">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c060a-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="c060a-153">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="c060a-153">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="c060a-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="c060a-155">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c060a-155">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c060a-156">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c060a-156">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c060a-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
<span data-ttu-id="c060a-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="c060a-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="c060a-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="c060a-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="c060a-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c060a-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="c060a-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c060a-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01a]: ./media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: ./media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: ./media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: ./media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: ./media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: ./media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: ./media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: ./media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: ./media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
