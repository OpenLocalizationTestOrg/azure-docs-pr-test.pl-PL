---
title: "Usługi Azure Data Lake Tools: Użycia usługi Azure Data Lake Tools dla programu Visual Studio Code | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak narzędzia toouse Azure Data Lake Tools dla Visual Studio Code toocreate, testowanie i uruchamianie skryptów U-SQL. "
Keywords: "VScode, usługi Azure Data Lake Tools, lokalnego uruchamiania lokalnego debugowania, debugowania lokalnego pliku magazynu w wersji zapoznawczej, Przekaż toostorage ścieżki"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="fa7f1-104">Użyj usługi Azure Data Lake Tools dla programu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="fa7f1-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="fa7f1-105">Dowiedz się, jak narzędzia toouse Azure Data Lake Tools dla toocreate programu Visual Studio (kod VS), testowanie i uruchamianie skryptów U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="fa7f1-106">informacje Hello jest również objęte powitania po wideo:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="fa7f1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa7f1-107">Prerequisites</span></span>

<span data-ttu-id="fa7f1-108">Narzędzia Data Lake Tools można zainstalować na powitania platformach obsługiwanych przez kod programu VS.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="fa7f1-109">Hello obsługiwane platformy to Windows, Linux lub MacOS.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="fa7f1-110">Witaj na różnych platformach mają hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="fa7f1-111">Windows</span><span class="sxs-lookup"><span data-stu-id="fa7f1-111">Windows</span></span>

    - <span data-ttu-id="fa7f1-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="fa7f1-113">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="fa7f1-114">Dodaj hello java.exe ścieżka toohello środowiska zmiennej ścieżki systemu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="fa7f1-115">Instrukcje konfiguracji można znaleźć [jak ustawić lub zmienić zmiennej systemowej Path hello?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="fa7f1-116">Ścieżka Hello jest tooC:\Program Files\Java\jdk1.8.0_77\jre\bin podobne.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="fa7f1-117">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="fa7f1-118">Linux (zalecamy Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="fa7f1-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="fa7f1-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="fa7f1-120">tooinstall hello kodu, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="fa7f1-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="fa7f1-122">Pakiet deb hello tooupdate źródło, wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="fa7f1-123">tooinstall Mono, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="fa7f1-124">Mono 4.6 nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="fa7f1-125">Całkowicie przed zainstalowaniem 4.2.x, należy odinstalować wersję 4.6.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="fa7f1-126">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="fa7f1-127">Aby uzyskać instrukcje instalacji, zobacz hello [Linux 64-bitowe instrukcje instalacji Java]( https://java.com/en/download/help/linux_x64_install.xml) strony.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="fa7f1-128">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="fa7f1-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="fa7f1-129">MacOS</span></span>

    - <span data-ttu-id="fa7f1-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="fa7f1-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="fa7f1-132">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="fa7f1-133">Aby uzyskać instrukcje instalacji, zobacz hello [Linux 64-bitowe instrukcje instalacji Java](https://java.com/en/download/help/mac_install.xml) strony.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="fa7f1-134">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="fa7f1-135">Instalowania narzędzi Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="fa7f1-135">Install Data Lake Tools</span></span>

<span data-ttu-id="fa7f1-136">Po zainstalowaniu wymagań wstępnych hello można zainstalować narzędzi Data Lake Tools dla programu VS kodu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="fa7f1-137">**tooinstall narzędzi Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="fa7f1-138">Otwórz kod programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="fa7f1-139">Wybierz kombinację klawiszy Ctrl + P, a następnie wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="fa7f1-140">Można wyświetlić listę rozszerzeń kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="fa7f1-141">Jeden z nich jest **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="fa7f1-142">Wybierz **zainstalować** dalej zbyt**Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="fa7f1-143">Po kilku sekundach hello **zainstalować** przycisk zmiany zbyt**Załaduj ponownie**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="fa7f1-144">Wybierz **Załaduj ponownie** tooactivate hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="fa7f1-145">Wybierz **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="fa7f1-146">Azure Data Lake Tools można zobaczyć w hello **rozszerzenia** okienka.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="fa7f1-147">![Narzędzia Data Lake Tools dla okienka rozszerzenia kodu programu Visual Studio](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="fa7f1-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="fa7f1-148">Aktywacja usługi Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="fa7f1-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="fa7f1-149">Utwórz nowy plik .usql lub Otwórz istniejący .usql tooactivate hello rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="fa7f1-150">Połącz tooAzure</span><span class="sxs-lookup"><span data-stu-id="fa7f1-150">Connect tooAzure</span></span>

<span data-ttu-id="fa7f1-151">Można było skompilować i uruchomić skrypty U-SQL w usługi Data Lake Analytics, należy połączyć tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="fa7f1-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="fa7f1-153">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="fa7f1-154">Wprowadź **ADL: logowania**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="fa7f1-155">informacje logowania Hello jest wyświetlana w hello **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="fa7f1-156">![Data Lake Tools dla Visual Studio Code polecenia palety](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![narzędzi Data Lake Tools dla Visual Studio Code informacji o logowaniu urządzenia](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="fa7f1-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="fa7f1-157">Wybierz kombinację klawiszy Ctrl + kliknięcie hello adres URL logowania: https://aka.ms/devicelogin tooopen hello logowania strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="fa7f1-158">Wprowadź kod hello **G567LX42V** w polu tekstowym hello, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code logowania Wklej kod](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="fa7f1-160">Wykonaj toosign instrukcje hello w z hello strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="fa7f1-161">Po nawiązaniu połączenia nazwa konta usługi Azure zostanie wyświetlony na pasku stanu hello w hello lewym dolnym rogu hello **kodzie VS** okna.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="fa7f1-162">Jeśli konto ma dwa składniki włączone, zalecane jest użycie z telefonu uwierzytelniania, a nie za pomocą numeru PIN.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="fa7f1-163">toosign, wprowadź polecenie hello **ADL: wylogowania**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="fa7f1-164">Lista kont usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fa7f1-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="fa7f1-165">połączenie hello tootest, Pobierz listę kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="fa7f1-166">**konta usługi Data Lake Analytics hello toolist w ramach Twojej subskrypcji platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="fa7f1-167">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="fa7f1-168">Wprowadź **ADL: listy kont**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="fa7f1-169">Witaj konta są wyświetlane w hello **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="fa7f1-170">Otwórz hello przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="fa7f1-170">Open hello sample script</span></span>
<span data-ttu-id="fa7f1-171">Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: Otwórz przykładowy skrypt**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="fa7f1-172">Zostanie otwarte inne wystąpienie tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-172">This opens another instance of this sample.</span></span> <span data-ttu-id="fa7f1-173">Można również edytować, skonfigurować i przesłać skrypt w tym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="fa7f1-174">Praca z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="fa7f1-174">Work with U-SQL</span></span>

<span data-ttu-id="fa7f1-175">Języku U-SQL należy otworzyć plików U-SQL lub toowork folderu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="fa7f1-176">**tooopen folderu projektu U-SQL**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="fa7f1-177">Visual Studio Code, zaznacz hello **pliku** menu, a następnie wybierz **Otwórz Folder**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="fa7f1-178">Określ folder, a następnie wybierz **wybierz Folder**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="fa7f1-179">Wybierz hello **pliku** menu, a następnie wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="fa7f1-180">Plik bez tytułu-1 jest dodawany toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="fa7f1-181">Wprowadź powitania po kod do pliku hello bez tytułu 1:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-181">Enter hello following code into hello Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="fa7f1-182">Witaj skrypt tworzy plik departments.csv z niektórych danych zawartych w folderze/Output hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="fa7f1-183">Zapisz plik hello jako **myUSQL.usql** w hello otworzyć folderu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="fa7f1-184">Plik konfiguracji adltools_settings.json jest także dodawane toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="fa7f1-185">Otwórz i skonfiguruj adltools_settings.json hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="fa7f1-186">Konto: Konta Data Lake Analytics w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="fa7f1-187">Baza danych: Baza danych przy użyciu tego konta.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-187">Database: A database under your account.</span></span> <span data-ttu-id="fa7f1-188">Domyślnie Hello **wzorca**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-188">hello default is **master**.</span></span>
    - <span data-ttu-id="fa7f1-189">Schemat: Schemat w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-189">Schema: A schema under your database.</span></span> <span data-ttu-id="fa7f1-190">Domyślnie Hello **dbo**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="fa7f1-191">Ustawienia opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-191">Optional settings:</span></span>
        - <span data-ttu-id="fa7f1-192">Priorytet: hello priorytet jest zakres od 1 too1000 z 1 hello najwyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="fa7f1-193">Witaj, wartość domyślna to **1000**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="fa7f1-194">Równoległość: zakres równoległości hello jest z 1 too150.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="fa7f1-195">Witaj, wartość domyślna to hello równoległości maksymalny dozwolony na koncie usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="fa7f1-196">Jeśli ustawienia hello są nieprawidłowe, wartości domyślne hello są używane.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code pliku konfiguracji](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="fa7f1-198">Obliczeniowe, to konto usługi Data Lake Analytics potrzebne toocompile i uruchamianie zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="fa7f1-199">Należy skonfigurować konto komputera hello przed możesz skompilować i uruchomić zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="fa7f1-200">Po zapisaniu konfiguracji hello hello konta, bazę danych i schemat informacje są wyświetlane na pasku stanu hello w hello lewym dolnym rogu hello odpowiedni plik .usql.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="fa7f1-201">W porównaniu tooopening plik, po otwarciu folderu, które można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="fa7f1-202">Użyj pliku CodeBehind.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-202">Use a code-behind file.</span></span> <span data-ttu-id="fa7f1-203">W trybie pojedynczego pliku hello związane z kodem nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="fa7f1-204">Przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-204">Use a configuration file.</span></span> <span data-ttu-id="fa7f1-205">Po otwarciu folderu hello skryptów w hello folder roboczy udostępniać pojedynczym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="fa7f1-206">Witaj skryptu U-SQL kompiluje zdalnie za pośrednictwem hello usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="fa7f1-207">Podczas wystawiania hello **skompilować** polecenia, konto usługi Data Lake Analytics tooyour jest wiadomości powitania skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="fa7f1-208">Później Visual Studio Code odbiera hello wynik kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="fa7f1-209">Powodu toohello kompilacji zdalnej Visual Studio Code wymaga, wyświetlić listę informacji hello tooconnect tooyour konto usługi Data Lake Analytics hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="fa7f1-210">**skrypt toocompile U-SQL**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="fa7f1-211">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="fa7f1-212">Wprowadź **ADL: kompilowania skryptu**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="fa7f1-213">Witaj kompilacji wyniki są wyświetlane na powitania **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="fa7f1-214">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: kompilowania skryptu** zadania toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="fa7f1-215">Wynik kompilacji Hello jest wyświetlana w hello **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="fa7f1-216">**skrypt toosubmit U-SQL**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="fa7f1-217">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="fa7f1-218">Wprowadź **ADL: przesłać zadania**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="fa7f1-219">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="fa7f1-220">Po przesłaniu zadania skryptu U-SQL hello przesyłanie dzienników pojawia się w hello **dane wyjściowe** okna w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="fa7f1-221">Jeśli hello przesyłanie zakończy się pomyślnie, również zostanie wyświetlony adres URL zadania hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="fa7f1-222">Adres URL zadania hello można otworzyć w stan zadania w czasie rzeczywistym hello tootrack przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="fa7f1-223">dane wyjściowe hello tooenable hello szczegóły zadania, ustaw **jobInformationOutputPath** w hello **vs kod hello u-sql_settings.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="fa7f1-224">Przy użyciu pliku CodeBehind</span><span class="sxs-lookup"><span data-stu-id="fa7f1-224">Use a code-behind file</span></span>

<span data-ttu-id="fa7f1-225">Plik CodeBehind jest pliku C# skojarzonego z jednego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="fa7f1-226">W pliku CodeBehind hello można zdefiniować tooUDO skryptu w wersji dedykowanej, UDA, UDT i funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="fa7f1-227">Witaj UDO, UDA UDT i funkcji zdefiniowanej przez użytkownika można bezpośrednio w skrypcie hello bez rejestrowania najpierw hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="fa7f1-228">Hello pliku CodeBehind jest umieszczany w hello sam folder jako jego komunikacji równorzędnej pliku skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="fa7f1-229">Jeśli skrypt hello nosi nazwę xxx.usql, kodem hello nosi nazwę jako xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="fa7f1-230">Jeśli usuniesz ręcznie pliku CodeBehind hello, hello CodeBehind funkcja jest wyłączona dla jego skojarzony skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="fa7f1-231">Aby uzyskać więcej informacji na temat pisania kodu klienta dla skryptu U-SQL, zobacz [pisania i przy użyciu niestandardowego kodu w języku U-SQL: funkcje zdefiniowane przez użytkownika]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="fa7f1-232">toosupport związane z kodem, możesz otworzyć folderu roboczego.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="fa7f1-233">**toogenerate pliku CodeBehind**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="fa7f1-234">Otwórz plik źródłowy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-234">Open a source file.</span></span> 
2. <span data-ttu-id="fa7f1-235">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="fa7f1-236">Wprowadź **ADL: generowanie kodu**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="fa7f1-237">Plik CodeBehind jest tworzony w hello sam folder.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="fa7f1-238">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: generowanie kodu za**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="fa7f1-239">toocompile i przesłać skrypt U-SQL przy użyciu pliku CodeBehind jest hello tak samo jak plik skryptu, autonomiczny hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="fa7f1-240">Witaj następujące dwa zrzuty ekranu pokazują plik CodeBehind i jego skojarzony plik skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Plik skryptu narzędzi Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="fa7f1-243">Korzystanie z zestawów</span><span class="sxs-lookup"><span data-stu-id="fa7f1-243">Use assemblies</span></span>

<span data-ttu-id="fa7f1-244">Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="fa7f1-245">Korzystanie z narzędzi Data Lake Tools tooregister kod niestandardowy zestawów, w katalogu Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="fa7f1-246">**tooregister zestawu**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-246">**tooregister an assembly**</span></span>

<span data-ttu-id="fa7f1-247">Można zarejestrować zestawu hello za pośrednictwem hello **ADL: Zarejestruj zestawu** lub **ADL: Zarejestruj zestawu za pomocą konfiguracji** poleceń.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="fa7f1-248">**tooregister za pośrednictwem hello ADL: polecenie zarejestrować zestawu**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="fa7f1-249">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="fa7f1-250">Wprowadź **ADL: zarejestrować zestawu**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="fa7f1-251">Określ ścieżkę zestawu lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="fa7f1-252">Wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="fa7f1-253">Wybierz bazę danych.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-253">Select a database.</span></span>

<span data-ttu-id="fa7f1-254">Wyniki: hello portal jest otwarty w przeglądarce i wyświetla procesu rejestracji zestawu hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="fa7f1-255">Inny hello tootrigger wygodny sposób **ADL: Zarejestruj zestawu** polecenia to plik dll hello tooright kliknij w Eksploratorze plików.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="fa7f1-256">**tooregister jednak hello ADL: Zarejestruj zestawu za pomocą polecenia konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="fa7f1-257">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="fa7f1-258">Wprowadź **ADL: zarejestrować zestawu za pomocą konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="fa7f1-259">Określ ścieżkę zestawu lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="fa7f1-260">Plik JSON Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-260">hello JSON file is displayed.</span></span> <span data-ttu-id="fa7f1-261">Przejrzyj i Edytuj zależności zestawu hello i parametry zasobu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="fa7f1-262">Instrukcje są wyświetlane w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="fa7f1-263">tooproceed toohello rejestrowania zestawów, Zapisz plik JSON hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="fa7f1-265">Zależności zestawu: automatycznie wykrywa Azure Data Lake Tools czy hello DLL ma zależności.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="fa7f1-266">zależności Hello są wyświetlane w pliku JSON powitania po ich wykryciu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="fa7f1-267">Zasoby: Można przekazać biblioteki DLL zasobów (na przykład txt, .png i .csv) jako część hello zestawu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="fa7f1-268">Inny sposób tootrigger hello **ADL: Zarejestruj zestawu za pomocą konfiguracji** polecenia to plik dll hello tooright kliknij w Eksploratorze plików.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="fa7f1-269">Pokazuje Hello następującego kodu U-SQL, jak toocall zestawu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="fa7f1-270">W przykładzie hello jest nazwą zestawu hello *testu*.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-270">In hello sample, hello assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="fa7f1-271">Wykaz usługi Data Lake Analytics hello dostępu</span><span class="sxs-lookup"><span data-stu-id="fa7f1-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="fa7f1-272">Po podłączeniu tooAzure służy hello następujące kroki tooaccess hello U-SQL katalogu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="fa7f1-273">**tooaccess hello Azure Data Lake Analytics metadanych**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="fa7f1-274">Wybierz kombinację klawiszy Ctrl + Shift + P, a następnie wprowadź **ADL: listy tabel**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="fa7f1-275">Wybierz jedno z kont usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="fa7f1-276">Wybierz jedną z bazy danych usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="fa7f1-277">Wybierz jedną z hello schematów.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-277">Select one of hello schemas.</span></span> <span data-ttu-id="fa7f1-278">Widać hello listy tabel.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="fa7f1-279">Widok Data Lake Analytics zadania</span><span class="sxs-lookup"><span data-stu-id="fa7f1-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="fa7f1-280">**zadania usługi Data Lake Analytics tooview**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="fa7f1-281">Otwórz hello polecenia palety (Ctrl + Shift + P) i wybierz **ADL: Pokaż zadania**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="fa7f1-282">Wybierz usługi Data Lake Analytics lub konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="fa7f1-283">Poczekaj na listę zadań hello hello tooappear konta.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="fa7f1-284">Wybierz zadanie z listy zadań, narzędzi Data Lake Tools otwiera hello szczegóły zadania w portalu Azure hello i wyświetla plik informacji o zadaniu hello w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="fa7f1-286">Integracja magazynu usługi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fa7f1-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="fa7f1-287">Można użyć poleceń usługi Azure Data Lake Storage, aby:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="fa7f1-288">Przeglądaj hello Azure Data Lake Storage zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="fa7f1-289">Plik usługi Azure Data Lake Storage hello podglądu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="fa7f1-290">Przekaż hello pliku bezpośrednio tooAzure usługi Data Lake Storage w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="fa7f1-291">Ścieżki do magazynu hello listy</span><span class="sxs-lookup"><span data-stu-id="fa7f1-291">List hello storage path</span></span> 
<span data-ttu-id="fa7f1-292">Można wyświetlić listę hello ścieżki do magazynu za pośrednictwem palety polecenia hello lub kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="fa7f1-293">**ścieżki do magazynu hello toolist za pośrednictwem hello polecenia palety**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="fa7f1-294">Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: ścieżka magazynu listy**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="fa7f1-296">Wybierz użytkownika preferowany sposób wyświetlania list hello ścieżki do magazynu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="fa7f1-297">Używa tego przejścia **wprowadź ścieżkę** jako przykład.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-297">This passage uses **Enter a path** as an example.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code ścieżki do magazynu hello toolist jednokierunkowej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="fa7f1-299">VS kod chroni hello odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="fa7f1-300">Na przykład: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="fa7f1-301">Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy hello z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="fa7f1-302">Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="fa7f1-303">Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz więcej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="fa7f1-305">Wybierz **więcej** toolist więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="fa7f1-307">Wprowadź ścieżkę do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-307">Enter an Azure storage path.</span></span> <span data-ttu-id="fa7f1-308">Na przykład/output.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-308">For example, /output.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code Wprowadź ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="fa7f1-310">Wyniki: hello palety polecenie wyświetla informacje o ścieżce hello na podstawie wpisów.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code lista wyników ścieżki magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="fa7f1-312">Ścieżka względna toolist hello jest za pośrednictwem hello wygodny sposób kliknij prawym przyciskiem myszy menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="fa7f1-313">**Kliknij prawym przyciskiem myszy toolist hello ścieżki do magazynu za pośrednictwem**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="fa7f1-314">Kliknij prawym przyciskiem myszy tooselect ciąg ścieżki hello **ścieżki do magazynu listy**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="fa7f1-316">Wybrana ścieżka względna Hello jest wyświetlana w hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-316">hello selected relative path appears in hello command palette.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybrane ścieżki względnej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="fa7f1-318">Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="fa7f1-320">Wyniki: hello palety polecenie wyświetla listę hello folderów i plików dla bieżącej ścieżki hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy z bieżącej ścieżki hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="fa7f1-322">Plik magazynu hello podglądu</span><span class="sxs-lookup"><span data-stu-id="fa7f1-322">Preview hello storage file</span></span>
<span data-ttu-id="fa7f1-323">Można wyświetlić podgląd pliku magazynu hello za pośrednictwem palety polecenia hello lub kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="fa7f1-324">**Plik magazynu hello toopreview za pomocą hello polecenia palety**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="fa7f1-325">Otwórz hello polecenia palety (Ctrl + Shift + P), a następnie wprowadź **ADL: Podgląd pliku magazynu**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wyświetlić podgląd pliku magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="fa7f1-327">Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy kont](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="fa7f1-329">Wybierz **więcej** toolist więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="fa7f1-331">Wprowadź ścieżkę do magazynu Azure lub pliku.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="fa7f1-332">Na przykład /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-332">For example, /output/SearchLog.txt.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę do magazynu i](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="fa7f1-334">Wyniki: hello palety polecenie wyświetla informacje o ścieżce hello na podstawie wpisów.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="fa7f1-336">**Kliknij prawym przyciskiem myszy toolist hello ścieżki do magazynu za pośrednictwem**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="fa7f1-337">toopreview pliku, ścieżka pliku powitania kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-337">toopreview a file, right-click hello file path.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="fa7f1-339">Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="fa7f1-341">Wyniki: Kod VS Wyświetla hello Podgląd wyników hello pliku.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="fa7f1-343">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="fa7f1-343">Upload a file</span></span> 

<span data-ttu-id="fa7f1-344">Możesz przekazać pliki, wprowadzając polecenia hello **ADL: Przekaż plik** lub **ADL: Przekaż plik przy użyciu konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="fa7f1-345">**pliki tooupload jednak hello ADL: Przekaż plik — polecenie**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="fa7f1-346">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety lub kliknij prawym przyciskiem myszy hello edytora skryptów, a następnie wprowadź **Przekaż plik**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="fa7f1-347">Witaj tooupload pliku, wprowadź ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-347">tooupload hello file, enter a local path.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę lokalną](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="fa7f1-349">Wybierz jeden z sposobów hello ścieżki do magazynu hello listy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="fa7f1-350">Używa tego przejścia **wprowadź ścieżkę** jako przykład.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-350">This passage uses **Enter a path** as an example.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="fa7f1-352">VS kod chroni hello odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="fa7f1-353">Na przykład: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="fa7f1-354">Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy hello z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="fa7f1-355">Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="fa7f1-356">Wybierz konto z hello ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code magazynu, kliknij prawym przyciskiem myszy](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="fa7f1-358">Wprowadź ścieżkę do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-358">Enter an Azure storage path.</span></span> <span data-ttu-id="fa7f1-359">Na przykład: / output.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="fa7f1-360">Znajdź ścieżki magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-360">Find your Azure storage path.</span></span> <span data-ttu-id="fa7f1-361">Wybierz **Wybierz bieżący folder**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-361">Select **Choose current folder**.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz folder](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="fa7f1-363">Wyniki: hello **dane wyjściowe** okno wyświetla stan przekazywania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="fa7f1-365">**pliki tooupload jednak hello ADL: Przekaż plik za pomocą polecenia konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="fa7f1-366">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety lub kliknij prawym przyciskiem myszy hello edytora skryptów, a następnie wprowadź **Przekaż plik przy użyciu konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="fa7f1-367">VS kod przedstawia plik JSON.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="fa7f1-368">Można wprowadzić ścieżki do plików i przekazywania wielu plików na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="fa7f1-369">Instrukcje są wyświetlane w hello **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="fa7f1-370">tooproceed tooupload hello plik, Zapisz plik JSON hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Ścieżka pliku narzędzia Data Lake Tools dla Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="fa7f1-372">Wyniki: hello **dane wyjściowe** okno wyświetla stan przekazywania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="fa7f1-374">Innym tooupload sposób toostorage pliku jest za pośrednictwem hello menu Pełna ścieżka pliku hello lub ścieżkę względną hello plik w Edytorze skryptów powitania kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="fa7f1-375">Wprowadź ścieżkę do pliku lokalnego hello, a następnie wybierz konto hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="fa7f1-376">Witaj **dane wyjściowe** okno wyświetla stan przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="fa7f1-377">Eksplorator usługi Storage Azure Otwórz</span><span class="sxs-lookup"><span data-stu-id="fa7f1-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="fa7f1-378">Możesz otworzyć **Eksploratora usługi Storage Azure** wprowadzając polecenie hello **ADL: Otwórz Eksploratora usługi sieci Web Azure Storage** lub wybierając z menu kontekstowego powitania kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="fa7f1-379">**tooopen Eksploratora usługi Storage platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="fa7f1-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="fa7f1-380">Wybierz kombinację klawiszy Ctrl + Shift + P tooopen hello polecenia palety.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="fa7f1-381">Wprowadź **Otwórz Eksploratora usługi Storage Azure Web** lub kliknij prawym przyciskiem myszy na ścieżkę względną lub pełną ścieżkę hello na powitania edytora skryptów, a następnie wybierz **Otwórz Eksploratora usługi Storage Azure Web**.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="fa7f1-382">Wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="fa7f1-383">Narzędzia Data Lake Tools otwiera ścieżki do magazynu Azure hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="fa7f1-384">Plik hello ścieżkę i Podgląd hello hello sieci Web można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="fa7f1-385">Przebieg lokalny i lokalny debugowania dla systemu Windows użytkownicy</span><span class="sxs-lookup"><span data-stu-id="fa7f1-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="fa7f1-386">Uruchamiania lokalnego skryptu U-SQL sprawdza danych lokalnych i weryfikuje skrypt lokalnie, zanim kodu jest opublikowane tooData Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="fa7f1-387">Umożliwia funkcji debugowania lokalnego Hello możesz toocomplete hello następujące zadania, zanim Twój kod przesłane tooData Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="fa7f1-388">Debugowanie programu C# związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="fa7f1-389">Przejrzyj kroki hello kodu.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-389">Step through hello code.</span></span> 
- <span data-ttu-id="fa7f1-390">Sprawdź poprawność skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-390">Validate your script locally.</span></span>

<span data-ttu-id="fa7f1-391">Aby uzyskać instrukcje dotyczące przebiegu lokalnego i debugowania lokalnego, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="fa7f1-392">Dodatkowe funkcje</span><span class="sxs-lookup"><span data-stu-id="fa7f1-392">Additional features</span></span>

<span data-ttu-id="fa7f1-393">Narzędzia Data Lake Tools dla programu VS kodu obsługuje hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="fa7f1-394">Funkcja automatycznego uzupełniania IntelliSense: sugestie są wyświetlane w wyskakujące wokół elementów, takich jak słowa kluczowe, metod i zmiennych.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="fa7f1-395">Inne ikony reprezentują różne typy obiektów hello:</span><span class="sxs-lookup"><span data-stu-id="fa7f1-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="fa7f1-396">Scala — typ danych</span><span class="sxs-lookup"><span data-stu-id="fa7f1-396">Scala data type</span></span>
    - <span data-ttu-id="fa7f1-397">Typ danych złożonych</span><span class="sxs-lookup"><span data-stu-id="fa7f1-397">Complex data type</span></span>
    - <span data-ttu-id="fa7f1-398">Wbudowanych typów</span><span class="sxs-lookup"><span data-stu-id="fa7f1-398">Built-in UDTs</span></span>
    - <span data-ttu-id="fa7f1-399">Klasy i kolekcji .NET</span><span class="sxs-lookup"><span data-stu-id="fa7f1-399">.NET collection and classes</span></span>
    - <span data-ttu-id="fa7f1-400">Wyrażenia języka C#</span><span class="sxs-lookup"><span data-stu-id="fa7f1-400">C# expressions</span></span>
    - <span data-ttu-id="fa7f1-401">Funkcje UDF wbudowane C#, obiektów udo i UDAAGs</span><span class="sxs-lookup"><span data-stu-id="fa7f1-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="fa7f1-402">Funkcje języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="fa7f1-402">U-SQL functions</span></span>
    - <span data-ttu-id="fa7f1-403">Funkcją okienkową U-SQL</span><span class="sxs-lookup"><span data-stu-id="fa7f1-403">U-SQL windowing function</span></span>
 
    ![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="fa7f1-405">Funkcja automatycznego uzupełniania w metadanych usługi Data Lake Analytics IntelliSense: narzędzi Data Lake Tools pobiera informacje metadanych usługi Data Lake Analytics hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="fa7f1-406">funkcja IntelliSense Hello automatycznie wypełni obiektów, w tym hello bazy danych, schematu, tabeli, widoku, funkcji zwracającej tabelę, procedury i zestawów języka C# z hello metadanych usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Narzędzia Data Lake Tools dla programu Visual Studio kodu IntelliSense metadanych](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="fa7f1-408">Znacznik błąd IntelliSense: narzędzi Data Lake Tools podkreśla hello edytowanie błędy U-SQL i C#.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="fa7f1-409">Najważniejsze funkcje Składnia: narzędzi Data Lake Tools używa elementów toodifferentiate różne kolory, takich jak zmienne, słowa kluczowe, typ danych i funkcji.</span><span class="sxs-lookup"><span data-stu-id="fa7f1-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Zawiera opis narzędzi Data Lake Tools dla Visual Studio Code składni](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="fa7f1-411">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa7f1-411">Next steps</span></span>

- <span data-ttu-id="fa7f1-412">Dla przebiegu lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="fa7f1-413">Aby — wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="fa7f1-414">Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="fa7f1-415">Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="fa7f1-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



