---
title: "Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zalogować się do systemu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="580e9-103">Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="580e9-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="580e9-104">Zestaw narzędzi platformy Azure dla IntelliJ udostępnia dwie metody logowania do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="580e9-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="580e9-105">**Interakcyjne**: należy wprowadzić poświadczenia platformy Azure za każdym razem, zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="580e9-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="580e9-106">**Automatyczne**: Tworzenie pliku poświadczeń, który służy do automatycznego logowania do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="580e9-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="580e9-107">W poniższych sekcjach opisano sposób używania każdej metody.</span><span class="sxs-lookup"><span data-stu-id="580e9-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="580e9-108">Zaloguj się interaktywnie do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="580e9-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="580e9-109">Aby zalogować się do platformy Azure ręcznie wprowadzić poświadczenia platformy Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="580e9-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="580e9-110">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="580e9-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="580e9-111">Kliknij przycisk **narzędzia**, wskaż polecenie **Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="580e9-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Polecenie IntelliJ Azure logowania][I01]

3. <span data-ttu-id="580e9-113">W **Azure logowania** wybierz **Interactive**, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Okno Azure logowania z Interactive wybrane][I02]

4. <span data-ttu-id="580e9-115">W **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![W oknie dialogowym logowania do platformy Azure][I03]

5. <span data-ttu-id="580e9-117">W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="580e9-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Okno dialogowe Wybieranie subskrypcji][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="580e9-119">Wylogować się z konta platformy Azure, po zarejestrowaniu trybie interakcyjnym</span><span class="sxs-lookup"><span data-stu-id="580e9-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="580e9-120">Po skonfigurowaniu konta przy użyciu powyższych kroków możesz spowoduje automatyczne wylogowanie z konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="580e9-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="580e9-121">Jednak jeśli chcesz wylogować się z konta platformy Azure *bez* ponowne uruchomienie IntelliJ IDEA, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="580e9-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="580e9-122">W IntelliJ IDEA na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Polecenie IntelliJ Azure Wyloguj][L01]

2. <span data-ttu-id="580e9-124">W **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="580e9-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Okno potwierdzenia Azure Wyloguj][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="580e9-126">Zaloguj się do konta platformy Azure automatycznie</span><span class="sxs-lookup"><span data-stu-id="580e9-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="580e9-127">Ta sekcja przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi.</span><span class="sxs-lookup"><span data-stu-id="580e9-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="580e9-128">Po zakończeniu tego procesu Eclipse używa pliku poświadczeń do automatycznie Cię logować do usługi Azure każdym otwarciu projektu.</span><span class="sxs-lookup"><span data-stu-id="580e9-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="580e9-129">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="580e9-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="580e9-130">Na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="580e9-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Polecenie IntelliJ Azure logowania][A01]

3. <span data-ttu-id="580e9-132">W **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="580e9-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Okno Azure logowania z automatycznego wybrane][A02]

4. <span data-ttu-id="580e9-134">W **dialogowym logowania do usługi Azure** okna, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![W oknie dialogowym logowania do platformy Azure][A03]

5. <span data-ttu-id="580e9-136">W **tworzenia plików uwierzytelniania** okna, wybierz subskrypcje, które chcesz użyć, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="580e9-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Tworzenie plików uwierzytelniania okna][A04]

6. <span data-ttu-id="580e9-138">W **stan tworzenia nazwy głównej usługi** okno dialogowe po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="580e9-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Okno dialogowe Stan tworzenia nazwy głównej usługi][A05]

7. <span data-ttu-id="580e9-140">W **Azure logowania** okna, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

8. <span data-ttu-id="580e9-142">W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="580e9-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Okno dialogowe Wybieranie subskrypcji][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="580e9-144">Wylogować się z konta platformy Azure po zalogowaniu się automatycznie</span><span class="sxs-lookup"><span data-stu-id="580e9-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="580e9-145">Po skonfigurowaniu konta przy użyciu powyższych kroków Azure Toolkit automatycznie loguje się użytkownik do konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="580e9-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="580e9-146">Jednak aby wylogować się z konta platformy Azure i uniemożliwić automatycznego rejestrowania w zestawie narzędzi programu Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="580e9-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="580e9-147">W IntelliJ IDEA na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Polecenie IntelliJ Azure Wyloguj][L01]

2. <span data-ttu-id="580e9-149">W **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="580e9-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Okno potwierdzenia Azure Wyloguj][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="580e9-151">Zaloguj się do konta platformy Azure automatycznie przy użyciu istniejącego pliku poświadczeń</span><span class="sxs-lookup"><span data-stu-id="580e9-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="580e9-152">Jeśli możesz wylogować się z konta platformy Azure, korzystając z IntelliJ IDEA, możesz korzystać istniejący plik poświadczeń do automatycznie zalogować się do konta.</span><span class="sxs-lookup"><span data-stu-id="580e9-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="580e9-153">Aby skonfigurować zestaw narzędzi platformy Azure dla programu Eclipse wykorzystywała istniejący plik poświadczeń, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="580e9-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="580e9-154">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="580e9-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="580e9-155">Na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="580e9-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Polecenie IntelliJ Azure logowania][A01]

3. <span data-ttu-id="580e9-157">W **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Okno Azure logowania z automatycznego wybrane][A02]

4. <span data-ttu-id="580e9-159">W **wybierz plik Authentication** okno dialogowe, wybierz plik utworzonej wcześniej poświadczenia, a następnie kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="580e9-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Wybierz plik Authentication — okno dialogowe][A08]

5. <span data-ttu-id="580e9-161">W **Azure logowania** okna, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="580e9-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Okno Azure logowania z automatycznego wybrane][A06]

6. <span data-ttu-id="580e9-163">W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="580e9-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Okno dialogowe Wybieranie subskrypcji][A07]

## <a name="next-steps"></a><span data-ttu-id="580e9-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="580e9-165">Next steps</span></span>
<span data-ttu-id="580e9-166">Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="580e9-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="580e9-167">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="580e9-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="580e9-168">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="580e9-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="580e9-169">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="580e9-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="580e9-170">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="580e9-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="580e9-171">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="580e9-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="580e9-172">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="580e9-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="580e9-173">[Nowości w zestawie narzędzi programu Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="580e9-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="580e9-174">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="580e9-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="580e9-175">*Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ* (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="580e9-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="580e9-176">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="580e9-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="580e9-177">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="580e9-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="580e9-178">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="580e9-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="580e9-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="580e9-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="580e9-180">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="580e9-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="580e9-181">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="580e9-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="580e9-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="580e9-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="580e9-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="580e9-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="580e9-184">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="580e9-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="580e9-185">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="580e9-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="580e9-186">[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="580e9-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="580e9-187">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="580e9-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="580e9-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="580e9-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
