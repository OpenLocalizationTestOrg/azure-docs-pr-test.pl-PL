---
title: aaaGet pracy z szablonami prywatnymi | Dokumentacja firmy Microsoft
description: "Dodawanie, zarządzanie i udostępnianie szablonów prywatnych przy użyciu hello portalu Azure, hello wiersza polecenia platformy Azure lub programu PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="224c7-103">Rozpoczynanie pracy z szablonami prywatnymi w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="224c7-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="224c7-104">[Usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) szablon to deklaracyjny szablon używany toodefine wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="224c7-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="224c7-105">Można zdefiniować hello toodeploy zasobów dla rozwiązania i określić parametry i zmienne, które pozwalają tooinput wartości dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="224c7-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="224c7-106">Witaj szablon składa się z kodu JSON i wyrażeń, których można użyć wartości tooconstruct na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="224c7-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="224c7-107">Można użyć nowego hello **szablony** możliwości w hello [Azure Portal](https://portal.azure.com) wraz z hello **Microsoft.Gallery** dostawcy zasobów jako rozszerzenie hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate użytkowników, zarządzanie i wdrażanie szablonów prywatnych z poziomu biblioteki osobistej.</span><span class="sxs-lookup"><span data-stu-id="224c7-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="224c7-108">Ten dokument przeprowadzi Cię przez dodawanie, zarządzanie i udostępnianie prywatnej **szablonu** przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="224c7-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="224c7-109">Wskazówki</span><span class="sxs-lookup"><span data-stu-id="224c7-109">Guidance</span></span>
<span data-ttu-id="224c7-110">Witaj poniższe sugestie pomogą Ci w pełni korzystać z **szablony** podczas pracy z rozwiązaniami:</span><span class="sxs-lookup"><span data-stu-id="224c7-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="224c7-111">**Szablon** to hermetyzowany zasób, który zawiera szablon usługi Resource Manager i dodatkowe metadane.</span><span class="sxs-lookup"><span data-stu-id="224c7-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="224c7-112">Zachowuje się bardzo podobnie tooan elementu hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="224c7-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="224c7-113">Hello klucza różnica polega na tym, że jest to element prywatny jako min. toohello publicznych elementów Marketplace.</span><span class="sxs-lookup"><span data-stu-id="224c7-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="224c7-114">Witaj **szablony** biblioteki działa dobrze w przypadku użytkowników, którzy potrzebują toocustomize ich wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="224c7-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="224c7-115">**Szablony** są dobrym rozwiązaniem dla użytkowników, którzy potrzebują prostego repozytorium na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="224c7-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="224c7-116">Rozpocznij pracę z istniejącym szablonem usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="224c7-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="224c7-117">Wyszukaj szablony w witrynie [github](https://github.com/Azure/azure-quickstart-templates) lub [wyeksportuj szablon](../azure-resource-manager/resource-manager-export-template.md) z istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="224c7-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="224c7-118">**Szablony** wiązanej toohello użytkowników, którzy je opublikował.</span><span class="sxs-lookup"><span data-stu-id="224c7-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="224c7-119">Nazwa wydawcy Hello jest widoczne tooeveryone, kto ma dostęp do odczytu tooit.</span><span class="sxs-lookup"><span data-stu-id="224c7-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="224c7-120">**Szablony** to zasoby usługi Resource Manager. Po opublikowaniu nie można zmienić ich nazwy.</span><span class="sxs-lookup"><span data-stu-id="224c7-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="224c7-121">Dodawanie zasobu Szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-121">Add a Template resource</span></span>
<span data-ttu-id="224c7-122">Istnieją dwa sposoby toocreate **szablonu** zasobu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="224c7-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="224c7-123">Metoda 1. Tworzenie nowego zasobu Szablon z poziomu uruchomionej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="224c7-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="224c7-124">Przejdź tooan istniejącej grupy zasobów na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="224c7-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="224c7-125">Wybierz pozycję **Eksportuj szablon** w obszarze **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="224c7-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="224c7-126">Po wyeksportowaniu szablonu usługi Resource Manager hello, użyj hello **Zapisz szablon** toosave przycisk go toohello **szablony** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="224c7-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="224c7-127">Wszystkie szczegóły eksportowania szablonu możesz znaleźć [tutaj](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="224c7-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="224c7-128">
   ![Eksportowanie grupy zasobów](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="224c7-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="224c7-129">Wybierz hello **zapisać tooTemplate** przycisku polecenia.</span><span class="sxs-lookup"><span data-stu-id="224c7-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="224c7-130">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="224c7-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="224c7-131">Nazwa — Nazwa obiektu szablonu hello (Uwaga: to jest nazwa usługi Azure Resource Manager, na podstawie.</span><span class="sxs-lookup"><span data-stu-id="224c7-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="224c7-132">Obowiązują wszystkie ograniczenia związane z nazewnictwem, a utworzonej nazwy nie można zmienić).</span><span class="sxs-lookup"><span data-stu-id="224c7-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="224c7-133">Opis — krótkie podsumowanie dotyczące szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="224c7-133">Description – Quick summary about hello template.</span></span>
     
     ![Zapisywanie szablonu](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="224c7-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="224c7-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="224c7-136">Hello bloku eksportowania szablonu zostaną wyświetlone powiadomienia podczas hello wyeksportowanego szablonu usługi Resource Manager zawiera błędy, ale nadal będzie można toosave tego toohello szablonu usługi Resource Manager szablonów.</span><span class="sxs-lookup"><span data-stu-id="224c7-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="224c7-137">Upewnij się, sprawdź, a następnie napraw wszystkie problemy dotyczące szablonu przed ponownego wdrażania hello wyeksportowanego szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="224c7-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="224c7-138">Metoda 2. Dodawanie nowego szablonu przy użyciu funkcji przeglądania</span><span class="sxs-lookup"><span data-stu-id="224c7-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="224c7-139">Można również dodać nowy **szablonu** od początku, używając Witaj + przycisk polecenia Dodaj w **Przeglądaj > Szablony**.</span><span class="sxs-lookup"><span data-stu-id="224c7-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="224c7-140">Konieczne będzie tooprovide nazwę, opis i hello JSON szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="224c7-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Dodawanie szablonu](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="224c7-142">Microsoft.Gallery to oparty na dzierżawie dostawca zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="224c7-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="224c7-143">Witaj zasobu szablon jest wiązana toohello użytkownika, który go utworzył.</span><span class="sxs-lookup"><span data-stu-id="224c7-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="224c7-144">Nie jest związany tooany określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="224c7-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="224c7-145">Subskrypcję należy wybrać tylko w przypadku wdrażania szablonu toobe.</span><span class="sxs-lookup"><span data-stu-id="224c7-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="224c7-146">Wyświetlanie zasobów Szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-146">View Template resources</span></span>
<span data-ttu-id="224c7-147">Wszystkie **szablony** tooyou dostępne są widoczne w **Przeglądaj > Szablony**.</span><span class="sxs-lookup"><span data-stu-id="224c7-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="224c7-148">Będą to **szablony** utworzone przez Ciebie, a także te, które zostały Ci udostępnione z różnymi poziomami uprawnień.</span><span class="sxs-lookup"><span data-stu-id="224c7-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="224c7-149">Więcej szczegółów w hello [kontrola dostępu](#access-control-for-a-tenant-resource-provider) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="224c7-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Wyświetlanie szablonu](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="224c7-151">Można wyświetlić szczegóły hello **szablonu** , kliknij element na liście hello.</span><span class="sxs-lookup"><span data-stu-id="224c7-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Wyświetlanie szablonu](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="224c7-153">Edytowanie zasobu Szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-153">Edit a Template resource</span></span>
<span data-ttu-id="224c7-154">Możesz zainicjować przepływ edycji hello **szablonu** przez kliknięcie prawym przyciskiem myszy element hello na powitania listy przeglądania lub wybierając przycisk polecenia edycji hello.</span><span class="sxs-lookup"><span data-stu-id="224c7-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Edytowanie szablonu](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="224c7-156">Można edytować hello opis lub tekst szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="224c7-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="224c7-157">Nie można edytować nazwy hello, ponieważ jest to nazwa zasobu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="224c7-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="224c7-158">Podczas edytowania szablonu usługi Resource Manager hello JSON sprawdzamy, czy tooensure jest poprawne dane JSON.</span><span class="sxs-lookup"><span data-stu-id="224c7-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="224c7-159">Wybierz **OK** , a następnie **zapisać** toosave zaktualizowany szablon.</span><span class="sxs-lookup"><span data-stu-id="224c7-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Edytowanie szablonu](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="224c7-161">Raz hello **szablonu** zapisaniu zostanie wyświetlone powiadomienie o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="224c7-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Edytowanie szablonu](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="224c7-163">Wdrażanie zasobu Szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-163">Deploy a Template resource</span></span>
<span data-ttu-id="224c7-164">Możesz wdrożyć dowolny **szablon**, do którego masz uprawnienia do **odczytu**.</span><span class="sxs-lookup"><span data-stu-id="224c7-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="224c7-165">Witaj przepływ wdrożenia powoduje uruchomienie standardowego bloku wdrożenia szablonu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="224c7-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="224c7-166">Należy wprowadzić wartości hello hello Menedżera zasobów szablonu parametrów tooproceed hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="224c7-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Wdrażanie szablonu](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="224c7-168">Udostępnianie zasobu Szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-168">Share a Template resource</span></span>
<span data-ttu-id="224c7-169">Zasób **Szablon** można udostępniać innym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="224c7-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="224c7-170">Udostępnianie działa podobnie zbyt[przypisania roli dla dowolnego zasobu na platformie Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="224c7-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="224c7-171">Witaj **szablonu** właściciela zapewnia uprawnienia tooother użytkowników, którzy mogą współdziałać z zasobem szablon.</span><span class="sxs-lookup"><span data-stu-id="224c7-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="224c7-172">Witaj osoba lub grupa osób udostępnianie hello **szablonu** z będą szablonu usługi Resource Manager hello stanie toosee i galerię jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="224c7-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="224c7-173">Kontrola dostępu do zasobów Microsoft.Gallery hello</span><span class="sxs-lookup"><span data-stu-id="224c7-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="224c7-174">Rola</span><span class="sxs-lookup"><span data-stu-id="224c7-174">Role</span></span> | <span data-ttu-id="224c7-175">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="224c7-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="224c7-176">Właściciel</span><span class="sxs-lookup"><span data-stu-id="224c7-176">Owner</span></span> |<span data-ttu-id="224c7-177">Umożliwia pełną kontrolę zasobu szablon hello tym udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="224c7-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="224c7-178">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="224c7-178">Reader</span></span> |<span data-ttu-id="224c7-179">Umożliwia odczyt i wykonywanie (wdrażanie) na powitania zasobu szablon</span><span class="sxs-lookup"><span data-stu-id="224c7-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="224c7-180">Współautor</span><span class="sxs-lookup"><span data-stu-id="224c7-180">Contributor</span></span> |<span data-ttu-id="224c7-181">Umożliwia edytowanie i usuwanie hello zasobu szablon.</span><span class="sxs-lookup"><span data-stu-id="224c7-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="224c7-182">Użytkownik nie może udostępnić hello szablonu</span><span class="sxs-lookup"><span data-stu-id="224c7-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="224c7-183">Wybierz **udziału** hello przeglądania elementu przez kliknięcie prawym przyciskiem myszy lub na powitania bloku przeglądania określonego elementu.</span><span class="sxs-lookup"><span data-stu-id="224c7-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="224c7-184">Spowoduje to uruchomienie środowiska udostępniania.</span><span class="sxs-lookup"><span data-stu-id="224c7-184">This launches a Share experience.</span></span>

![Udostępnianie szablonu](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="224c7-186">Teraz możesz wybrać rolę i użytkownika lub grupę tooprovide dostępu tooa określonego **szablonu**.</span><span class="sxs-lookup"><span data-stu-id="224c7-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="224c7-187">Witaj dostępne role to właściciel, Czytelnik i współautor.</span><span class="sxs-lookup"><span data-stu-id="224c7-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="224c7-188">Więcej szczegółów w hello [kontrola dostępu](#access-control-for-a-tenant-resource-provider) powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="224c7-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Udostępnianie szablonu](media/share-template-portal2b.png)  <br />

![Udostępnianie szablonu](media/share-template-portal3b.png)  <br />

<span data-ttu-id="224c7-191">Kliknij pozycję **Wybierz**, a następnie przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="224c7-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="224c7-192">Możesz teraz przeglądać hello użytkowników lub grupy dodane toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="224c7-192">You can now see hello users or groups you added toohello resource.</span></span>

![Udostępnianie szablonu](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="224c7-194">Szablon tylko może być udostępniane innym użytkownikom i grupom w hello tej samej dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="224c7-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="224c7-195">Jeśli szablon jest udostępniany adres e-mail, który nie jest w dzierżawie, zostaną wysłane zaproszenie pytaniem hello użytkownika toojoin hello dzierżawy jako Gość.</span><span class="sxs-lookup"><span data-stu-id="224c7-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="224c7-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="224c7-196">Next steps</span></span>
* <span data-ttu-id="224c7-197">toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [tworzenia szablonów](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="224c7-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="224c7-198">Funkcje hello toounderstand można użyć w szablonie usługi Resource Manager, zobacz [funkcje szablonów](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="224c7-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="224c7-199">Aby uzyskać wskazówki dotyczące projektowania szablonów, zobacz artykuł [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md) (Najlepsze rozwiązania dotyczące projektowania szablonów usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="224c7-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

