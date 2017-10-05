---
title: "Usługi Azure Data Lake Tools: Użycia usługi Azure Data Lake Tools dla programu Visual Studio Code | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure Data Lake Tools dla Visual Studio Code umożliwia tworzenie, testowanie i uruchamianie skryptów U-SQL. "
Keywords: "VScode, usługi Azure Data Lake Tools, uruchamiania lokalnego debugowania, debugowania lokalnego pliku magazynu w wersji zapoznawczej, lokalnego przekazać do ścieżki do magazynu"
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="5251d-104">Użyj usługi Azure Data Lake Tools dla programu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5251d-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="5251d-105">Dowiedz się, jak używać usługi Azure Data Lake Tools dla programu Visual Studio (kod VS) do tworzenia, testowania i uruchamiać skrypty U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="5251d-106">Informacje są także omówione w poniższym klipie wideo:</span><span class="sxs-lookup"><span data-stu-id="5251d-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="5251d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5251d-107">Prerequisites</span></span>

<span data-ttu-id="5251d-108">Narzędzia Data Lake Tools można zainstalować na platformach obsługiwanych przez kod programu VS.</span><span class="sxs-lookup"><span data-stu-id="5251d-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="5251d-109">Obsługiwane platformy to Windows, Linux lub MacOS.</span><span class="sxs-lookup"><span data-stu-id="5251d-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="5251d-110">Różnych platform zostały spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="5251d-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="5251d-111">Windows</span><span class="sxs-lookup"><span data-stu-id="5251d-111">Windows</span></span>

    - <span data-ttu-id="5251d-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5251d-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5251d-113">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5251d-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5251d-114">Dodaj ścieżkę java.exe ścieżki zmiennej środowiskowej systemu.</span><span class="sxs-lookup"><span data-stu-id="5251d-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="5251d-115">Instrukcje konfiguracji można znaleźć [jak ustawić lub zmienić zmiennej systemowej Path?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="5251d-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="5251d-116">Ścieżka jest podobny do C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="5251d-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="5251d-117">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5251d-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="5251d-118">Linux (zalecamy Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="5251d-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="5251d-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5251d-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="5251d-120">Aby zainstalować kod, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5251d-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="5251d-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="5251d-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="5251d-122">Aby zaktualizować źródła pakietu deb, wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="5251d-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="5251d-123">Aby zainstalować Mono, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5251d-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="5251d-124">Mono 4.6 nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5251d-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="5251d-125">Całkowicie przed zainstalowaniem 4.2.x, należy odinstalować wersję 4.6.</span><span class="sxs-lookup"><span data-stu-id="5251d-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="5251d-126">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5251d-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5251d-127">Aby uzyskać instrukcje instalacji, zobacz [Linux 64-bitowe instrukcje instalacji Java]( https://java.com/en/download/help/linux_x64_install.xml) strony.</span><span class="sxs-lookup"><span data-stu-id="5251d-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="5251d-128">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5251d-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="5251d-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="5251d-129">MacOS</span></span>

    - <span data-ttu-id="5251d-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5251d-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5251d-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="5251d-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="5251d-132">[Aktualizacja wersji 8 środowiska uruchomieniowego języka Java SE 77 lub nowszym](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5251d-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5251d-133">Aby uzyskać instrukcje instalacji, zobacz [Linux 64-bitowe instrukcje instalacji Java](https://java.com/en/download/help/mac_install.xml) strony.</span><span class="sxs-lookup"><span data-stu-id="5251d-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="5251d-134">[Zestaw SDK programu .NET core 1.0.3 lub środowisko uruchomieniowe .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5251d-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="5251d-135">Instalowania narzędzi Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="5251d-135">Install Data Lake Tools</span></span>

<span data-ttu-id="5251d-136">Po zainstalowaniu wymagań wstępnych, można zainstalować narzędzi Data Lake Tools dla programu VS kodu.</span><span class="sxs-lookup"><span data-stu-id="5251d-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="5251d-137">**Aby zainstalować narzędzia Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="5251d-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="5251d-138">Otwórz kod programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5251d-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="5251d-139">Wybierz kombinację klawiszy Ctrl + P, a następnie wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5251d-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="5251d-140">Można wyświetlić listę rozszerzeń kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5251d-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="5251d-141">Jeden z nich jest **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="5251d-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="5251d-142">Wybierz **zainstalować** obok **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="5251d-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="5251d-143">Po kilku sekundach **zainstalować** przycisku zmienia się na **Załaduj ponownie**.</span><span class="sxs-lookup"><span data-stu-id="5251d-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="5251d-144">Wybierz **Załaduj ponownie** aktywować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="5251d-145">Wybierz **OK** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="5251d-145">Select **OK** to confirm.</span></span> <span data-ttu-id="5251d-146">Widać Azure Data Lake Tools w **rozszerzenia** okienka.</span><span class="sxs-lookup"><span data-stu-id="5251d-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="5251d-147">![Narzędzia Data Lake Tools dla okienka rozszerzenia kodu programu Visual Studio](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="5251d-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="5251d-148">Aktywacja usługi Azure Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="5251d-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="5251d-149">Utwórz nowy plik .usql lub Otwórz istniejący plik .usql aktywować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="5251d-150">Nawiązywanie połączenia z usługą Azure</span><span class="sxs-lookup"><span data-stu-id="5251d-150">Connect to Azure</span></span>

<span data-ttu-id="5251d-151">Można było skompilować i uruchomić skrypty U-SQL w usługi Data Lake Analytics, należy połączyć z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="5251d-152">**Do nawiązania połączenia platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="5251d-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="5251d-153">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="5251d-154">Wprowadź **ADL: logowania**.</span><span class="sxs-lookup"><span data-stu-id="5251d-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="5251d-155">Informacje logowania są wyświetlane w **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="5251d-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="5251d-156">![Data Lake Tools dla Visual Studio Code polecenia palety](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![narzędzi Data Lake Tools dla Visual Studio Code informacji o logowaniu urządzenia](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="5251d-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="5251d-157">Wybierz kombinację klawiszy Ctrl + kliknięcie na adres URL logowania: https://aka.ms/devicelogin aby otworzyć stronę logowania w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5251d-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="5251d-158">Wprowadź kod **G567LX42V** w polu tekstowym, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="5251d-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code logowania Wklej kod](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="5251d-160">Postępuj zgodnie z instrukcjami, aby zalogować się w stronę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5251d-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="5251d-161">Po nawiązaniu połączenia nazwa konta platformy Azure jest wyświetlana na pasku stanu, w lewym dolnym rogu **kodzie VS** okna.</span><span class="sxs-lookup"><span data-stu-id="5251d-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="5251d-162">Jeśli konto ma dwa składniki włączone, zalecane jest użycie z telefonu uwierzytelniania, a nie za pomocą numeru PIN.</span><span class="sxs-lookup"><span data-stu-id="5251d-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="5251d-163">Aby się wylogować, wprowadź polecenie **ADL: wylogowania**.</span><span class="sxs-lookup"><span data-stu-id="5251d-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="5251d-164">Lista kont usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5251d-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="5251d-165">Aby przetestować połączenie, wyświetlenie listy kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="5251d-166">**Aby wyświetlić listę kont usługi Data Lake Analytics w ramach Twojej subskrypcji platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="5251d-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="5251d-167">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="5251d-168">Wprowadź **ADL: listy kont**.</span><span class="sxs-lookup"><span data-stu-id="5251d-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="5251d-169">Konta są wyświetlane w **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="5251d-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="5251d-170">Otwórz przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5251d-170">Open the sample script</span></span>
<span data-ttu-id="5251d-171">Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: Otwórz przykładowy skrypt**.</span><span class="sxs-lookup"><span data-stu-id="5251d-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="5251d-172">Zostanie otwarte inne wystąpienie tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="5251d-172">This opens another instance of this sample.</span></span> <span data-ttu-id="5251d-173">Można również edytować, skonfigurować i przesłać skrypt w tym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="5251d-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="5251d-174">Praca z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="5251d-174">Work with U-SQL</span></span>

<span data-ttu-id="5251d-175">Należy otworzyć plik U-SQL lub folder do pracy w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="5251d-176">**Aby otworzyć folder projektu U-SQL**</span><span class="sxs-lookup"><span data-stu-id="5251d-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="5251d-177">W programie Visual Studio Code, wybierz **pliku** menu, a następnie wybierz **Otwórz Folder**.</span><span class="sxs-lookup"><span data-stu-id="5251d-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="5251d-178">Określ folder, a następnie wybierz **wybierz Folder**.</span><span class="sxs-lookup"><span data-stu-id="5251d-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="5251d-179">Wybierz **pliku** menu, a następnie wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="5251d-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="5251d-180">Plik 1 bez tytułu zostanie dodany do projektu.</span><span class="sxs-lookup"><span data-stu-id="5251d-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="5251d-181">Wprowadź następujący kod do pliku bez tytułu 1:</span><span class="sxs-lookup"><span data-stu-id="5251d-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="5251d-182">Skrypt tworzy plik departments.csv z niektóre dane zawarte w folderze/Output.</span><span class="sxs-lookup"><span data-stu-id="5251d-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="5251d-183">Zapisz plik jako **myUSQL.usql** w otwartym folderze.</span><span class="sxs-lookup"><span data-stu-id="5251d-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="5251d-184">Plik konfiguracji adltools_settings.json jest także dodawane do projektu.</span><span class="sxs-lookup"><span data-stu-id="5251d-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="5251d-185">Otwórz i skonfiguruj adltools_settings.json z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="5251d-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="5251d-186">Konto: Konta Data Lake Analytics w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="5251d-187">Baza danych: Baza danych przy użyciu tego konta.</span><span class="sxs-lookup"><span data-stu-id="5251d-187">Database: A database under your account.</span></span> <span data-ttu-id="5251d-188">Wartość domyślna to **wzorca**.</span><span class="sxs-lookup"><span data-stu-id="5251d-188">The default is **master**.</span></span>
    - <span data-ttu-id="5251d-189">Schemat: Schemat w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5251d-189">Schema: A schema under your database.</span></span> <span data-ttu-id="5251d-190">Wartość domyślna to **dbo**.</span><span class="sxs-lookup"><span data-stu-id="5251d-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="5251d-191">Ustawienia opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="5251d-191">Optional settings:</span></span>
        - <span data-ttu-id="5251d-192">Priorytet: Zakres priorytetu jest z zakresu od 1 do 1000 z 1 oznacza najwyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="5251d-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="5251d-193">Wartość domyślna to **1000**.</span><span class="sxs-lookup"><span data-stu-id="5251d-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="5251d-194">Równoległość: Zakres równoległości jest z zakresu od 1 do 150.</span><span class="sxs-lookup"><span data-stu-id="5251d-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="5251d-195">Wartość domyślna to równoległości maksymalny dozwolony na koncie usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="5251d-196">Jeśli te ustawienia są nieprawidłowe, zostaną użyte wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="5251d-196">If the settings are invalid, the default values are used.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code pliku konfiguracji](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="5251d-198">Obliczeniowe konta usługi Data Lake Analytics jest potrzebny do kompilowanie i uruchamianie zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="5251d-199">Aby można było skompilować i uruchamianie zadań U-SQL, należy skonfigurować konto komputera.</span><span class="sxs-lookup"><span data-stu-id="5251d-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="5251d-200">Po zapisaniu konfiguracji informacje konta, bazy danych i schematu są wyświetlane na pasku stanu, w lewym dolnym rogu odpowiedni plik .usql.</span><span class="sxs-lookup"><span data-stu-id="5251d-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="5251d-201">W porównaniu do otwierania pliku, po otwarciu folderu, które można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5251d-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="5251d-202">Użyj pliku CodeBehind.</span><span class="sxs-lookup"><span data-stu-id="5251d-202">Use a code-behind file.</span></span> <span data-ttu-id="5251d-203">W trybie pojedynczego pliku CodeBehind nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5251d-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="5251d-204">Przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5251d-204">Use a configuration file.</span></span> <span data-ttu-id="5251d-205">Po otwarciu folderu skryptów w folderze roboczym udostępniać pojedynczym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5251d-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="5251d-206">Skrypt U-SQL kompiluje zdalnie za pomocą usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="5251d-207">Podczas wystawiania **skompilować** polecenia skryptu U-SQL jest wysyłany do swojego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="5251d-208">Później Visual Studio Code odbiera wynik kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5251d-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="5251d-209">Z powodu zdalnej kompilacji programu Visual Studio Code wymaga, wyświetlić listę informacji do łączenia się z kontem usługi Data Lake Analytics w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5251d-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="5251d-210">**Do kompilowania skryptu U-SQL**</span><span class="sxs-lookup"><span data-stu-id="5251d-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="5251d-211">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="5251d-212">Wprowadź **ADL: kompilowania skryptu**.</span><span class="sxs-lookup"><span data-stu-id="5251d-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="5251d-213">Zostaną wyświetlone wyniki kompilacji w **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="5251d-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="5251d-214">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: kompilowania skryptu** skompilować zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="5251d-215">Wynik kompilacji jest wyświetlana w **dane wyjściowe** okienka.</span><span class="sxs-lookup"><span data-stu-id="5251d-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="5251d-216">**Aby przesłać skrypt U-SQL**</span><span class="sxs-lookup"><span data-stu-id="5251d-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="5251d-217">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="5251d-218">Wprowadź **ADL: przesłać zadania**.</span><span class="sxs-lookup"><span data-stu-id="5251d-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="5251d-219">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="5251d-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="5251d-220">Po przesłaniu zadania skryptu U-SQL w dziennikach przesyłania są wyświetlane w **dane wyjściowe** okna w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="5251d-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="5251d-221">Jeśli przesyłanie zakończy się pomyślnie, zadanie adres URL pojawia się również.</span><span class="sxs-lookup"><span data-stu-id="5251d-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="5251d-222">Adres URL zadania można otworzyć w przeglądarce sieci web, aby śledzić stan zadania w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="5251d-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="5251d-223">Aby włączyć danych wyjściowych szczegóły zadania, ustaw **jobInformationOutputPath** w **vs kod u sql_settings.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="5251d-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="5251d-224">Przy użyciu pliku CodeBehind</span><span class="sxs-lookup"><span data-stu-id="5251d-224">Use a code-behind file</span></span>

<span data-ttu-id="5251d-225">Plik CodeBehind jest pliku C# skojarzonego z jednego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="5251d-226">Skrypt dedykowanych można zdefiniować UDO UDA, UDT i funkcji zdefiniowanej przez użytkownika w pliku CodeBehind.</span><span class="sxs-lookup"><span data-stu-id="5251d-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="5251d-227">UDO, UDA, UDT i UDF można bezpośrednio w skrypcie bez rejestrowania najpierw zestaw.</span><span class="sxs-lookup"><span data-stu-id="5251d-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="5251d-228">Plik CodeBehind jest umieszczany w tym samym folderze co jego komunikacji równorzędnej pliku skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="5251d-229">Jeśli skrypt ma nazwę xxx.usql, jako xxx.usql.cs nosi nazwę CodeBehind.</span><span class="sxs-lookup"><span data-stu-id="5251d-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="5251d-230">Jeśli ręcznie usuń plik CodeBehind, funkcja CodeBehind jest wyłączona dla jego skojarzony skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="5251d-231">Aby uzyskać więcej informacji na temat pisania kodu klienta dla skryptu U-SQL, zobacz [pisania i przy użyciu niestandardowego kodu w języku U-SQL: funkcje zdefiniowane przez użytkownika]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="5251d-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="5251d-232">Aby obsługiwać związane z kodem, możesz otworzyć folderu roboczego.</span><span class="sxs-lookup"><span data-stu-id="5251d-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="5251d-233">**Aby wygenerować plik CodeBehind**</span><span class="sxs-lookup"><span data-stu-id="5251d-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="5251d-234">Otwórz plik źródłowy.</span><span class="sxs-lookup"><span data-stu-id="5251d-234">Open a source file.</span></span> 
2. <span data-ttu-id="5251d-235">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="5251d-236">Wprowadź **ADL: generowanie kodu**.</span><span class="sxs-lookup"><span data-stu-id="5251d-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="5251d-237">Plik CodeBehind jest tworzony w tym samym folderze.</span><span class="sxs-lookup"><span data-stu-id="5251d-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="5251d-238">Można również kliknąć prawym przyciskiem myszy plik skryptu, a następnie wybierz **ADL: generowanie kodu za**.</span><span class="sxs-lookup"><span data-stu-id="5251d-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="5251d-239">Aby skompilować i przesłać skrypt U-SQL przy użyciu pliku CodeBehind jest taka sama jak z autonomicznego pliku skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="5251d-240">Dwa poniższe zrzuty ekranu pokazują plik CodeBehind i jego skojarzony plik skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="5251d-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Plik skryptu narzędzi Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="5251d-243">Korzystanie z zestawów</span><span class="sxs-lookup"><span data-stu-id="5251d-243">Use assemblies</span></span>

<span data-ttu-id="5251d-244">Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="5251d-245">Data Lake Tools służy do rejestrowania zestawów niestandardowych kodów w katalogu Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="5251d-246">**Można zarejestrować zestawu**</span><span class="sxs-lookup"><span data-stu-id="5251d-246">**To register an assembly**</span></span>

<span data-ttu-id="5251d-247">Można zarejestrować zestawu za pomocą **ADL: Zarejestruj zestawu** lub **ADL: Zarejestruj zestawu za pomocą konfiguracji** poleceń.</span><span class="sxs-lookup"><span data-stu-id="5251d-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="5251d-248">**Aby zarejestrować za pomocą ADL: polecenie zarejestrować zestawu**</span><span class="sxs-lookup"><span data-stu-id="5251d-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="5251d-249">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="5251d-250">Wprowadź **ADL: zarejestrować zestawu**.</span><span class="sxs-lookup"><span data-stu-id="5251d-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="5251d-251">Określ ścieżkę zestawu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5251d-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="5251d-252">Wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="5251d-253">Wybierz bazę danych.</span><span class="sxs-lookup"><span data-stu-id="5251d-253">Select a database.</span></span>

<span data-ttu-id="5251d-254">Wyniki: Portal jest otwarty w przeglądarce i przedstawia proces rejestracji zestawu.</span><span class="sxs-lookup"><span data-stu-id="5251d-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="5251d-255">Inny wygodny sposób, aby wyzwolić **ADL: Zarejestruj zestawu** polecenie jest kliknij prawym przyciskiem myszy plik .dll w Eksploratorze plików.</span><span class="sxs-lookup"><span data-stu-id="5251d-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="5251d-256">**Aby zarejestrować jednak ADL: Zarejestruj zestawu za pomocą polecenia konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="5251d-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="5251d-257">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="5251d-258">Wprowadź **ADL: zarejestrować zestawu za pomocą konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="5251d-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="5251d-259">Określ ścieżkę zestawu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5251d-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="5251d-260">Plik JSON jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5251d-260">The JSON file is displayed.</span></span> <span data-ttu-id="5251d-261">Przejrzyj i Edytuj zależności zestawu i parametry zasobu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5251d-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="5251d-262">Instrukcje są wyświetlane w **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="5251d-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="5251d-263">Aby przejść do rejestrowania zestawów, Zapisz (Ctrl + S) w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="5251d-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Narzędzia Data Lake Tools dla Visual Studio Code kodem](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="5251d-265">Zależności zestawu: automatycznie wykrywa Azure Data Lake Tools Określa, czy biblioteka DLL nie ma żadnych zależności.</span><span class="sxs-lookup"><span data-stu-id="5251d-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="5251d-266">Zależności są wyświetlane w pliku JSON, po ich wykryciu.</span><span class="sxs-lookup"><span data-stu-id="5251d-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="5251d-267">Zasoby: Można przekazać biblioteki DLL zasobów (na przykład txt, .png i .csv) jako część zestawu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5251d-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="5251d-268">Innym sposobem wyzwolenia **ADL: Zarejestruj zestawu za pomocą konfiguracji** polecenie jest kliknij prawym przyciskiem myszy plik .dll w Eksploratorze plików.</span><span class="sxs-lookup"><span data-stu-id="5251d-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="5251d-269">Poniższy kod języka U-SQL przedstawia sposób wywołania zestawu.</span><span class="sxs-lookup"><span data-stu-id="5251d-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="5251d-270">W przykładzie nazwa zestawu jest *testu*.</span><span class="sxs-lookup"><span data-stu-id="5251d-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="5251d-271">Dostęp do katalogu Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5251d-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="5251d-272">Po podłączeniu do platformy Azure, służy następujące kroki, aby uzyskać dostęp do katalogu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5251d-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="5251d-273">**Aby uzyskać dostępu do metadanych usługi Azure Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="5251d-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="5251d-274">Wybierz kombinację klawiszy Ctrl + Shift + P, a następnie wprowadź **ADL: listy tabel**.</span><span class="sxs-lookup"><span data-stu-id="5251d-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="5251d-275">Wybierz jedno z kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="5251d-276">Wybierz jedną z bazy danych usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="5251d-277">Wybierz jeden ze schematów.</span><span class="sxs-lookup"><span data-stu-id="5251d-277">Select one of the schemas.</span></span> <span data-ttu-id="5251d-278">Można wyświetlić listę tabel.</span><span class="sxs-lookup"><span data-stu-id="5251d-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="5251d-279">Widok Data Lake Analytics zadania</span><span class="sxs-lookup"><span data-stu-id="5251d-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="5251d-280">**Aby wyświetlić zadania usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="5251d-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="5251d-281">Otwórz palety polecenia (Ctrl + Shift + P) i wybierz **ADL: Pokaż zadania**.</span><span class="sxs-lookup"><span data-stu-id="5251d-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="5251d-282">Wybierz usługi Data Lake Analytics lub konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5251d-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="5251d-283">Poczekaj na liście zadania konta są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="5251d-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="5251d-284">Wybierz zadanie z listy zadań, narzędzi Data Lake Tools Otwiera szczegóły zadania w portalu Azure i plik informacji o zadaniu jest wyświetlany w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="5251d-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="5251d-286">Integracja magazynu usługi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5251d-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="5251d-287">Można użyć poleceń usługi Azure Data Lake Storage, aby:</span><span class="sxs-lookup"><span data-stu-id="5251d-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="5251d-288">Przeglądaj zasoby usługi Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="5251d-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="5251d-289">Wyświetl podgląd pliku usługi Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="5251d-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="5251d-290">Przekaż plik bezpośrednio do usługi Azure Data Lake Storage w kodzie VS.</span><span class="sxs-lookup"><span data-stu-id="5251d-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="5251d-291">Lista ścieżki do magazynu</span><span class="sxs-lookup"><span data-stu-id="5251d-291">List the storage path</span></span> 
<span data-ttu-id="5251d-292">Można wyświetlić listę ścieżki do magazynu za pośrednictwem palety polecenia lub kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="5251d-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="5251d-293">**Aby wyświetlić listę ścieżki magazynu za pomocą polecenia palety**</span><span class="sxs-lookup"><span data-stu-id="5251d-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="5251d-294">Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: ścieżka magazynu listy**.</span><span class="sxs-lookup"><span data-stu-id="5251d-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="5251d-296">Wybierz użytkownika preferowany sposób wyświetlania list ścieżki do magazynu.</span><span class="sxs-lookup"><span data-stu-id="5251d-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="5251d-297">Używa tego przejścia **wprowadź ścieżkę** jako przykład.</span><span class="sxs-lookup"><span data-stu-id="5251d-297">This passage uses **Enter a path** as an example.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code jednym ze sposobów listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="5251d-299">VS kod chroni odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5251d-300">Na przykład: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="5251d-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5251d-301">Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="5251d-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5251d-302">Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="5251d-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="5251d-303">Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz więcej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="5251d-305">Wybierz **więcej** listy więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="5251d-307">Wprowadź ścieżkę do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-307">Enter an Azure storage path.</span></span> <span data-ttu-id="5251d-308">Na przykład/output.</span><span class="sxs-lookup"><span data-stu-id="5251d-308">For example, /output.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code Wprowadź ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="5251d-310">Wyniki: Palety polecenie wyświetla informacje o ścieżce na podstawie wpisów.</span><span class="sxs-lookup"><span data-stu-id="5251d-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code lista wyników ścieżki magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="5251d-312">Bardziej wygodne ścieżka względna jest za pośrednictwem menu kontekstowym kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="5251d-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="5251d-313">**Aby wyświetlić listę ścieżki magazynu za pośrednictwem kliknij prawym przyciskiem myszy**</span><span class="sxs-lookup"><span data-stu-id="5251d-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="5251d-314">Kliknij prawym przyciskiem myszy ciąg ścieżki, aby wybrać **ścieżki do magazynu listy**.</span><span class="sxs-lookup"><span data-stu-id="5251d-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="5251d-316">Wybrana ścieżka względna zostanie wyświetlony w palecie polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-316">The selected relative path appears in the command palette.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code wybrane ścieżki względnej](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="5251d-318">Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="5251d-320">Wyniki: Palety polecenie wyświetla listę folderów i plików dla bieżącej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="5251d-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy z bieżącej ścieżki](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="5251d-322">Podgląd pliku magazynu</span><span class="sxs-lookup"><span data-stu-id="5251d-322">Preview the storage file</span></span>
<span data-ttu-id="5251d-323">Można wyświetlić podgląd pliku magazynu za pośrednictwem palety polecenia lub kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="5251d-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="5251d-324">**Aby wyświetlić podgląd pliku magazynu za pomocą polecenia palety**</span><span class="sxs-lookup"><span data-stu-id="5251d-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="5251d-325">Otwórz palety polecenia (Ctrl + Shift + P), a następnie wprowadź **ADL: Podgląd pliku magazynu**.</span><span class="sxs-lookup"><span data-stu-id="5251d-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wyświetlić podgląd pliku magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="5251d-327">Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code listy kont](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5251d-329">Wybierz **więcej** listy więcej kont usługi Data Lake Analytics, a następnie wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="5251d-331">Wprowadź ścieżkę do magazynu Azure lub pliku.</span><span class="sxs-lookup"><span data-stu-id="5251d-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="5251d-332">Na przykład /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="5251d-332">For example, /output/SearchLog.txt.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę do magazynu i](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="5251d-334">Wyniki: Palety polecenie wyświetla informacje o ścieżce na podstawie wpisów.</span><span class="sxs-lookup"><span data-stu-id="5251d-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="5251d-336">**Aby wyświetlić listę ścieżki magazynu za pośrednictwem kliknij prawym przyciskiem myszy**</span><span class="sxs-lookup"><span data-stu-id="5251d-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="5251d-337">Aby wyświetlić podgląd pliku, kliknij prawym przyciskiem myszy ścieżkę pliku.</span><span class="sxs-lookup"><span data-stu-id="5251d-337">To preview a file, right-click the file path.</span></span>

   ![Narzędzia Data Lake Tools dla Visual Studio Code kliknij prawym przyciskiem myszy menu kontekstowe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="5251d-339">Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz konto](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5251d-341">Wyniki: Kod VS wyświetla wyniki podglądu pliku.</span><span class="sxs-lookup"><span data-stu-id="5251d-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code Podgląd pliku wyników](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="5251d-343">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="5251d-343">Upload a file</span></span> 

<span data-ttu-id="5251d-344">Możesz przekazać pliki, wprowadzając polecenia **ADL: Przekaż plik** lub **ADL: Przekaż plik przy użyciu konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="5251d-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="5251d-345">**Aby przekazać pliki jednak ADL: Przekaż plik — polecenie**</span><span class="sxs-lookup"><span data-stu-id="5251d-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="5251d-346">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia lub kliknij prawym przyciskiem myszy edytora skryptów, a następnie wprowadź **Przekaż plik**.</span><span class="sxs-lookup"><span data-stu-id="5251d-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="5251d-347">Można przekazać pliku, wprowadź ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="5251d-347">To upload the file, enter a local path.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wprowadź ścieżkę lokalną](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="5251d-349">Wybierz jeden ze sposobów wyświetlania ścieżki do magazynu.</span><span class="sxs-lookup"><span data-stu-id="5251d-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="5251d-350">Używa tego przejścia **wprowadź ścieżkę** jako przykład.</span><span class="sxs-lookup"><span data-stu-id="5251d-350">This passage uses **Enter a path** as an example.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code listy ścieżki do magazynu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="5251d-352">VS kod chroni odwiedzi ostatnie ścieżki co konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5251d-353">Na przykład: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="5251d-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5251d-354">Przeglądarka ze ścieżki katalogu głównego: ścieżka katalogu głównego listy z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="5251d-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5251d-355">Wprowadź ścieżkę: Lista określonej ścieżki z wybranego konta usługi Data Lake Analytics lub ścieżkę lokalną.</span><span class="sxs-lookup"><span data-stu-id="5251d-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="5251d-356">Wybierz konto z ścieżka lokalna lub konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code magazynu, kliknij prawym przyciskiem myszy](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="5251d-358">Wprowadź ścieżkę do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-358">Enter an Azure storage path.</span></span> <span data-ttu-id="5251d-359">Na przykład: / output.</span><span class="sxs-lookup"><span data-stu-id="5251d-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="5251d-360">Znajdź ścieżki magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-360">Find your Azure storage path.</span></span> <span data-ttu-id="5251d-361">Wybierz **Wybierz bieżący folder**.</span><span class="sxs-lookup"><span data-stu-id="5251d-361">Select **Choose current folder**.</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio Code wybierz folder](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="5251d-363">Wyniki: **dane wyjściowe** okno wyświetla stan przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="5251d-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="5251d-365">**Aby przekazać pliki jednak ADL: Przekaż plik za pomocą polecenia konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="5251d-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="5251d-366">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia lub kliknij prawym przyciskiem myszy edytora skryptów, a następnie wprowadź **Przekaż plik przy użyciu konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="5251d-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="5251d-367">VS kod przedstawia plik JSON.</span><span class="sxs-lookup"><span data-stu-id="5251d-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="5251d-368">Można wprowadzić ścieżki do plików i przekazywania wielu plików jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="5251d-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="5251d-369">Instrukcje są wyświetlane w **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="5251d-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="5251d-370">Aby kontynuować, można przekazać pliku, Zapisz (Ctrl + S) w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="5251d-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Ścieżka pliku narzędzia Data Lake Tools dla Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="5251d-372">Wyniki: **dane wyjściowe** okno wyświetla stan przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="5251d-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Narzędzia Data Lake Tools dla Visual Studio Code przekazać stanu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="5251d-374">Innym sposobem przekazania pliku do magazynu jest za pomocą menu kliknij prawym przyciskiem myszy na pełną ścieżkę pliku lub ścieżki względnej pliku w Edytorze skryptów.</span><span class="sxs-lookup"><span data-stu-id="5251d-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="5251d-375">Wprowadź ścieżkę do pliku lokalnego, a następnie wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="5251d-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="5251d-376">**Dane wyjściowe** okno wyświetla stan przekazywania.</span><span class="sxs-lookup"><span data-stu-id="5251d-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="5251d-377">Eksplorator usługi Storage Azure Otwórz</span><span class="sxs-lookup"><span data-stu-id="5251d-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="5251d-378">Możesz otworzyć **Eksploratora usługi Storage Azure** przez wprowadzenie polecenia **ADL: Otwórz Eksploratora usługi sieci Web Azure Storage** lub wybierając z menu kontekstowego kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="5251d-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="5251d-379">**Aby otworzyć Eksploratora usługi Storage platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="5251d-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="5251d-380">Wybierz kombinację klawiszy Ctrl + Shift + P, aby otworzyć paletę polecenia.</span><span class="sxs-lookup"><span data-stu-id="5251d-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="5251d-381">Wprowadź **Otwórz Eksploratora usługi Storage Azure Web** lub kliknij prawym przyciskiem myszy na ścieżkę względną lub pełną ścieżkę w Edytorze skryptów, a następnie wybierz **Otwórz Eksploratora usługi Storage Azure Web**.</span><span class="sxs-lookup"><span data-stu-id="5251d-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="5251d-382">Wybierz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="5251d-383">Narzędzia Data Lake Tools otwiera ścieżki do magazynu Azure w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5251d-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="5251d-384">Można znaleźć ścieżki i wyświetlić podgląd pliku z sieci web.</span><span class="sxs-lookup"><span data-stu-id="5251d-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="5251d-385">Przebieg lokalny i lokalny debugowania dla systemu Windows użytkownicy</span><span class="sxs-lookup"><span data-stu-id="5251d-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="5251d-386">Uruchamiania lokalnego skryptu U-SQL sprawdza danych lokalnych i sprawdza poprawność skrypt lokalnie, przed opublikowaniem kodu do usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="5251d-387">Funkcja debugowania lokalnego umożliwia wykonywanie następujących zadań przed przesłaniem do usługi Data Lake Analytics kodu:</span><span class="sxs-lookup"><span data-stu-id="5251d-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="5251d-388">Debugowanie programu C# związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="5251d-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="5251d-389">Kroków opisanych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5251d-389">Step through the code.</span></span> 
- <span data-ttu-id="5251d-390">Sprawdź poprawność skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5251d-390">Validate your script locally.</span></span>

<span data-ttu-id="5251d-391">Aby uzyskać instrukcje dotyczące przebiegu lokalnego i debugowania lokalnego, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="5251d-392">Dodatkowe funkcje</span><span class="sxs-lookup"><span data-stu-id="5251d-392">Additional features</span></span>

<span data-ttu-id="5251d-393">Narzędzia Data Lake Tools dla programu VS kodu obsługuje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="5251d-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="5251d-394">Funkcja automatycznego uzupełniania IntelliSense: sugestie są wyświetlane w wyskakujące wokół elementów, takich jak słowa kluczowe, metod i zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5251d-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="5251d-395">Inne ikony reprezentują różnych typów obiektów:</span><span class="sxs-lookup"><span data-stu-id="5251d-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="5251d-396">Scala — typ danych</span><span class="sxs-lookup"><span data-stu-id="5251d-396">Scala data type</span></span>
    - <span data-ttu-id="5251d-397">Typ danych złożonych</span><span class="sxs-lookup"><span data-stu-id="5251d-397">Complex data type</span></span>
    - <span data-ttu-id="5251d-398">Wbudowanych typów</span><span class="sxs-lookup"><span data-stu-id="5251d-398">Built-in UDTs</span></span>
    - <span data-ttu-id="5251d-399">Klasy i kolekcji .NET</span><span class="sxs-lookup"><span data-stu-id="5251d-399">.NET collection and classes</span></span>
    - <span data-ttu-id="5251d-400">Wyrażenia języka C#</span><span class="sxs-lookup"><span data-stu-id="5251d-400">C# expressions</span></span>
    - <span data-ttu-id="5251d-401">Funkcje UDF wbudowane C#, obiektów udo i UDAAGs</span><span class="sxs-lookup"><span data-stu-id="5251d-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="5251d-402">Funkcje języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="5251d-402">U-SQL functions</span></span>
    - <span data-ttu-id="5251d-403">Funkcją okienkową U-SQL</span><span class="sxs-lookup"><span data-stu-id="5251d-403">U-SQL windowing function</span></span>
 
    ![Typy obiektów narzędzi Data Lake Tools dla programu Visual Studio kodu IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="5251d-405">Funkcja automatycznego uzupełniania w metadanych usługi Data Lake Analytics IntelliSense: narzędzi Data Lake Tools pobierze lokalnie informacje metadanych usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="5251d-406">Funkcja IntelliSense automatycznie wypełni obiektów, łącznie z bazy danych, schematu, tabeli, widoku, funkcji zwracającej tabelę, procedury i zestawów języka C# z metadanych usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5251d-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Narzędzia Data Lake Tools dla programu Visual Studio kodu IntelliSense metadanych](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="5251d-408">Znacznik błąd IntelliSense: narzędzi Data Lake Tools podkreśla błędy edytowania U-SQL i C#.</span><span class="sxs-lookup"><span data-stu-id="5251d-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="5251d-409">Najważniejsze funkcje Składnia: narzędzi Data Lake Tools używa różne kolory do odróżnienia elementów, takich jak zmienne, słowa kluczowe, typ danych i funkcji.</span><span class="sxs-lookup"><span data-stu-id="5251d-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Zawiera opis narzędzi Data Lake Tools dla Visual Studio Code składni](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="5251d-411">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5251d-411">Next steps</span></span>

- <span data-ttu-id="5251d-412">Dla przebiegu lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio, zobacz [uruchamiania lokalnego skryptu U-SQL i debugowania lokalnego z kodem Visual Studio](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="5251d-413">Aby — wprowadzenie informacji na temat usługi Data Lake Analytics, zobacz [samouczek: rozpoczynanie pracy z usługą Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="5251d-414">Aby informacji na temat narzędzia Data Lake Tools dla programu Visual Studio, zobacz [samouczek: skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="5251d-415">Aby uzyskać informacje na temat tworzenia zespołów, zobacz [opracowanie U-SQL zestawy dla usługi Azure Data Lake Analytics zadań](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="5251d-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



