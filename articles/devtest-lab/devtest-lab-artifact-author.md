---
title: niestandardowe artefakty aaaCreate dla maszyny Wirtualnej DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooauthor własne artefaktów dla za pomocą DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="e51bf-103">Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e51bf-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="e51bf-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e51bf-104">Overview</span></span>
<span data-ttu-id="e51bf-105">**Artefakty** są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e51bf-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="e51bf-106">Artefakt składa się z plikiem definicji artefaktów i innych plików skryptów, które są przechowywane w folderze w repozytorium git.</span><span class="sxs-lookup"><span data-stu-id="e51bf-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="e51bf-107">Pliki definicji artefaktów składają się z kodu JSON i wyrażeń, których można używać toospecify co chcesz tooinstall na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e51bf-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="e51bf-108">Na przykład można zdefiniować nazwę hello artefaktu, toorun poleceń i parametrów, które są dostępne po uruchomieniu polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="e51bf-109">Może się odwoływać tooother plików skryptów w pliku definicji artefaktów hello według nazwy.</span><span class="sxs-lookup"><span data-stu-id="e51bf-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="e51bf-110">Format pliku definicji artefaktów</span><span class="sxs-lookup"><span data-stu-id="e51bf-110">Artifact definition file format</span></span>
<span data-ttu-id="e51bf-111">Witaj poniższy przykład przedstawia hello sekcje, które tworzą hello podstawowej struktury pliku definicji:</span><span class="sxs-lookup"><span data-stu-id="e51bf-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="e51bf-112">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e51bf-112">Element name</span></span> | <span data-ttu-id="e51bf-113">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="e51bf-113">Required?</span></span> | <span data-ttu-id="e51bf-114">Opis</span><span class="sxs-lookup"><span data-stu-id="e51bf-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e51bf-115">$schema</span><span class="sxs-lookup"><span data-stu-id="e51bf-115">$schema</span></span> |<span data-ttu-id="e51bf-116">Nie</span><span class="sxs-lookup"><span data-stu-id="e51bf-116">No</span></span> |<span data-ttu-id="e51bf-117">Lokalizacja pliku hello schematu JSON, który ułatwia testowanie hello ważności hello pliku definicji.</span><span class="sxs-lookup"><span data-stu-id="e51bf-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="e51bf-118">Tytuł</span><span class="sxs-lookup"><span data-stu-id="e51bf-118">title</span></span> |<span data-ttu-id="e51bf-119">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-119">Yes</span></span> |<span data-ttu-id="e51bf-120">Nazwa wyświetlana w laboratorium hello artefaktu hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="e51bf-121">description</span><span class="sxs-lookup"><span data-stu-id="e51bf-121">description</span></span> |<span data-ttu-id="e51bf-122">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-122">Yes</span></span> |<span data-ttu-id="e51bf-123">Opis wyświetlany w laboratorium hello artefaktu hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="e51bf-124">Identyfikator iconUri</span><span class="sxs-lookup"><span data-stu-id="e51bf-124">iconUri</span></span> |<span data-ttu-id="e51bf-125">Nie</span><span class="sxs-lookup"><span data-stu-id="e51bf-125">No</span></span> |<span data-ttu-id="e51bf-126">Identyfikator URI ikony hello wyświetlany w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="e51bf-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="e51bf-127">targetOsType</span></span> |<span data-ttu-id="e51bf-128">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-128">Yes</span></span> |<span data-ttu-id="e51bf-129">System operacyjny hello zainstalowanym artefaktu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e51bf-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="e51bf-130">Są obsługiwane opcje: systemu Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="e51bf-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="e51bf-131">parameters</span><span class="sxs-lookup"><span data-stu-id="e51bf-131">parameters</span></span> |<span data-ttu-id="e51bf-132">Nie</span><span class="sxs-lookup"><span data-stu-id="e51bf-132">No</span></span> |<span data-ttu-id="e51bf-133">Wartości, które znajdują się po uruchomieniu polecenia install artefaktów na maszynie.</span><span class="sxs-lookup"><span data-stu-id="e51bf-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="e51bf-134">Pomaga to w Dostosowywanie Twojej artefaktu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="e51bf-135">UruchomPolecenie</span><span class="sxs-lookup"><span data-stu-id="e51bf-135">runCommand</span></span> |<span data-ttu-id="e51bf-136">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-136">Yes</span></span> |<span data-ttu-id="e51bf-137">Artefaktu zainstalować polecenia, która jest wykonywana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e51bf-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="e51bf-138">Parametry artefaktów</span><span class="sxs-lookup"><span data-stu-id="e51bf-138">Artifact parameters</span></span>
<span data-ttu-id="e51bf-139">W sekcji parametrów hello pliku definicji hello należy określić wartości, które użytkownik może wprowadzić podczas instalowania artefaktów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="e51bf-140">Może się odwoływać wartości toothese polecenia install hello artefaktu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="e51bf-141">Definiuje parametry z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="e51bf-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="e51bf-142">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e51bf-142">Element name</span></span> | <span data-ttu-id="e51bf-143">Wymagana?</span><span class="sxs-lookup"><span data-stu-id="e51bf-143">Required?</span></span> | <span data-ttu-id="e51bf-144">Opis</span><span class="sxs-lookup"><span data-stu-id="e51bf-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e51bf-145">type</span><span class="sxs-lookup"><span data-stu-id="e51bf-145">type</span></span> |<span data-ttu-id="e51bf-146">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-146">Yes</span></span> |<span data-ttu-id="e51bf-147">Typ wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="e51bf-147">Type of parameter value.</span></span> <span data-ttu-id="e51bf-148">Zobacz hello następujące listy hello dozwolone typy:</span><span class="sxs-lookup"><span data-stu-id="e51bf-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="e51bf-149">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="e51bf-149">displayName</span></span> |<span data-ttu-id="e51bf-150">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-150">Yes</span></span> |<span data-ttu-id="e51bf-151">Nazwa parametru hello, który jest użytkownikiem tooa wyświetlanych w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="e51bf-152">description</span><span class="sxs-lookup"><span data-stu-id="e51bf-152">description</span></span> |<span data-ttu-id="e51bf-153">Tak</span><span class="sxs-lookup"><span data-stu-id="e51bf-153">Yes</span></span> |<span data-ttu-id="e51bf-154">Opis parametru hello, który jest wyświetlany w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="e51bf-155">Witaj dozwolone typy to:</span><span class="sxs-lookup"><span data-stu-id="e51bf-155">hello allowed types are:</span></span>

