---
title: "Szablon usługi Azure Resource Manager aaaExport | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager tooexport szablon z istniejącej grupy zasobów."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="9c6de-103">Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów</span><span class="sxs-lookup"><span data-stu-id="9c6de-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="9c6de-104">W tym artykule dowiesz się, jak tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="9c6de-105">Możesz użyć tego toogain wygenerowanego szablonu lepszego zrozumienia składni szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="9c6de-106">Istnieją dwa sposoby tooexport szablonu:</span><span class="sxs-lookup"><span data-stu-id="9c6de-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="9c6de-107">Możesz wyeksportować hello **rzeczywiste szablon używany do wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="9c6de-108">Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="9c6de-109">Takie podejście jest przydatne podczas wdrażania zasobów za pośrednictwem portalu hello i mają toosee hello szablonu toocreate tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="9c6de-110">Ten szablon jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-110">This template is readily usable.</span></span> 
* <span data-ttu-id="9c6de-111">Możesz wyeksportować **wygenerowane z szablonu, która reprezentuje bieżący stan grupy zasobów hello hello**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="9c6de-112">Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="9c6de-113">Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="9c6de-114">Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="9c6de-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="9c6de-115">Takie rozwiązanie jest przydatne, gdy hello grupy zasobów zostały zmodyfikowane po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="9c6de-116">Taki szablon zwykle wymaga modyfikacji, zanim będzie go można użyć.</span><span class="sxs-lookup"><span data-stu-id="9c6de-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="9c6de-117">W tym temacie przedstawiono oba podejścia za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="9c6de-118">Wdrażanie zasobów</span><span class="sxs-lookup"><span data-stu-id="9c6de-118">Deploy resources</span></span>
<span data-ttu-id="9c6de-119">Zacznijmy od wdrażania tooAzure zasobów, używanej do eksportowania jako szablon.</span><span class="sxs-lookup"><span data-stu-id="9c6de-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="9c6de-120">Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport tooa szablonu, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9c6de-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="9c6de-121">Witaj dalszej części tego artykułu przyjęto założenie, że wdrożono hello aplikacji sieci web i rozwiązanie bazy danych SQL w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="9c6de-122">Jeśli używasz inne rozwiązanie środowiska mogą się nieco różnić, ale są tooexport szablon czynności hello hello takie same.</span><span class="sxs-lookup"><span data-stu-id="9c6de-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="9c6de-123">W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![wybieranie nowego elementu](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="9c6de-125">Wyszukaj **aplikacja sieci web i SQL** i wybierz ją z hello dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![wyszukiwanie aplikacji internetowej i bazy danych SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="9c6de-127">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-127">Select **Create**.</span></span>

      ![wybieranie pozycji Utwórz](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="9c6de-129">Podaj wartości wymagane hello hello aplikacji sieci web i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9c6de-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="9c6de-130">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-130">Select **Create**.</span></span>

      ![podawanie wartości dla aplikacji internetowej i bazy danych SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="9c6de-132">Witaj wdrożenia może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9c6de-132">hello deployment may take a minute.</span></span> <span data-ttu-id="9c6de-133">Po zakończeniu wdrożenia hello subskrypcja zawiera hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9c6de-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="9c6de-134">Wyświetlanie szablonu z historii wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9c6de-134">View template from deployment history</span></span>
1. <span data-ttu-id="9c6de-135">Przejdź toohello bloku grupy zasobów dla nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="9c6de-136">Należy zauważyć, że tego bloku hello przedstawia wynik hello hello ostatniego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="9c6de-137">Wybierz ten link.</span><span class="sxs-lookup"><span data-stu-id="9c6de-137">Select this link.</span></span>
   
      ![blok grupy zasobów](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="9c6de-139">Zostanie wyświetlona historia wdrożeń dla grupy hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="9c6de-140">W Twoim przypadku bloku hello wymieniono prawdopodobnie tylko jedno wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="9c6de-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="9c6de-141">Wybierz to wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="9c6de-141">Select this deployment.</span></span>
   
     ![ostatnie wdrożenie](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="9c6de-143">Blok Hello Wyświetla podsumowanie hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="9c6de-144">Hello Podsumowanie zawiera stan hello hello wdrożenia i jego operacji oraz wartości hello, które podany dla parametrów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="9c6de-145">używany dla wdrożenia hello, wybierz szablon hello toosee **Wyświetl szablon**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![wyświetlanie podsumowania wdrożenia](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="9c6de-147">Usługa Resource Manager pobiera hello czynności siedem plików:</span><span class="sxs-lookup"><span data-stu-id="9c6de-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="9c6de-148">**Szablon** -hello szablonu, który definiuje infrastrukturę Twojego rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="9c6de-149">Po utworzeniu konta magazynu hello za pośrednictwem portalu hello Resource Manager używany toodeploy szablonu go i zapisała ten szablon do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9c6de-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="9c6de-150">**Parametry** -pliku parametrów czy toopass można użyć w wartości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9c6de-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="9c6de-151">Zawiera wartości hello, które podane podczas pierwszego wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="9c6de-152">Podczas ponownego wdrażania szablonu hello można zmienić dowolne z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9c6de-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="9c6de-153">**Interfejs wiersza polecenia** -Azure polecenia wiersza interfejsu (CLI) pliku skryptu służy toodeploy hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="9c6de-154">**Interfejs wiersza polecenia 2.0** -Azure polecenia wiersza interfejsu (CLI) pliku skryptu służy toodeploy hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="9c6de-155">**PowerShell** — czy toodeploy hello szablonu można użyć pliku skryptu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c6de-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="9c6de-156">**.NET** -służy toodeploy hello szablonu klasy A .NET.</span><span class="sxs-lookup"><span data-stu-id="9c6de-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="9c6de-157">**Ruby** -klasy A Ruby służy toodeploy hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="9c6de-158">pliki Hello są dostępne za pośrednictwem łącza między hello bloku.</span><span class="sxs-lookup"><span data-stu-id="9c6de-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="9c6de-159">Domyślnie bloku hello Wyświetla szablon hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-159">By default, hello blade displays hello template.</span></span>
      
       ![wyświetlanie szablonu](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="9c6de-161">Ten szablon jest rzeczywista szablonu hello używanych toocreate aplikacji sieci web i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9c6de-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="9c6de-162">Należy zauważyć, że zawiera on parametry umożliwiające tooprovide różne wartości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9c6de-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="9c6de-163">toolearn więcej informacji na temat struktury hello szablonu, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9c6de-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="9c6de-164">Eksportowanie szablonu hello z grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="9c6de-164">Export hello template from resource group</span></span>
<span data-ttu-id="9c6de-165">Jeśli ręcznie zmienić zasoby lub dodać zasoby w wielu wdrożeń, pobieranie szablonu z historii wdrożenia hello nie odzwierciedlały bieżący stan hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="9c6de-166">W tej sekcji przedstawiono, jak tooexport szablonu, które odzwierciedla hello bieżący stan hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c6de-167">Nie można eksportować szablonu dla grupy zasobów zawierającej ponad 200 zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="9c6de-168">tooview hello szablonu dla grupy zasobów, wybierz opcję **skryptu automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![eksportowanie grupy zasobów](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="9c6de-170">Menedżer zasobów szacuje hello zasoby w grupie zasobów hello oraz generuje szablon dla tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="9c6de-171">Nie wszystkie typy zasobów obsługują hello eksportowania szablonu funkcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="9c6de-172">Może zostać wyświetlony komunikat o błędzie informujący, że istnieje problem z hello eksportu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="9c6de-173">Dowiedz się, jak toohandle tych problemów w hello [kwestie związane z eksportem poprawka](#fix-export-issues) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="9c6de-174">Ponownie Zobacz pliki sześciu hello służy tooredeploy hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9c6de-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="9c6de-175">Jednak ten czas hello szablon jest nieco inne.</span><span class="sxs-lookup"><span data-stu-id="9c6de-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="9c6de-176">Należy zauważyć, że hello wygenerowanego szablonu zawiera parametry mniej niż szablon hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="9c6de-177">Ponadto wiele hello wartości (takie jak lokalizacja i wartości jednostki SKU) jest ustalony w tym szablonie, a nie przyjmuje wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="9c6de-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="9c6de-178">Przed ponownym tego szablonu, może zaistnieć tooedit hello szablonu toomake lepiej wykorzystać parametrów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="9c6de-179">Masz kilka opcji dla dalszego toowork przy użyciu tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="9c6de-180">Można pobrać szablonu hello i na nim pracować lokalnie za pomocą edytora JSON.</span><span class="sxs-lookup"><span data-stu-id="9c6de-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="9c6de-181">Lub można zapisać hello szablonu tooyour biblioteki i pracy z nim za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="9c6de-182">Jeśli potrafisz za pomocą edytora JSON, takich jak [kodzie VS](https://code.visualstudio.com/) lub [programu Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), można wybrać Pobieranie szablonu hello lokalnie i za pomocą tego edytora.</span><span class="sxs-lookup"><span data-stu-id="9c6de-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="9c6de-183">toowork lokalnie, wybierz opcję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-183">toowork locally, select **Download**.</span></span>
   
      ![pobieranie szablonu](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="9c6de-185">Jeśli nie są skonfigurowane za pomocą edytora JSON można wybrać edycji szablonu hello za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="9c6de-186">Witaj pozostałej części tematu przyjęto założenie, że biblioteka tooyour szablonów hello zostały zapisane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="9c6de-187">Ważne jest, aby hello sama składnia zmienia toohello szablonu, czy działa lokalnie za pomocą edytora JSON lub za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="9c6de-188">Wybierz toowork za pośrednictwem portalu hello **dodać toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![Dodaj toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="9c6de-190">Podczas dodawania biblioteki toohello szablonów, należy nadać szablonowi hello nazwę i opis.</span><span class="sxs-lookup"><span data-stu-id="9c6de-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="9c6de-191">Następnie wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-191">Then, select **Save**.</span></span>
   
     ![ustawianie wartości szablonu](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="9c6de-193">tooview szablonu zapisana w bibliotece, wybierz **więcej usług**, typ **szablony** toofilter wyniki, wybierz opcję **szablony**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![znajdowanie szablonów](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="9c6de-195">Wybierz szablon hello o nazwie hello, który został zapisany.</span><span class="sxs-lookup"><span data-stu-id="9c6de-195">Select hello template with hello name you saved.</span></span>
   
      ![wybieranie szablonu](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="9c6de-197">Dostosowywanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="9c6de-197">Customize hello template</span></span>
<span data-ttu-id="9c6de-198">Hello wyeksportowany szablon działa poprawnie, jeśli chcesz toocreate hello sam sieci web aplikacji i bazy danych SQL dla każdego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="9c6de-199">Usługa Resource Manager oferuje jednak opcje, dzięki którym można wdrażać szablony ze znacznie większą elastycznością.</span><span class="sxs-lookup"><span data-stu-id="9c6de-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="9c6de-200">W tym artykule opisano, jak parametry tooadd hello bazy danych, nazwę i hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="9c6de-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="9c6de-201">Można użyć tego samego tooadd podejście większą elastyczność i innych wartości na powitania szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="9c6de-202">toocustomize hello szablonu, wybierz opcję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![wyświetlanie szablonu](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="9c6de-204">Wybierz szablon hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-204">Select hello template.</span></span>
   
     ![edytowanie szablonu](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="9c6de-206">toobe toopass stanie hello wartości, które toospecify podczas wdrażania, Dodaj hello następujące dwa parametry toohello **parametry** części szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="9c6de-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="9c6de-207">nowe parametry hello toouse zastąpić definicji serwera SQL hello hello **zasobów** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="9c6de-208">Zwróć uwagę, że właściwości **administratorLogin** i **administratorLoginPassword** korzystają teraz z wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="9c6de-209">Wybierz **OK** po zakończeniu edycji szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="9c6de-210">Wybierz **zapisać** toosave hello zmiany toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![zapisywanie szablonu](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="9c6de-212">tooredeploy hello zaktualizowany szablon, wybierz opcję **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="9c6de-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![wdrażanie szablonu](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="9c6de-214">Podaj wartości parametrów, a następnie wybierz zasób grupy toodeploy hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="9c6de-215">Rozwiązywanie problemów z eksportowaniem</span><span class="sxs-lookup"><span data-stu-id="9c6de-215">Fix export issues</span></span>
<span data-ttu-id="9c6de-216">Nie wszystkie typy zasobów obsługują hello eksportowania szablonu funkcji.</span><span class="sxs-lookup"><span data-stu-id="9c6de-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="9c6de-217">Ten problem, ręcznie tooresolve hello Brak zasobów z powrotem dodać do szablonu.</span><span class="sxs-lookup"><span data-stu-id="9c6de-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="9c6de-218">komunikat o błędzie Hello obejmuje hello typów zasobów, które nie mogą być eksportowane.</span><span class="sxs-lookup"><span data-stu-id="9c6de-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="9c6de-219">Znajdź ten typ zasobów w [dokumentacji szablonu](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="9c6de-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="9c6de-220">Na przykład toomanually dodać bramę sieci wirtualnej, zobacz [odwołania do szablonu Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="9c6de-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="9c6de-221">Problemy związane z eksportowaniem występują tylko podczas eksportowania szablonu na podstawie grupy roboczej, a nie z historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9c6de-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="9c6de-222">Jeśli ostatniego wdrożenia dokładnie odzwierciedla bieżący stan hello hello grupy zasobów, możesz wyeksportować szablon hello z historii wdrożenia hello, a nie z hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="9c6de-223">Po dokonaniu zmiany toohello grup zasobów, nie są zdefiniowane w jednym szablonie tylko wyeksportować z grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c6de-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9c6de-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c6de-224">Next steps</span></span>
<span data-ttu-id="9c6de-225">Wiesz już, jak tooexport szablonu z zasobów, które zostały utworzone w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9c6de-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="9c6de-226">Szablon można wdrożyć przy użyciu [programu PowerShell](resource-group-template-deploy.md), [interfejsu wiersza polecenia platformy Azure](resource-group-template-deploy-cli.md) lub [interfejsu API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9c6de-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="9c6de-227">toosee tooexport szablonu za pomocą programu PowerShell, zobacz temat [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9c6de-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="9c6de-228">toosee tooexport szablonu za pomocą interfejsu wiersza polecenia Azure, zobacz temat [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9c6de-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

