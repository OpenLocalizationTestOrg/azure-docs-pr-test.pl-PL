---
title: "aaaSign w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosign w Microsoft Azure przy użyciu hello zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="1c7e1-103">Azure znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="1c7e1-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="1c7e1-104">zestaw narzędzi platformy Azure dla programu Eclipse Hello udostępnia dwie metody logowanie do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="1c7e1-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="1c7e1-105">**Interakcyjne** — gdy używana jest ta metoda będzie wprowadź swoje poświadczenia usługi Azure każdym logowaniu się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="1c7e1-106">**Automatyczne** — w przypadku korzystania z tej metody spowoduje utworzenie pliku poświadczeń, który zawiera dane główne usługi, po upływie którego można użyć hello poświadczenia pliku tooautomatically logowania do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="1c7e1-107">Witaj kroki hello w następujących sekcjach opisano sposób toouse każdej metody.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="1c7e1-108">Interakcyjne logowanie do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1c7e1-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="1c7e1-109">Witaj poniższe kroki przedstawiają sposób toosign na platformie Azure ręcznie wprowadzić poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="1c7e1-110">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="1c7e1-111">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][I01]

1. <span data-ttu-id="1c7e1-113">Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **Interactive**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Zaloguj się okno dialogowe][I02]

1. <span data-ttu-id="1c7e1-115">Gdy hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][I03]

1. <span data-ttu-id="1c7e1-117">Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="1c7e1-119">Podpisywanie poza konta platformy Azure po zalogowaniu trybie interakcyjnym</span><span class="sxs-lookup"><span data-stu-id="1c7e1-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="1c7e1-120">Po skonfigurowaniu hello kroki opisane w poprzedniej sekcji hello, zostaną automatycznie wylogowani z konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="1c7e1-121">Jednak jeśli chcesz toosign poza konta platformy Azure bez ponownego uruchamiania programu Eclipse, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="1c7e1-122">W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu Eclipse Azure wylogowaniu][L01]

1. <span data-ttu-id="1c7e1-124">Gdy hello **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Wyloguj się okno dialogowe][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="1c7e1-126">Automatyczne logowanie do konta platformy Azure i tworzenia poświadczeń dla plików toouse w hello przyszłych</span><span class="sxs-lookup"><span data-stu-id="1c7e1-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="1c7e1-127">Witaj następujące kroki przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="1c7e1-128">Po wykonaniu tych kroków, Eclipse zostanie automatycznie użyj hello poświadczenia pliku tooautomatically logowania się, że możesz w każdej Azure czasu Otwórz projekt.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="1c7e1-129">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="1c7e1-130">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][A01]

1. <span data-ttu-id="1c7e1-132">Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Zaloguj się okno dialogowe][A02]

1. <span data-ttu-id="1c7e1-134">Gdy hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A03]

1. <span data-ttu-id="1c7e1-136">Gdy hello **tworzenia plików uwierzytelniania** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A04]

1. <span data-ttu-id="1c7e1-138">Witaj **stan Creatation nazwy głównej usługi** zostanie wyświetlone okno dialogowe i po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Okno dialogowe Stan Creatation nazwy głównej usługi][A05]

1. <span data-ttu-id="1c7e1-140">Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

1. <span data-ttu-id="1c7e1-142">Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="1c7e1-144">Podpisywanie poza konta platformy Azure po zalogowaniu automatycznie</span><span class="sxs-lookup"><span data-stu-id="1c7e1-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="1c7e1-145">Po skonfigurowaniu hello kroki opisane w poprzedniej sekcji hello hello Azure Toolkit spowoduje automatyczne zalogowanie do konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="1c7e1-146">Jednak toosign poza konta platformy Azure i uniemożliwić hello Azure Toolkit podczas logowania automatycznie, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="1c7e1-147">W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu Eclipse Azure wylogowaniu][L01]

1. <span data-ttu-id="1c7e1-149">Gdy hello **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Wyloguj się okno dialogowe][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="1c7e1-151">Logowanie do konta platformy Azure automatycznie przy użyciu pliku poświadczeń, które zostały już utworzone</span><span class="sxs-lookup"><span data-stu-id="1c7e1-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="1c7e1-152">Jeśli możesz wylogować się z platformy Azure, korzystając z programu Eclipse, konieczne będzie tooreconfigure hello Azure zestawu narzędzi dla programu Eclipse toouse pliku poświadczeń, które zostały utworzone, aby automatycznie mógł zalogować się na konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="1c7e1-153">Hello poniższe kroki objaśniają Konfigurowanie hello Azure Toolkit toouse istniejący plik poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="1c7e1-154">Otwórz projekt z Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="1c7e1-155">Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu Eclipse Azure w celu logowania się][A01]

1. <span data-ttu-id="1c7e1-157">Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Zaloguj się okno dialogowe][A02]

1. <span data-ttu-id="1c7e1-159">Gdy hello **wybierz plik uwierzytelniony** zostanie wyświetlone okno dialogowe, wybierz plik poświadczeń, który został utworzony wcześniej, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Zaloguj się okno dialogowe][A08]

1. <span data-ttu-id="1c7e1-161">Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

1. <span data-ttu-id="1c7e1-163">Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c7e1-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="see-also"></a><span data-ttu-id="1c7e1-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1c7e1-165">See Also</span></span>
<span data-ttu-id="1c7e1-166">Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="1c7e1-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="1c7e1-167">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1c7e1-168">[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1c7e1-169">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1c7e1-170">*Zaloguj się w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="1c7e1-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="1c7e1-171">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="1c7e1-172">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="1c7e1-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1c7e1-173">[Nowości w hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1c7e1-174">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1c7e1-175">[Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1c7e1-176">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1c7e1-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="1c7e1-177">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="1c7e1-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

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
