---
title: "Zaloguj się instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zalogować się do programu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="f6c5f-103">Azure logowania instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="f6c5f-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="f6c5f-104">Zestaw narzędzi platformy Azure dla programu Eclipse udostępnia dwie metody logowanie do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="f6c5f-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="f6c5f-105">**Interakcyjne** — gdy używana jest ta metoda będzie wprowadź swoje poświadczenia usługi Azure każdym logowaniu się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="f6c5f-106">**Automatyczne** — w przypadku korzystania z tej metody spowoduje utworzenie pliku poświadczeń, który zawiera dane główne usługi, po upływie którego służy plik poświadczeń do automatycznego logowania się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="f6c5f-107">Kroki opisane w poniższych sekcjach opisano sposób używania każdej metody.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="f6c5f-108">Interakcyjne logowanie do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f6c5f-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="f6c5f-109">Poniższe kroki przedstawiają sposób logowania się do usługi Azure ręcznie wprowadzić poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="f6c5f-110">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f6c5f-111">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][I01]

1. <span data-ttu-id="f6c5f-113">Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **Interactive**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Zaloguj się okno dialogowe][I02]

1. <span data-ttu-id="f6c5f-115">Gdy **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][I03]

1. <span data-ttu-id="f6c5f-117">Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="f6c5f-119">Podpisywanie poza konta platformy Azure po zalogowaniu trybie interakcyjnym</span><span class="sxs-lookup"><span data-stu-id="f6c5f-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="f6c5f-120">Po skonfigurowaniu kroki opisane w poprzedniej sekcji, zostaną automatycznie wylogowani z konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f6c5f-121">Jednak jeśli chcesz wylogować się z konta platformy Azure bez ponownego uruchamiania Eclipse, należy użyć następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="f6c5f-122">W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu Eclipse Azure wylogowaniu][L01]

1. <span data-ttu-id="f6c5f-124">Gdy **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Wyloguj się okno dialogowe][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="f6c5f-126">Automatyczne logowanie do konta platformy Azure i utworzeniu pliku poświadczenia do użycia w przyszłości</span><span class="sxs-lookup"><span data-stu-id="f6c5f-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="f6c5f-127">Poniższe kroki przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="f6c5f-128">Po wykonaniu tych kroków, Eclipse będą automatycznie używać pliku poświadczeń do automatycznego rejestrowania użytkownika na platformie Azure każdym otwarciu projektu.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="f6c5f-129">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f6c5f-130">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][A01]

1. <span data-ttu-id="f6c5f-132">Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Zaloguj się okno dialogowe][A02]

1. <span data-ttu-id="f6c5f-134">Gdy **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A03]

1. <span data-ttu-id="f6c5f-136">Gdy **tworzenia plików uwierzytelniania** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A04]

1. <span data-ttu-id="f6c5f-138">**Stan Creatation nazwy głównej usługi** zostanie wyświetlone okno dialogowe i po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Okno dialogowe Stan Creatation nazwy głównej usługi][A05]

1. <span data-ttu-id="f6c5f-140">Gdy **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

1. <span data-ttu-id="f6c5f-142">Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="f6c5f-144">Podpisywanie poza konta platformy Azure po zalogowaniu automatycznie</span><span class="sxs-lookup"><span data-stu-id="f6c5f-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="f6c5f-145">Po skonfigurowaniu kroki opisane w poprzedniej sekcji, Azure Toolkit spowoduje automatyczne zalogowanie na konto platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f6c5f-146">Jednak aby wylogować się z konta platformy Azure i uniemożliwić automatycznego rejestrowania w zestawie narzędzi programu Azure, należy użyć następujących kroków.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="f6c5f-147">W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu Eclipse Azure wylogowaniu][L01]

1. <span data-ttu-id="f6c5f-149">Gdy **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Wyloguj się okno dialogowe][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="f6c5f-151">Logowanie do konta platformy Azure automatycznie przy użyciu pliku poświadczeń, które zostały już utworzone</span><span class="sxs-lookup"><span data-stu-id="f6c5f-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="f6c5f-152">Jeśli możesz wylogować się z platformy Azure, korzystając z programu Eclipse, należy ponownie skonfigurować zestaw narzędzi platformy Azure dla programu Eclipse użyć pliku poświadczeń, które zostały utworzone, aby automatycznie mógł zalogować się na konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="f6c5f-153">Poniższe kroki objaśniają Konfigurowanie narzędzi Azure, aby wykorzystywała istniejący plik poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="f6c5f-154">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f6c5f-155">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][A01]

1. <span data-ttu-id="f6c5f-157">Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Zaloguj się okno dialogowe][A02]

1. <span data-ttu-id="f6c5f-159">Gdy **wybierz plik uwierzytelniony** zostanie wyświetlone okno dialogowe, wybierz plik poświadczeń, który został utworzony wcześniej, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Zaloguj się okno dialogowe][A08]

1. <span data-ttu-id="f6c5f-161">Gdy **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

1. <span data-ttu-id="f6c5f-163">Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6c5f-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="see-also"></a><span data-ttu-id="f6c5f-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f6c5f-165">See Also</span></span>
<span data-ttu-id="f6c5f-166">Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="f6c5f-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="f6c5f-167">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f6c5f-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f6c5f-168">[What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f6c5f-169">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f6c5f-170">*Zaloguj się instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="f6c5f-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="f6c5f-171">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f6c5f-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="f6c5f-172">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f6c5f-173">[What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f6c5f-174">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f6c5f-175">[Sign In Instructions for the Azure Toolkit for IntelliJ] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f6c5f-176">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f6c5f-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="f6c5f-177">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="f6c5f-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="f6c5f-178">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f6c5f-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f6c5f-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="f6c5f-180">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f6c5f-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f6c5f-181">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f6c5f-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f6c5f-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f6c5f-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="f6c5f-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="f6c5f-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f6c5f-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f6c5f-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f6c5f-187">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f6c5f-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f6c5f-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f6c5f-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
