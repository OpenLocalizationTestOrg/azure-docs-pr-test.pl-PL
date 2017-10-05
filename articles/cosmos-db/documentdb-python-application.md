---
title: "Samouczek dotyczący aplikacji internetowej platformy Python Flask dla usługi Azure Cosmos DB | Microsoft Docs"
description: "Przejrzyj samouczek bazy danych na temat korzystania z usługi Azure Cosmos DB w celu przechowywania i uzyskiwania dostępu do danych z aplikacji internetowej platformy Python Flask hostowanej na platformie Azure. Znajdź rozwiązania do tworzenia aplikacji."
keywords: Application development, python flask, python web application, python web development
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="fd0fe-105">Tworzenie aplikacji internetowej platformy Python Flask za pomocą usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd0fe-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd0fe-106">.NET</span><span class="sxs-lookup"><span data-stu-id="fd0fe-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="fd0fe-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="fd0fe-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="fd0fe-108">Java</span><span class="sxs-lookup"><span data-stu-id="fd0fe-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="fd0fe-109">Python</span><span class="sxs-lookup"><span data-stu-id="fd0fe-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="fd0fe-110">Ten samouczek pokazuje, jak używać usługi Azure Cosmos DB do przechowywania i uzyskiwania dostępu do danych aplikacji internetowej utworzonej w języku Python i hostowanej na platformie Azure. Przyjęto w nim założenie, że użytkownik posiada już pewne doświadczenie związane z używaniem języka Python i witryn internetowych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="fd0fe-111">Ten samouczek bazy danych obejmuje następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="fd0fe-112">Tworzenie i Inicjowanie obsługi konta DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="fd0fe-113">Tworzenie aplikacji platformy Python Flask.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="fd0fe-114">Nawiązywanie połączenia z usługą Azure Cosmos DB i korzystanie z niej z poziomu aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="fd0fe-115">Wdrażanie aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="fd0fe-116">Wykonując poszczególne kroki tego samouczka, utworzysz prostą aplikację do głosowania, która umożliwia głosowanie w ankiecie.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Zrzut ekranu przedstawiający aplikację do głosowania utworzone przez tego samouczka bazy danych](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="fd0fe-118">Wymagania wstępne dotyczące samouczka</span><span class="sxs-lookup"><span data-stu-id="fd0fe-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="fd0fe-119">Przed wykonaniem instrukcji zawartych w tym artykule upewnij się, że masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="fd0fe-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-120">An active Azure account.</span></span> <span data-ttu-id="fd0fe-121">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fd0fe-122">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="fd0fe-123">LUB</span><span class="sxs-lookup"><span data-stu-id="fd0fe-123">OR</span></span> 

    <span data-ttu-id="fd0fe-124">Lokalna instalacja [emulatora usługi Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="fd0fe-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="fd0fe-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="fd0fe-127">[Zestaw Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="fd0fe-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fd0fe-129">Jeśli instalujesz środowisko Python 2.7 po raz pierwszy, upewnij się, na ekranie dostosować Python 2.7.13 wybranym **Dodaj python.exe do ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Zrzut ekranu Customize Python 2.7.11 (Dostosowywanie środowiska Python 2.7.11), na którym należy wybrać pozycję Add python.exe to Path (Dodaj plik python.exe do ścieżki)](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="fd0fe-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="fd0fe-132">Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd0fe-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="fd0fe-133">Zacznijmy od utworzenia konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="fd0fe-134">Jeśli masz już konto lub jeśli korzystasz z emulatora usługi Azure Cosmos DB na potrzeby tego samouczka, możesz od razu przejść do sekcji [Krok 2. Tworzenie nowej aplikacji internetowej platformy Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="fd0fe-135">Teraz przejdziemy przez proces tworzenia nowej aplikacji sieci Web platformy Python Flask od podstaw.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="fd0fe-136">Krok 2. Tworzenie nowej aplikacji sieci Web platformy Python Flask</span><span class="sxs-lookup"><span data-stu-id="fd0fe-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="fd0fe-137">W menu **Plik** programu Visual Studio wskaż pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="fd0fe-138">Zostanie wyświetlone okno dialogowe **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="fd0fe-139">W lewym okienku rozwiń pozycję **Szablony** i **Python**, a następnie kliknij pozycję **Sieć Web**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="fd0fe-140">W środkowym okienku wybierz pozycję **Projekt sieci Web platformy Flask**, a następnie w polu **Nazwa** wpisz wartość **tutorial** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="fd0fe-141">Pamiętaj, że wszystkie nazwy pakietów języka Python powinny być pisane małymi literami, zgodnie z opisem zawartym w publikacji [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names) (Przewodnik po stylu kodu Python).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="fd0fe-142">Python Flask to platforma programistyczna aplikacji sieci Web, która umożliwia szybsze tworzenie aplikacji sieci Web w języku Python.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Zrzut ekranu okna Nowy projekt w programie Visual Studio z wyróżnioną po lewej stronie pozycją Python, zaznaczoną w środkowej części pozycją Projekt sieci Web platformy Python Flask oraz nazwą tutorial w polu Nazwa](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="fd0fe-144">W oknie **Python Tools for Visual Studio** kliknij pozycję **Zainstaluj w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Zrzut ekranu samouczka bazy danych — okno Python Tools for Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="fd0fe-146">W oknie **Dodawanie środowiska wirtualnego** możesz zaakceptować wartości domyślne i użyć środowiska Python 2.7 jako podstawowego środowiska, ponieważ pakiet PyDocumentDB nie obsługuje obecnie środowiska Python 3.x, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="fd0fe-147">Spowoduje to skonfigurowanie wymaganego środowiska wirtualnego Python dla Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Zrzut ekranu samouczka bazy danych — okno Python Tools for Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="fd0fe-149">Po pomyślnym zainstalowaniu środowiska w oknie Dane wyjściowe zostanie wyświetlona informacja `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.`.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="fd0fe-150">Krok 3. Modyfikowanie aplikacji sieci Web platformy Python Flask</span><span class="sxs-lookup"><span data-stu-id="fd0fe-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="fd0fe-151">Dodawanie pakietów platformy Python Flask do projektu</span><span class="sxs-lookup"><span data-stu-id="fd0fe-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="fd0fe-152">Po skonfigurowaniu projektu musisz dodać do niego wymagane pakiety platformy Flask, w tym pydocumentdb — pakiet języka Python dla usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="fd0fe-153">W Eksploratorze rozwiązań otwórz plik o nazwie **requirements.txt** i zastąp jego zawartość następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="fd0fe-154">Zapisz plik **requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="fd0fe-155">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **env**, a następnie kliknij polecenie **Zainstaluj z pliku requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Zrzut ekranu przedstawiający wybraną pozycję env (Python 2.7) oraz polecenie Zainstaluj z pliku requirements.txt wyróżnione na liście](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="fd0fe-157">Po pomyślnej instalacji w oknie Dane wyjściowe zostaną wyświetlone następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="fd0fe-158">W rzadkich przypadkach w oknie Dane wyjściowe może zostać wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="fd0fe-159">Jeśli tak się stanie, sprawdź, czy błąd jest związany z oczyszczaniem.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="fd0fe-160">Czasami oczyszczanie nie powiedzie się, ale instalacja i tak zakończy się pomyślnie (aby to sprawdzić, przewiń w górę w oknie Dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="fd0fe-161">Instalację można sprawdzić przez [zweryfikowanie środowiska wirtualnego](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="fd0fe-162">Jeśli instalacja nie powiodła się, ale weryfikacja zakończyła się pomyślnie, można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="fd0fe-163">Weryfikowanie środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="fd0fe-163">Verify the virtual environment</span></span>
<span data-ttu-id="fd0fe-164">Upewnijmy się, że wszystko jest poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="fd0fe-165">Skompiluj rozwiązanie, naciskając klawisze **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="fd0fe-166">Gdy kompilacja zakończy się powodzeniem, uruchom witrynę sieci Web, naciskając klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="fd0fe-167">Powoduje to uruchomienie serwera programistycznego platformy Flask i przeglądarki sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="fd0fe-168">Powinna zostać wyświetlona następująca strona.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-168">You should see the following page.</span></span>
   
    ![Pusty projekt aplikacji sieci Web platformy Python Flask wyświetlony w przeglądarce](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="fd0fe-170">Zatrzymaj debugowanie witryny sieci Web, naciskając klawisze **Shift**+**F5** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="fd0fe-171">Tworzenie definicji bazy danych, kolekcji i dokumentu</span><span class="sxs-lookup"><span data-stu-id="fd0fe-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="fd0fe-172">Teraz utwórzmy aplikację do głosowania przez dodanie nowych plików i zaktualizowanie pozostałych.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="fd0fe-173">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **tutorial**, kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="fd0fe-174">Wybierz pozycję **Pusty plik Python** i nazwij ten plik **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="fd0fe-175">Dodaj następujący kod do pliku forms.py, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="fd0fe-176">Dodawanie wymaganych importów do pliku views.py</span><span class="sxs-lookup"><span data-stu-id="fd0fe-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="fd0fe-177">W Eksploratorze rozwiązań rozwiń folder **tutorial**, a następnie otwórz plik **views.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="fd0fe-178">Dodaj następujące instrukcje importu u góry pliku **views.py**, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="fd0fe-179">Spowoduje to zaimportowanie zestawu SDK Python usługi Cosmos DB oraz pakietów platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="fd0fe-180">Tworzenie bazy danych, kolekcji i dokumentu</span><span class="sxs-lookup"><span data-stu-id="fd0fe-180">Create database, collection, and document</span></span>
* <span data-ttu-id="fd0fe-181">Dodaj następujący kod na końcu pliku **views.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="fd0fe-182">Odpowiada on za tworzenie bazy danych używanej przez formularz.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="fd0fe-183">Nie usuwaj żadnego kodu znajdującego się w pliku **views.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="fd0fe-184">Po prostu dołącz podany kod na końcu.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="fd0fe-185">Odczytywanie bazy danych, kolekcji i dokumentów oraz przesyłanie formularza</span><span class="sxs-lookup"><span data-stu-id="fd0fe-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="fd0fe-186">Dodaj następujący kod na końcu pliku **views.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="fd0fe-187">Odpowiada on za konfigurowanie formularza oraz odczytywanie bazy danych, kolekcji i dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="fd0fe-188">Nie usuwaj żadnego kodu znajdującego się w pliku **views.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="fd0fe-189">Po prostu dołącz podany kod na końcu.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-189">Simply append this to the end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-the-html-files"></a><span data-ttu-id="fd0fe-190">Tworzenie plików HTML</span><span class="sxs-lookup"><span data-stu-id="fd0fe-190">Create the HTML files</span></span>
1. <span data-ttu-id="fd0fe-191">W Eksploratorze rozwiązań, w folderze **tutorial** kliknij prawym przyciskiem myszy folder **templates**, potem polecenie **Dodaj**, a następnie kliknij pozycję **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="fd0fe-192">Wybierz pozycję **Strona HTML**, a następnie w polu nazwy wpisz **create.html**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="fd0fe-193">Powtórz kroki 1 i 2, aby utworzyć dwa dodatkowe pliki HTML: results.html i vote.html.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="fd0fe-194">Dodaj następujący kod do pliku **create.html** w elemencie `<body>`.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="fd0fe-195">Służy do wyświetlania komunikatu informującego o tym, że utworzyliśmy nową bazę danych, kolekcję i dokument.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="fd0fe-196">Dodaj następujący kod do pliku **results.html** w elemencie `<body`>.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="fd0fe-197">Służy do wyświetlania wyników ankiety.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="fd0fe-198">Dodaj następujący kod do pliku **vote.html** w elemencie `<body`>.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="fd0fe-199">Służy do wyświetlania ankiety i akceptowania oddanych głosów.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="fd0fe-200">Po zarejestrowaniu głosów kontrola jest przekazywana do pliku views.py, gdzie oddany głos jest rozpoznawany i odpowiednie dane są dołączane do dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="fd0fe-201">W folderze **templates** zastąp zawartość pliku **index.html** poniższym kodem.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="fd0fe-202">Będzie to strona docelowa dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="fd0fe-203">Dodawanie pliku konfiguracji i zmienianie pliku \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="fd0fe-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="fd0fe-204">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **tutorial**, kliknij polecenie **Dodaj**, potem pozycję **Nowy element**, następnie wybierz opcję **Pusty plik Python**, a na końcu podaj nazwę pliku, **config.py**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="fd0fe-205">Ten plik konfiguracji jest wymagany przez formularze na platformie Flask.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="fd0fe-206">Można go również użyć, aby dostarczyć klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="fd0fe-207">Ten klucz nie jest jednak potrzebny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="fd0fe-208">Dodaj poniższy kod do pliku config.py. Konieczna będzie zmiana wartości **DOCUMENTDB\_HOST** i **DOCUMENTDB\_KEY** w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="fd0fe-209">W witrynie [Azure Portal](https://portal.azure.com/) przejdź do bloku **Klucze**, klikając pozycję **Przeglądaj**, **Konta usługi Azure Cosmos DB**, kliknij dwukrotnie nazwę konta, którego chcesz użyć, a następnie kliknij przycisk **Klucze** w obszarze **Podstawy**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="fd0fe-210">W bloku **Klucze** skopiuj wartość **URI** i wklej ją do pliku **config.py** jako wartość właściwości **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="fd0fe-211">W witrynie Azure Portal, w bloku **Klucze** skopiuj wartość **Klucz podstawowy** lub **Klucz pomocniczy** i wklej ją do pliku **config.py** jako wartość właściwości **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="fd0fe-212">W pliku **\_\_init\_\_.py** dodaj następujący wiersz.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="fd0fe-213">Plik powinien mieć następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="fd0fe-214">Po dodaniu wszystkich plików Eksplorator rozwiązań powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Zrzut ekranu okna Eksploratora rozwiązań programu Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="fd0fe-216">Krok 4. Uruchamianie aplikacji sieci Web lokalnie</span><span class="sxs-lookup"><span data-stu-id="fd0fe-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="fd0fe-217">Skompiluj rozwiązanie, naciskając klawisze **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="fd0fe-218">Gdy kompilacja zakończy się powodzeniem, uruchom witrynę sieci Web, naciskając klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="fd0fe-219">Na ekranie powinna być widoczna następująca strona.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-219">You should see the following on your screen.</span></span>
   
    ![Zrzut ekranu aplikacji do głosowania opartej na języku Python i usłudze Azure Cosmos DB wyświetlonej w przeglądarce internetowej](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="fd0fe-221">Kliknij przycisk **Create/Clear the Voting Database** (Utwórz/wyczyść bazę danych głosowania), aby wygenerować bazę danych.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Zrzut ekranu strony tworzenia w aplikacji sieci Web — szczegóły programowania](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="fd0fe-223">Następnie kliknij przycisk **Vote** (Głosuj) i wybierz jedną z opcji.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-223">Then, click **Vote** and select your option.</span></span>
   
    ![Zrzut ekranu aplikacji sieci Web z pytaniem, na które należy udzielić odpowiedzi](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="fd0fe-225">Każdy oddany głos powoduje zwiększenie odpowiedniego licznika.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Zrzut ekranu strony Results of the vote (Wyniki głosowania)](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="fd0fe-227">Zatrzymaj debugowanie projektu przez naciśnięcie klawiszy Shift+F5.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="fd0fe-228">Krok 5: Wdrażanie aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fd0fe-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="fd0fe-229">Teraz, gdy kompletna aplikacja działa poprawnie z rozwiązania Cosmos DB, chcemy to wdrażanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="fd0fe-230">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań (upewnij się, że nie jest uruchomiony lokalnie) i wybierz polecenie **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Zrzut ekranu przedstawiający pozycję tutorial wybraną w Eksploratorze rozwiązań oraz wyróżnione polecenie Publikuj](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="fd0fe-232">W **publikowania** okno dialogowe, wybierz opcję **Microsoft Azure App Service**, wybierz pozycję **Utwórz nowy**, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Zrzut ekranu okna publikowanie w sieci Web wyróżnione program Microsoft Azure App Service](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="fd0fe-234">W **Tworzenie usługi App Service** okna dialogowego wprowadź nazwę dla aplikacji sieci web, wraz z Twojej **subskrypcji**, **grupy zasobów**, i **planu usługi App Service**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Zrzut ekranu okna Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="fd0fe-236">W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji usługi i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="fd0fe-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Zrzut ekranu okna Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="fd0fe-238">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fd0fe-238">Troubleshooting</span></span>
<span data-ttu-id="fd0fe-239">Jeśli jest to pierwsza aplikacja napisana w języku Python uruchomiona na Twoim komputerze, upewnij się, że następujące foldery (lub odpowiadające im lokalizacje instalacji) są uwzględnione w zmiennej PATH:</span><span class="sxs-lookup"><span data-stu-id="fd0fe-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="fd0fe-240">Jeśli wystąpi błąd na stronie głosowania, a nazwa projektu jest inna niż **tutorial**, upewnij się, że plik **\_\_init\_\_.py** odwołuje się do właściwej nazwy projektu w wierszu: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd0fe-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd0fe-241">Next steps</span></span>
<span data-ttu-id="fd0fe-242">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="fd0fe-242">Congratulations!</span></span> <span data-ttu-id="fd0fe-243">Po prostu ma wykonać swoją pierwszą aplikację sieci web języka Python za pomocą rozwiązania Cosmos bazy danych i opublikować ją w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="fd0fe-244">Często aktualizujemy i poprawiamy ten temat na podstawie opinii czytelników.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="fd0fe-245">Po ukończeniu samouczka użyj przycisków głosowania znajdujących się u góry i u dołu tej strony oraz napisz swoją opinię na temat tego, co możemy ulepszyć.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="fd0fe-246">Jeśli chcesz, abyśmy skontaktowali się z Tobą bezpośrednio, możesz w komentarzach podać swój adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="fd0fe-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="fd0fe-247">Aby dodać dodatkowe funkcje do aplikacji sieci web, zapoznaj się z interfejsami API dostępnymi w [Azure rozwiązania Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="fd0fe-248">Aby uzyskać więcej informacji na temat platformy Azure, programu Visual Studio i języka Python, zobacz [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="fd0fe-249">Dodatkowe samouczki dotyczące platformy Python Flask znajdziesz na stronie [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) (Megasamouczek platformy Flask, część I: Witaj, świecie!).</span><span class="sxs-lookup"><span data-stu-id="fd0fe-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
