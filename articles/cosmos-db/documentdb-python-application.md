---
title: "Samouczek aplikacji sieci web platformy Flask aaaPython dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Przejrzyj samouczek bazy danych przy użyciu bazy danych Azure rozwiązania Cosmos toostore i dostępu do danych z aplikacji sieci web platformy Python Flask hostowanej na platformie Azure. Znajdź rozwiązania do tworzenia aplikacji."
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
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="f2d82-105">Tworzenie aplikacji internetowej platformy Python Flask za pomocą usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f2d82-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2d82-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f2d82-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f2d82-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f2d82-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f2d82-108">Java</span><span class="sxs-lookup"><span data-stu-id="f2d82-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f2d82-109">Python</span><span class="sxs-lookup"><span data-stu-id="f2d82-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f2d82-110">Ten samouczek pokazuje, jak toouse danych toostore i dostępu do bazy danych Azure rozwiązania Cosmos w języku Python hostowanej na platformie Azure aplikacji sieci web i przyjęto założenie, że ma pewne doświadczenie w korzystaniu z języka Python i witryn sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d82-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="f2d82-111">Ten samouczek bazy danych obejmuje następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="f2d82-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="f2d82-112">Tworzenie i Inicjowanie obsługi konta DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f2d82-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="f2d82-113">Tworzenie aplikacji platformy Python Flask.</span><span class="sxs-lookup"><span data-stu-id="f2d82-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="f2d82-114">Łączenie tooand przy użyciu rozwiązania Cosmos bazy danych z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="f2d82-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="f2d82-115">Wdrażanie tooAzure aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="f2d82-116">W ramach tego samouczka, utworzysz prostą aplikację do głosowania umożliwiający toovote w ankiecie.</span><span class="sxs-lookup"><span data-stu-id="f2d82-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Zrzut ekranu przedstawiający aplikację do głosowania hello utworzone przez tego samouczka bazy danych](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="f2d82-118">Wymagania wstępne dotyczące samouczka</span><span class="sxs-lookup"><span data-stu-id="f2d82-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="f2d82-119">Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że mają zainstalowane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f2d82-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="f2d82-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d82-120">An active Azure account.</span></span> <span data-ttu-id="f2d82-121">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f2d82-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f2d82-122">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="f2d82-123">LUB</span><span class="sxs-lookup"><span data-stu-id="f2d82-123">OR</span></span> 

    <span data-ttu-id="f2d82-124">Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f2d82-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="f2d82-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="f2d82-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="f2d82-127">[Zestaw Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="f2d82-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f2d82-129">Jeśli instalujesz środowisko Python 2.7 dla powitania po raz pierwszy, upewnij się, na ekranie powitania dostosować Python 2.7.13 wybranym **dodać python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Zrzut ekranu przedstawiający ekran Dostosowywanie środowiska Python 2.7.11 hello, których należy tooselect Add python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="f2d82-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="f2d82-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="f2d82-132">Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f2d82-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f2d82-133">Zacznijmy od utworzenia konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f2d82-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="f2d82-134">Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: Tworzenie nowej aplikacji sieci web platformy Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="f2d82-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="f2d82-135">Teraz przejdziemy przez jak toocreate nowej aplikacji sieci web platformy Python Flask od hello tła w.</span><span class="sxs-lookup"><span data-stu-id="f2d82-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="f2d82-136">Krok 2. Tworzenie nowej aplikacji sieci Web platformy Python Flask</span><span class="sxs-lookup"><span data-stu-id="f2d82-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="f2d82-137">W programie Visual Studio na powitania **pliku** menu punktu zbyt**nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="f2d82-138">Witaj **nowy projekt** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f2d82-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="f2d82-139">W okienku po lewej stronie powitania, rozwiń węzeł **szablony** , a następnie **Python**, a następnie kliknij przycisk **Web**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="f2d82-140">Wybierz **projektu sieci Web platformy Flask** hello środkowym okienku, a następnie w hello **nazwa** wpisz **samouczek**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="f2d82-141">Pamiętaj, że nazwy pakietów języka Python powinny być tylko małe litery, zgodnie z opisem w hello [Przewodnik po stylu kodu Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="f2d82-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="f2d82-142">Te nowe tooPython Flask jest platforma programistyczna aplikacji sieci web, ułatwiające szybsze tworzenie aplikacji sieci web w języku Python.</span><span class="sxs-lookup"><span data-stu-id="f2d82-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Zrzut ekranu okna nowy projekt hello w programie Visual Studio wyróżnione na powitania po lewej, projekt sieci Web platformy Flask Python wybrany w środku hello i hello nazwą tutorial w polu Nazwa hello języka Python](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="f2d82-144">W hello **narzędzi Python Tools for Visual Studio** okna, kliknij przycisk **zainstalować w środowisku wirtualnym**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Zrzut ekranu samouczka bazy danych hello — narzędzia Python Tools for Visual Studio okna](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="f2d82-146">W hello **Dodawanie środowiska wirtualnego** okna, można zaakceptować ustawienia domyślne hello i użyć środowiska Python 2.7 jako podstawowego środowiska hello, ponieważ pakiet PyDocumentDB nie obsługuje obecnie środowiska Python 3.x, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="f2d82-147">Konfiguruje środowisko wirtualne języka Python hello wymagane dla projektu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Zrzut ekranu samouczka bazy danych hello — narzędzia Python Tools for Visual Studio okna](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="f2d82-149">Wyświetla okno danych wyjściowych Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` po pomyślnym zainstalowaniu środowiska hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="f2d82-150">Krok 3: Modyfikowanie aplikacji sieci web platformy Python Flask hello</span><span class="sxs-lookup"><span data-stu-id="f2d82-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="f2d82-151">Dodaj projekt tooyour pakietów platformy Python Flask hello</span><span class="sxs-lookup"><span data-stu-id="f2d82-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="f2d82-152">Po skonfigurowaniu projektu musisz tooadd hello wymagane Flask pakiety tooyour projektu, w tym pydocumentdb — pakiet języka Python hello usługi documentdb.</span><span class="sxs-lookup"><span data-stu-id="f2d82-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="f2d82-153">W Eksploratorze rozwiązań Otwórz plik hello o nazwie **requirements.txt** i Zastąp zawartość hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2d82-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
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
2. <span data-ttu-id="f2d82-154">Zapisz hello **requirements.txt** pliku.</span><span class="sxs-lookup"><span data-stu-id="f2d82-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="f2d82-155">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **env**, a następnie kliknij polecenie **Zainstaluj z pliku requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Zrzut ekranu przedstawiający env (Python 2.7) wybrany w ramach instalacji z pliku requirements.txt wyróżnione na liście hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="f2d82-157">Po pomyślnej instalacji okno danych wyjściowych hello wyświetla następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f2d82-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="f2d82-158">W rzadkich przypadkach można napotkać błąd w oknie danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="f2d82-159">W takim przypadku należy sprawdzić, czy błąd hello jest toocleanup powiązane.</span><span class="sxs-lookup"><span data-stu-id="f2d82-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="f2d82-160">Czasami Oczyszczanie hello nie powiedzie się, ale hello instalacja zakończy się pomyślnie (Przewiń w górę tooverify okno danych wyjściowych hello to).</span><span class="sxs-lookup"><span data-stu-id="f2d82-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="f2d82-161">Można sprawdzić instalację przez [środowiska wirtualnego hello weryfikacji](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="f2d82-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="f2d82-162">Jeśli hello instalacja nie powiodła się, ale hello weryfikacja zakończy się pomyślnie, jest OK toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f2d82-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="f2d82-163">Sprawdź hello środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="f2d82-163">Verify hello virtual environment</span></span>
<span data-ttu-id="f2d82-164">Upewnijmy się, że wszystko jest poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="f2d82-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="f2d82-165">Utworzenie rozwiązania hello naciskając **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="f2d82-166">Po pomyślnym hello kompilacji, należy uruchomić hello witryny sieci Web, naciskając **F5**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="f2d82-167">To spowoduje uruchomienie serwera programistycznego platformy Flask hello i uruchomi przeglądarkę sieci web.</span><span class="sxs-lookup"><span data-stu-id="f2d82-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="f2d82-168">Powinny pojawić się po stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="f2d82-168">You should see hello following page.</span></span>
   
    ![Witaj pusty platformy Python Flask projekt aplikacji sieci web wyświetlany w przeglądarce](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="f2d82-170">Zatrzymaj debugowanie hello witryny sieci Web, naciskając klawisz **Shift**+**F5** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2d82-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="f2d82-171">Tworzenie definicji bazy danych, kolekcji i dokumentu</span><span class="sxs-lookup"><span data-stu-id="f2d82-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="f2d82-172">Teraz utwórzmy aplikację do głosowania przez dodanie nowych plików i zaktualizowanie pozostałych.</span><span class="sxs-lookup"><span data-stu-id="f2d82-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="f2d82-173">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **samouczek** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="f2d82-174">Wybierz **pusty plik Python** i nazwa pliku hello **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="f2d82-175">Dodaj hello następującego pliku forms.py toohello kodu, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="f2d82-176">Dodaj hello wymaganych importów tooviews.py</span><span class="sxs-lookup"><span data-stu-id="f2d82-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="f2d82-177">W Eksploratorze rozwiązań rozwiń hello **samouczek** folderu, a następnie otwórz hello **views.py** pliku.</span><span class="sxs-lookup"><span data-stu-id="f2d82-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="f2d82-178">Dodaj następujące instrukcje importu toohello góry hello hello **views.py** pliku, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="f2d82-179">Te zaimportowane spowoduje DB rozwiązania Cosmos i hello pakietów platformy Flask.</span><span class="sxs-lookup"><span data-stu-id="f2d82-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="f2d82-180">Tworzenie bazy danych, kolekcji i dokumentu</span><span class="sxs-lookup"><span data-stu-id="f2d82-180">Create database, collection, and document</span></span>
* <span data-ttu-id="f2d82-181">Nadal **views.py**, Dodaj hello kod zakończenia toohello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="f2d82-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="f2d82-182">Odpowiada on za tworzenie hello bazy danych używane przez hello formularza.</span><span class="sxs-lookup"><span data-stu-id="f2d82-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="f2d82-183">Nie usuwaj żadnego kodu istniejących hello w **views.py**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="f2d82-184">Po prostu Dołącz toohello temu elementowi end.</span><span class="sxs-lookup"><span data-stu-id="f2d82-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="f2d82-185">Odczytywanie bazy danych, kolekcji i dokumentów oraz przesyłanie formularza</span><span class="sxs-lookup"><span data-stu-id="f2d82-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="f2d82-186">Nadal **views.py**, Dodaj hello kod zakończenia toohello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="f2d82-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="f2d82-187">Odpowiada on za konfigurowanie formularza hello, odczytywanie hello bazy danych, kolekcji i dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="f2d82-188">Nie usuwaj żadnego kodu istniejących hello w **views.py**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="f2d82-189">Po prostu Dołącz toohello temu elementowi end.</span><span class="sxs-lookup"><span data-stu-id="f2d82-189">Simply append this toohello end.</span></span>

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

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
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


### <a name="create-hello-html-files"></a><span data-ttu-id="f2d82-190">Utwórz hello pliki HTML</span><span class="sxs-lookup"><span data-stu-id="f2d82-190">Create hello HTML files</span></span>
1. <span data-ttu-id="f2d82-191">W Eksploratorze rozwiązań w hello **samouczek** powitania kliknij folder prawym **szablony** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="f2d82-192">Wybierz **strony HTML**, a następnie wpisz nazwę hello **create.html**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="f2d82-193">Powtórz kroki 1 i 2 toocreate dwa dodatkowe pliki HTML: results.html i vote.html.</span><span class="sxs-lookup"><span data-stu-id="f2d82-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="f2d82-194">Dodaj hello zbyt następującego kodu**create.html** w hello `<body>` elementu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="f2d82-195">Służy do wyświetlania komunikatu informującego o tym, że utworzyliśmy nową bazę danych, kolekcję i dokument.</span><span class="sxs-lookup"><span data-stu-id="f2d82-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="f2d82-196">Dodaj hello zbyt następującego kodu**results.html** w hello `<body`> elementu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="f2d82-197">Wyświetla wyniki hello hello sondowania.</span><span class="sxs-lookup"><span data-stu-id="f2d82-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
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
6. <span data-ttu-id="f2d82-198">Dodaj hello zbyt następującego kodu**vote.html** w hello `<body`> elementu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="f2d82-199">On wyświetla hello sondowania i akceptuje hello głosów.</span><span class="sxs-lookup"><span data-stu-id="f2d82-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="f2d82-200">Po zarejestrowaniu głosów hello, hello kontrola jest przekazywana tooviews.py gdzie możemy rozpozna hello głos jest rozpoznawany i odpowiednio Dołącz hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f2d82-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="f2d82-201">W hello **szablony** folderu, Zastąp zawartość hello **index.html** następujący hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="f2d82-202">Służy to jako hello początkowej strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2d82-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="f2d82-203">Dodaj plik konfiguracji i zmień hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="f2d82-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="f2d82-204">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **samouczek** projektu, kliknij przycisk **Dodaj**, kliknij przycisk **nowy element**, wybierz pozycję **pusty plik Python**, a następnie Nazwa pliku hello **config.py**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="f2d82-205">Ten plik konfiguracji jest wymagany przez formularze na platformie Flask.</span><span class="sxs-lookup"><span data-stu-id="f2d82-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="f2d82-206">Służy on tooprovide także klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="f2d82-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="f2d82-207">Ten klucz nie jest jednak potrzebny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="f2d82-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="f2d82-208">Dodaj następujące hello tooconfig.py kodu, musisz tooalter hello wartości **DOCUMENTDB\_hosta** i **DOCUMENTDB\_klucza** w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="f2d82-209">W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **klucze** bloku, klikając **Przeglądaj**, **kont DB rozwiązania Cosmos Azure**, kliknij dwukrotnie nazwę hello z hello toouse konta, a następnie kliknij przycisk hello **klucze** przycisku na powitania **Essentials** obszaru.</span><span class="sxs-lookup"><span data-stu-id="f2d82-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="f2d82-210">W hello **klucze** bloku, hello kopiowania **URI** wartość i wklej go do hello **config.py** pliku jako wartość hello hello **DOCUMENTDB\_hosta**  właściwości.</span><span class="sxs-lookup"><span data-stu-id="f2d82-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="f2d82-211">W portalu Azure w hello hello **klucze** bloku kopia wartość hello hello **klucza podstawowego** lub hello **klucza pomocniczego**i wklej go do hello **config.py**  pliku jako wartość hello hello **DOCUMENTDB\_klucza** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f2d82-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="f2d82-212">W hello  **\_ \_init\_\_.py** plików, dodawanie hello następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="f2d82-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="f2d82-213">Tak, aby zawartość pliku hello hello jest:</span><span class="sxs-lookup"><span data-stu-id="f2d82-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="f2d82-214">Po dodaniu wszystkich plików hello, Eksplorator rozwiązań powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="f2d82-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Zrzut ekranu przedstawiający okno programu Visual Studio Solution Explorer hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="f2d82-216">Krok 4. Uruchamianie aplikacji sieci Web lokalnie</span><span class="sxs-lookup"><span data-stu-id="f2d82-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="f2d82-217">Utworzenie rozwiązania hello naciskając **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="f2d82-218">Po pomyślnym hello kompilacji, należy uruchomić hello witryny sieci Web, naciskając **F5**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="f2d82-219">Następujące hello powinny zostać wyświetlone na ekranie.</span><span class="sxs-lookup"><span data-stu-id="f2d82-219">You should see hello following on your screen.</span></span>
   
    ![Zrzut ekranu przedstawiający Witaj Python + Azure rozwiązania Cosmos głosowania aplikacji DB wyświetlany w przeglądarce sieci web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="f2d82-221">Kliknij przycisk **Utwórz/wyczyść hello głosowania bazy danych** toogenerate hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f2d82-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Zrzut ekranu przedstawiający hello strony tworzenia aplikacji sieci web hello — szczegóły programowania](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="f2d82-223">Następnie kliknij przycisk **Vote** (Głosuj) i wybierz jedną z opcji.</span><span class="sxs-lookup"><span data-stu-id="f2d82-223">Then, click **Vote** and select your option.</span></span>
   
    ![Zrzut ekranu przedstawiający hello aplikacji sieci web z pytaniem, które należy udzielić odpowiedzi](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="f2d82-225">Dla każdego oddany głos powoduje zwiększenie odpowiedniego licznika hello.</span><span class="sxs-lookup"><span data-stu-id="f2d82-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Zrzut ekranu przedstawiający hello wyniki wyświetlane stronie głosowania hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="f2d82-227">Zatrzymaj debugowanie projektu hello, naciskając klawisz Shift + F5.</span><span class="sxs-lookup"><span data-stu-id="f2d82-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="f2d82-228">Krok 5: Wdrożenie tooAzure aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="f2d82-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="f2d82-229">Teraz, gdy masz hello kompletna aplikacja działa poprawnie z rozwiązania Cosmos DB zamierzamy toodeploy to tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f2d82-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="f2d82-230">Kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań (Upewnij się, że nie masz uruchomiony lokalnie) i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Zrzut ekranu samouczka hello zaznaczone w Eksploratorze rozwiązań z wyróżnioną opcją publikowania hello](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="f2d82-232">W hello **publikowania** okno dialogowe, wybierz opcję **Microsoft Azure App Service**, wybierz pozycję **Utwórz nowy**, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Zrzut ekranu okna publikowanie w sieci Web hello z wyróżnionym programem Microsoft Azure App Service](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="f2d82-234">W hello **Tworzenie usługi App Service** okna dialogowego wprowadź nazwę powitania dla aplikacji sieci web, wraz z Twojej **subskrypcji**, **grupy zasobów**, i **planu usługi App Service** , następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f2d82-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Zrzut ekranu okna hello okno aplikacji sieci Web programu Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="f2d82-236">W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji usługi i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="f2d82-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Zrzut ekranu okna hello okno aplikacji sieci Web programu Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="f2d82-238">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f2d82-238">Troubleshooting</span></span>
<span data-ttu-id="f2d82-239">Jeśli jest to hello na komputerze uruchomiono pierwszej aplikacji Python, upewnij się, następujących hello foldery (lub hello odpowiadające im lokalizacje instalacji) są uwzględnione w zmiennej PATH:</span><span class="sxs-lookup"><span data-stu-id="f2d82-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="f2d82-240">Jeśli wystąpi błąd na stronie głosowania, a nazwa projektu jest coś innego niż **samouczek**, upewnij się, że  **\_ \_init\_\_.py** Popraw nazwę projektu w wierszu hello hello odwołania: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="f2d82-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2d82-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2d82-241">Next steps</span></span>
<span data-ttu-id="f2d82-242">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="f2d82-242">Congratulations!</span></span> <span data-ttu-id="f2d82-243">Ma wystarczy wykonać swoją pierwszą aplikację sieci web języka Python za pomocą rozwiązania Cosmos bazy danych i opublikować ją tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f2d82-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="f2d82-244">Często aktualizujemy i poprawiamy ten temat na podstawie opinii czytelników.</span><span class="sxs-lookup"><span data-stu-id="f2d82-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="f2d82-245">Po ukończeniu samouczka hello, należy za pomocą hello głosowania przyciski na powitania góry i u dołu tej strony oraz być tooinclude się swoją opinię na jakie ulepszenia ma toosee wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="f2d82-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="f2d82-246">Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.</span><span class="sxs-lookup"><span data-stu-id="f2d82-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="f2d82-247">Aplikacja sieci web tooyour tooadd dodatkowe funkcje, przejrzyj hello interfejsami API dostępnymi w hello [Azure rozwiązania Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="f2d82-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="f2d82-248">Aby uzyskać więcej informacji na temat platformy Azure, programu Visual Studio i języka Python, zobacz hello [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f2d82-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="f2d82-249">Aby uzyskać dodatkowe samouczki platformy Python Flask, zobacz [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="f2d82-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