* <span data-ttu-id="e51bf-156">String — dowolny prawidłowy ciąg JSON</span><span class="sxs-lookup"><span data-stu-id="e51bf-156">string – any valid JSON string</span></span>
* <span data-ttu-id="e51bf-157">int — dowolną prawidłową liczbą całkowitą JSON</span><span class="sxs-lookup"><span data-stu-id="e51bf-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="e51bf-158">bool — wszystkie prawidłowe JSON logiczna</span><span class="sxs-lookup"><span data-stu-id="e51bf-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="e51bf-159">Array — nieprawidłowy tablicy JSON</span><span class="sxs-lookup"><span data-stu-id="e51bf-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="e51bf-160">Artefaktu wyrażeń i funkcji</span><span class="sxs-lookup"><span data-stu-id="e51bf-160">Artifact expressions and functions</span></span>
<span data-ttu-id="e51bf-161">Można użyć wyrażenia i funkcje tooconstruct hello artefaktu polecenie instalacji.</span><span class="sxs-lookup"><span data-stu-id="e51bf-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="e51bf-162">Wyrażenia są ujęte w nawiasy kwadratowe ([i]) i są oceniane po zainstalowaniu hello artefaktu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="e51bf-163">Wyrażenia mogą występować w dowolnym miejscu w wartości ciągu JSON i zawsze zwracają inną wartość JSON.</span><span class="sxs-lookup"><span data-stu-id="e51bf-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="e51bf-164">Jeśli potrzebujesz toouse literałem, która rozpoczyna się od nawiasu [, należy użyć dwóch nawiasy kwadratowe [[.</span><span class="sxs-lookup"><span data-stu-id="e51bf-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="e51bf-165">Zwykle używanie wyrażeń z tooconstruct funkcji wartości.</span><span class="sxs-lookup"><span data-stu-id="e51bf-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="e51bf-166">Podobnie jak w języku JavaScript, wywołania funkcji są sformatowane jako functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="e51bf-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="e51bf-167">Witaj Poniższa lista zawiera typowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="e51bf-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="e51bf-168">parameters(parameterName) — zwraca wartość parametru jest dostępne po uruchomieniu polecenia artefaktu hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="e51bf-169">concat (arg1, arg2, arg3,...) - łączy wiele wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="e51bf-170">Ta funkcja może być dowolną liczbę argumentów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="e51bf-171">powitania po przykładzie pokazano, jak toouse wyrażeń i funkcji tooconstruct wartość:</span><span class="sxs-lookup"><span data-stu-id="e51bf-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="e51bf-172">Tworzenie niestandardowych artefaktów</span><span class="sxs-lookup"><span data-stu-id="e51bf-172">Create a custom artifact</span></span>
<span data-ttu-id="e51bf-173">Utwórz użytkownika niestandardowego artefaktu wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e51bf-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="e51bf-174">Zainstaluj edytor JSON — należy toowork Edytor JSON z plików definicji artefaktów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="e51bf-175">Firma Microsoft zaleca używanie [Visual Studio Code](https://code.visualstudio.com/), która jest dostępna dla systemu Windows, Linux i OS X.</span><span class="sxs-lookup"><span data-stu-id="e51bf-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="e51bf-176">Get artifactfile.json próbki - wyewidencjonowanie artefakty hello utworzone przez zespół Azure DevTest Labs na naszych [repozytorium GitHub](https://github.com/Azure/azure-devtestlab), w którym utworzono rozbudowane biblioteki artefaktów, które ułatwiają tworzenie własnych artefaktów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="e51bf-177">Pobierz plik definicji artefaktów i upewnić toocreate tooit zmiany własne artefaktów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="e51bf-178">Upewnij się, użyj IntelliSense — IntelliSense wykorzystać toosee prawidłowe elementy, które mogą być używane tooconstruct pliku definicji artefaktów.</span><span class="sxs-lookup"><span data-stu-id="e51bf-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="e51bf-179">Można również sprawdzić hello różnych opcji dla wartości elementu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="e51bf-180">Na przykład Pokaż IntelliSense Witaj dwie możliwości systemu Windows lub Linux, edytując hello **targetOsType** elementu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="e51bf-181">Magazyn artefaktów hello w [repozytorium git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e51bf-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="e51bf-182">Utwórz oddzielne katalog dla każdego artefaktu, gdzie nazwa katalogu hello jest hello takie same jak nazwa artefaktu hello.</span><span class="sxs-lookup"><span data-stu-id="e51bf-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="e51bf-183">Magazyn hello artefaktu definicji (artifactfile.json) w katalogu hello utworzonego pliku.</span><span class="sxs-lookup"><span data-stu-id="e51bf-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="e51bf-184">Polecenie instalacji magazynu hello skrypty, które są przywoływane z hello artefaktu.</span><span class="sxs-lookup"><span data-stu-id="e51bf-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="e51bf-185">Oto przykład może wyglądać folderu artefaktu:</span><span class="sxs-lookup"><span data-stu-id="e51bf-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Przykład repozytorium git artefaktów](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="e51bf-187">Dodawanie laboratorium toohello repozytorium artefaktów hello — można znaleźć w artykule toohello [dodać repozytorium Git artefakty i szablony](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e51bf-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="e51bf-188">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="e51bf-188">Related articles</span></span>
* [<span data-ttu-id="e51bf-189">Jak toodiagnose artefaktu błędów w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e51bf-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="e51bf-190">Dołącz do maszyny Wirtualnej tooexisting domeny AD przy użyciu szablonu usługi resource manager w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e51bf-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="e51bf-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e51bf-191">Next steps</span></span>
* <span data-ttu-id="e51bf-192">Dowiedz się, jak za[Dodawanie laboratorium tooa repozytorium artefaktów Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e51bf-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

