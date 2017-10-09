---
title: "aaaSign w instrukcje dotyczące hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosign w tooMicrosoft Azure przy użyciu hello Azure Toolkit for IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="d87e8-103">Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d87e8-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="d87e8-104">Hello Azure Toolkit for IntelliJ udostępnia dwie metody logowania tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d87e8-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="d87e8-105">**Interakcyjne**: Wprowadź każdym logowaniu poświadczenia platformy Azure w tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d87e8-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="d87e8-106">**Automatyczne**: Utwórz plik poświadczeń w tooyour konto platformy Azure można tooautomatically logowania.</span><span class="sxs-lookup"><span data-stu-id="d87e8-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="d87e8-107">Witaj poniższych sekcjach opisano sposób toouse każdej metody.</span><span class="sxs-lookup"><span data-stu-id="d87e8-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="d87e8-108">Zaloguj się interaktywnie tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d87e8-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="d87e8-109">toosign w tooAzure ręcznie wprowadzić poświadczenia platformy Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d87e8-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="d87e8-110">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="d87e8-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="d87e8-111">Kliknij przycisk **narzędzia**, punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Witaj polecenia IntelliJ Azure logowania][I01]

3. <span data-ttu-id="d87e8-113">W hello **Azure logowania** wybierz **Interactive**, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello Azure logowania okna z Interactive wybrane][I02]

4. <span data-ttu-id="d87e8-115">W hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![okno dialogowe logowania Azure Hello][I03]

5. <span data-ttu-id="d87e8-117">W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje Hello — okno dialogowe][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="d87e8-119">Wylogować się z konta platformy Azure, po zarejestrowaniu trybie interakcyjnym</span><span class="sxs-lookup"><span data-stu-id="d87e8-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="d87e8-120">Po skonfigurowaniu konta przy użyciu hello w poprzednich krokach, użytkownik będzie automatyczne wylogowanie z konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="d87e8-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="d87e8-121">Jednak jeśli chcesz toosign poza konta platformy Azure *bez* ponowne uruchomienie IntelliJ IDEA hello następujące.</span><span class="sxs-lookup"><span data-stu-id="d87e8-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="d87e8-122">W IntelliJ IDEA, na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Witaj IntelliJ Azure Wyloguj polecenia][L01]

2. <span data-ttu-id="d87e8-124">W hello **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure Wyloguj okno potwierdzenia][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="d87e8-126">Zaloguj się automatycznie tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d87e8-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="d87e8-127">Ta sekcja przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi.</span><span class="sxs-lookup"><span data-stu-id="d87e8-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="d87e8-128">Po zakończeniu tego procesu Eclipse używa hello poświadczenia pliku tooautomatically logowania się, że w każdym tooAzure czasu Otwórz projekt.</span><span class="sxs-lookup"><span data-stu-id="d87e8-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="d87e8-129">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="d87e8-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="d87e8-130">Na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Witaj polecenia IntelliJ Azure logowania][A01]

3. <span data-ttu-id="d87e8-132">W hello **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Hello Azure logowania okna z automatycznego wybrane][A02]

4. <span data-ttu-id="d87e8-134">W hello **dialogowym logowania do usługi Azure** okna, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![okno dialogowe logowania Azure Hello][A03]

5. <span data-ttu-id="d87e8-136">W hello **tworzenia plików uwierzytelniania** okna, wybierz hello subskrypcje mają toouse, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Witaj okna Tworzenie plików uwierzytelniania][A04]

6. <span data-ttu-id="d87e8-138">W hello **stan tworzenia nazwy głównej usługi** okno dialogowe po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Witaj okno dialogowe Stan tworzenia nazwy głównej usługi][A05]

7. <span data-ttu-id="d87e8-140">W hello **Azure logowania** okna, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Okno dialogowe logowania do platformy Azure][A06]

8. <span data-ttu-id="d87e8-142">W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje Hello — okno dialogowe][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="d87e8-144">Wylogować się z konta platformy Azure po zalogowaniu się automatycznie</span><span class="sxs-lookup"><span data-stu-id="d87e8-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="d87e8-145">Po skonfigurowaniu konta przy użyciu poprzednich krokach hello, hello Azure Toolkit automatycznie loguje się użytkownik tooyour każdorazowo po ponownym uruchomieniu IntelliJ IDEA konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d87e8-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="d87e8-146">Jednak toosign poza konta platformy Azure i zapobiec hello Azure Toolkit z automatycznego rejestrowania, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d87e8-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="d87e8-147">W IntelliJ IDEA, na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Witaj IntelliJ Azure Wyloguj polecenia][L01]

2. <span data-ttu-id="d87e8-149">W hello **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure Wyloguj okno potwierdzenia][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="d87e8-151">Zaloguj się tooyour konta Azure automatycznie przy użyciu istniejącego pliku poświadczeń</span><span class="sxs-lookup"><span data-stu-id="d87e8-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="d87e8-152">Jeśli możesz wylogować się z konta platformy Azure, korzystając z IntelliJ IDEA, należy użyć znaku tooautomatically pliku istniejących poświadczeń w toohello konta.</span><span class="sxs-lookup"><span data-stu-id="d87e8-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="d87e8-153">tooconfigure hello Azure zestawu narzędzi dla programu Eclipse toouse istniejący plik poświadczeń, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d87e8-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="d87e8-154">Otwórz projekt z IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="d87e8-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="d87e8-155">Na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Witaj polecenia IntelliJ Azure logowania][A01]

3. <span data-ttu-id="d87e8-157">W hello **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Hello Azure logowania okna z automatycznego wybrane][A02]

4. <span data-ttu-id="d87e8-159">W hello **wybierz plik Authentication** okno dialogowe, wybierz plik utworzonej wcześniej poświadczenia, a następnie kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Wybierz plik Authentication Hello — okno dialogowe][A08]

5. <span data-ttu-id="d87e8-161">W hello **Azure logowania** okna, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Hello Azure logowania okna z automatycznego wybrane][A06]

6. <span data-ttu-id="d87e8-163">W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d87e8-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Wybierz subskrypcje Hello — okno dialogowe][A07]

## <a name="next-steps"></a><span data-ttu-id="d87e8-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d87e8-165">Next steps</span></span>
<span data-ttu-id="d87e8-166">Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="d87e8-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="d87e8-167">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d87e8-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d87e8-168">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d87e8-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d87e8-169">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d87e8-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d87e8-170">[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d87e8-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d87e8-171">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d87e8-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="d87e8-172">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="d87e8-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d87e8-173">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d87e8-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d87e8-174">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d87e8-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d87e8-175">*Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ* (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="d87e8-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="d87e8-176">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d87e8-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="d87e8-177">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d87e8-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

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
