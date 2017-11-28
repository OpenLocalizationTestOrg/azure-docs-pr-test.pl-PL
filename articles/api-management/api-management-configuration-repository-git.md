---
title: "Konfigurowanie usługi Zarządzanie interfejsami API przy użyciu narzędzia Git - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zapisać i skonfigurować konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="8ab3b-103">Zapisz i konfigurowaniu konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="8ab3b-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="8ab3b-104">Każde wystąpienie usługi Zarządzanie interfejsami API utrzymuje bazę danych konfiguracji, który zawiera informacje o konfiguracji i metadanych dla wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="8ab3b-105">Można zmodyfikować wystąpienie usługi przez zmianę ustawień w portalu wydawcy, za pomocą polecenia cmdlet programu PowerShell lub wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="8ab3b-106">Oprócz tych metod można również zarządzać konfiguracji wystąpienia usługi przy użyciu narzędzia Git, takie jak włączanie scenariusze zarządzania usługi:</span><span class="sxs-lookup"><span data-stu-id="8ab3b-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="8ab3b-107">Przechowywanie wersji konfiguracji — Pobierz i przechowywać różne wersje konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="8ab3b-108">Zbiorcze zmiany konfiguracji — wprowadzić zmiany w wielu części konfiguracji usługi w lokalnym repozytorium i integracji zmian z powrotem na serwer z jednej operacji</span><span class="sxs-lookup"><span data-stu-id="8ab3b-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="8ab3b-109">Znane Git łańcuch narzędzi i przepływ pracy - Użyj narzędzia Git i przepływy pracy, które znasz już</span><span class="sxs-lookup"><span data-stu-id="8ab3b-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="8ab3b-110">Na poniższym diagramie przedstawiono przegląd różnych sposobów, aby skonfigurować wystąpienie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Skonfiguruj Git][api-management-git-configure]

<span data-ttu-id="8ab3b-112">Po wprowadzeniu zmian w usłudze przy użyciu portalu wydawcy, poleceń cmdlet programu PowerShell lub interfejsu API REST zarządzania z usługi konfiguracji bazy danych przy użyciu `https://{name}.management.azure-api.net` punktu końcowego, jak pokazano po prawej stronie diagramu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="8ab3b-113">W lewej części diagram ilustruje, jak można zarządzać przy użyciu narzędzia Git konfiguracji usługi i repozytorium Git dla usługi znajduje się w `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="8ab3b-114">Poniższe kroki zawierają omówienie zarządzania wystąpienia usługi Zarządzanie interfejsami API przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="8ab3b-115">Konfiguracja Git dostępu w usłudze</span><span class="sxs-lookup"><span data-stu-id="8ab3b-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="8ab3b-116">Zapisz bazę danych konfiguracji usługi do repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="8ab3b-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="8ab3b-117">Klonowanie repozytorium Git na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="8ab3b-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="8ab3b-118">Pobierać najnowsze repozytorium do komputera lokalnego i zatwierdzania i wypychania zmian z powrotem do Twojego repozytorium</span><span class="sxs-lookup"><span data-stu-id="8ab3b-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="8ab3b-119">Wdrażanie zmiany z Twojego repozytorium do bazy danych konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="8ab3b-120">W tym artykule opisano, jak włączyć i umożliwia zarządzanie konfiguracji usługi Git i zawiera odwołanie do plików i folderów w repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="8ab3b-121">Konfiguracja Git dostępu w usłudze</span><span class="sxs-lookup"><span data-stu-id="8ab3b-121">Access Git configuration in your service</span></span>
<span data-ttu-id="8ab3b-122">Można szybko wyświetlić stan konfiguracji Git, wyświetlając Git ikonę w prawym górnym rogu portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="8ab3b-123">W tym przykładzie komunikatu o stanie wskazuje, że że istnieją niezapisane zmiany do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="8ab3b-124">Jest to spowodowane bazy danych konfiguracji usługi API Management nie został jeszcze zapisany do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Stan Git][api-management-git-icon-enable]

<span data-ttu-id="8ab3b-126">Aby wyświetlić i skonfigurować ustawienia konfiguracji Git, możesz kliknąć ikonę Git, lub kliknij przycisk **zabezpieczeń** menu i przejdź do **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Włącz GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="8ab3b-128">Wszystkie klucze tajne, które nie są zdefiniowane jako właściwości będą przechowywane w repozytorium i pozostanie w jego historii dopóki Wyłącz i ponownie włączyć dostęp Git.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="8ab3b-129">Właściwości zapewniają bezpiecznym miejscu, aby zarządzać stałych wartości ciągów, tym klucze tajne, we wszystkich Konfiguracja interfejsu API i zasad, więc nie trzeba przechowywać je bezpośrednio w instrukcjach użytkownika zasady.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="8ab3b-130">Aby uzyskać więcej informacji, zobacz [sposób użycia właściwości w ramach zasad usługi Azure API Management](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="8ab3b-131">Aby uzyskać informacje na włączanie lub wyłączanie dostępu Git przy użyciu interfejsu API REST, zobacz [Włączanie lub wyłączanie dostępu Git przy użyciu interfejsu API REST](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="8ab3b-132">Aby zapisać konfigurację usługi do repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="8ab3b-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="8ab3b-133">Pierwszym krokiem przed klonowanie repozytorium jest zapisanie bieżącego stanu konfiguracji usługi do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="8ab3b-134">Kliknij przycisk **Zapisz konfigurację do repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-134">Click **Save configuration to repository**.</span></span>

![Zapisywanie konfiguracji][api-management-save-configuration]

<span data-ttu-id="8ab3b-136">Wprowadź żądane zmiany na ekranie potwierdzenia i kliknij przycisk **Ok** do zapisania.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Zapisywanie konfiguracji][api-management-save-configuration-confirm]

<span data-ttu-id="8ab3b-138">Po kilku chwilach konfiguracji jest zapisywana i wyświetlany jest stan konfiguracji repozytorium, w tym datę i godzinę ostatniej zmiany konfiguracji i ostatniej synchronizacji konfiguracji usługi i repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Stan konfiguracji][api-management-configuration-status]

<span data-ttu-id="8ab3b-140">Po zapisaniu konfiguracji do repozytorium można sklonować.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="8ab3b-141">Aby uzyskać informacje na wykonanie tej operacji przy użyciu interfejsu API REST, zobacz [migawki za pomocą interfejsu API REST konfiguracji zatwierdzania](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="8ab3b-142">Klonowanie repozytorium na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="8ab3b-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="8ab3b-143">Klonowanie repozytorium, musisz adres URL repozytorium, nazwę użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="8ab3b-144">Nazwa użytkownika i adres URL są wyświetlane w górnej części **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Klonowania Git][api-management-configuration-git-clone]

<span data-ttu-id="8ab3b-146">Hasło jest generowane w dolnej części **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Generowanie hasła][api-management-generate-password]

<span data-ttu-id="8ab3b-148">Aby wygenerować hasła, najpierw upewnij się, że **wygaśnięcia** jest ustawiona na odpowiednią datę i godzinę wygaśnięcia, a następnie kliknij przycisk **Generuj Token**.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Hasło][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="8ab3b-150">Zanotuj to hasło.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-150">Make a note of this password.</span></span> <span data-ttu-id="8ab3b-151">Gdy opuścisz tę stronę hasło nie zostanie ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="8ab3b-152">W poniższych przykładach użyto narzędzia Git Bash z [Git dla systemu Windows](http://www.git-scm.com/downloads) , ale można użyć dowolnego narzędzia Git, które znasz.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="8ab3b-153">Otwórz narzędzie Git w odpowiedni folder i uruchom następujące polecenie, aby Klonuj repozytorium git na komputerze lokalnym za pomocą polecenia udostępnionych przez portal wydawcy.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="8ab3b-154">Podaj nazwę użytkownika i hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="8ab3b-155">Jeśli wystąpią błędy, spróbuj zmodyfikować Twoje `git clone` polecenie, aby uwzględnić nazwę użytkownika i hasło, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="8ab3b-156">Jeśli to zawiera błąd, spróbuj kodowania hasła część polecenia URL.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="8ab3b-157">To jeden szybko, w tym celu otwórz program Visual Studio i wydać następujące polecenie w **oknie bezpośrednim**.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="8ab3b-158">Aby otworzyć **oknie bezpośrednim**, otwórz dowolnego rozwiązania lub projektu w programie Visual Studio (lub Utwórz nową aplikację konsoli puste) i wybierz polecenie **Windows**, **Immediate** z **Debugowania** menu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="8ab3b-159">Użyj zaszyfrowanych haseł wraz z lokalizacji nazwy i repozytorium użytkownika do skonstruowania polecenia git.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="8ab3b-160">Gdy jest sklonować repozytorium można przeglądać i pracę z nią w lokalnym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="8ab3b-161">Aby uzyskać więcej informacji, zobacz [plików i folderów odniesienia lokalnego repozytorium Git struktury](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="8ab3b-162">Aby zaktualizować lokalnym repozytorium z najnowszą konfiguracją wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="8ab3b-163">Jeśli wprowadzasz zmiany do Twojego wystąpienia usługi Zarządzanie interfejsami API w portalu wydawcy lub przy użyciu interfejsu API REST, należy zapisać te zmiany do repozytorium przed zaktualizowaniem lokalnym repozytorium o najnowsze zmiany.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="8ab3b-164">Aby to zrobić, kliknij przycisk **Zapisz konfigurację do repozytorium** na **repozytorium konfiguracji** karcie w portalu wydawcy, a następnie należy wydać następujące polecenie w lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="8ab3b-165">Przed uruchomieniem `git pull` upewnij się, że znajdujesz się w folderze lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="8ab3b-166">Jeśli właśnie został ukończony `git clone` polecenia, a następnie należy zmienić katalogu do Twojego repozytorium, uruchamiając polecenie podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="8ab3b-167">Aby wypchnąć zmiany z z lokalnego repozytorium do repozytorium serwera</span><span class="sxs-lookup"><span data-stu-id="8ab3b-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="8ab3b-168">Aby wypchnąć zmiany z lokalnym repozytorium do repozytorium serwera, należy zatwierdzić zmiany i wypychanie ich do repozytorium serwera.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="8ab3b-169">Aby zatwierdzić zmiany, Otwórz narzędzie polecenia Git, przełącz się do katalogu lokalnego repozytorium i wydawać następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="8ab3b-170">Aby wypchnąć wszystkie zatwierdzenia na serwerze, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="8ab3b-171">Aby wdrożyć zmian konfiguracji usługi do wystąpienia usługi Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="8ab3b-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="8ab3b-172">Po lokalne zmiany są zatwierdzone i do repozytorium serwera, można je wdrożyć do Twojego wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Wdrażanie][api-management-configuration-deploy]

<span data-ttu-id="8ab3b-174">Aby uzyskać informacje na wykonanie tej operacji przy użyciu interfejsu API REST, zobacz [wdrażanie Git zmiany w konfiguracji bazy danych przy użyciu interfejsu API REST](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="8ab3b-175">Odwołanie struktury plików i folderów z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="8ab3b-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="8ab3b-176">Pliki i foldery w repozytorium git lokalne zawierają informacje o konfiguracji dotyczące wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="8ab3b-177">Element</span><span class="sxs-lookup"><span data-stu-id="8ab3b-177">Item</span></span> | <span data-ttu-id="8ab3b-178">Opis</span><span class="sxs-lookup"><span data-stu-id="8ab3b-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ab3b-179">Folder główny zarządzanie interfejsami api</span><span class="sxs-lookup"><span data-stu-id="8ab3b-179">root api-management folder</span></span> |<span data-ttu-id="8ab3b-180">Zawiera konfigurację najwyższego poziomu dla wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="8ab3b-181">interfejsy API folderu</span><span class="sxs-lookup"><span data-stu-id="8ab3b-181">apis folder</span></span> |<span data-ttu-id="8ab3b-182">Zawiera konfigurację interfejsów API w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="8ab3b-183">folder grupy</span><span class="sxs-lookup"><span data-stu-id="8ab3b-183">groups folder</span></span> |<span data-ttu-id="8ab3b-184">Zawiera konfigurację grup w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="8ab3b-185">folder zasady</span><span class="sxs-lookup"><span data-stu-id="8ab3b-185">policies folder</span></span> |<span data-ttu-id="8ab3b-186">Zawiera zasady w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="8ab3b-187">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="8ab3b-187">portalStyles folder</span></span> |<span data-ttu-id="8ab3b-188">Zawiera konfigurację Dostosowywanie portalu deweloperów w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="8ab3b-189">folder produktów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-189">products folder</span></span> |<span data-ttu-id="8ab3b-190">Zawiera konfigurację produktów w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="8ab3b-191">folder szablonów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-191">templates folder</span></span> |<span data-ttu-id="8ab3b-192">Zawiera konfigurację szablony wiadomości e-mail w wystąpieniu usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="8ab3b-193">Każdego folderu może zawierać jeden lub więcej plików, a w niektórych przypadkach jeden lub więcej folderów, na przykład folderu dla każdego interfejsu API, produktu lub grupy.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="8ab3b-194">Pliki w tych folderach są specyficzne dla typu jednostki opisanego przez nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="8ab3b-195">Typ pliku</span><span class="sxs-lookup"><span data-stu-id="8ab3b-195">File type</span></span> | <span data-ttu-id="8ab3b-196">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="8ab3b-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="8ab3b-197">JSON</span><span class="sxs-lookup"><span data-stu-id="8ab3b-197">json</span></span> |<span data-ttu-id="8ab3b-198">Informacje o konfiguracji dotyczące odpowiednich jednostek</span><span class="sxs-lookup"><span data-stu-id="8ab3b-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="8ab3b-199">HTML</span><span class="sxs-lookup"><span data-stu-id="8ab3b-199">html</span></span> |<span data-ttu-id="8ab3b-200">Opisy jednostek, często są wyświetlane w portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="8ab3b-201">xml</span><span class="sxs-lookup"><span data-stu-id="8ab3b-201">xml</span></span> |<span data-ttu-id="8ab3b-202">Instrukcje zasad</span><span class="sxs-lookup"><span data-stu-id="8ab3b-202">Policy statements</span></span> |
| <span data-ttu-id="8ab3b-203">CSS</span><span class="sxs-lookup"><span data-stu-id="8ab3b-203">css</span></span> |<span data-ttu-id="8ab3b-204">Arkusze stylów do dostosowania portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="8ab3b-205">Te pliki można tworzyć, usunąć, edytować i zarządzane w lokalnym systemie plików i wdrożeniu zmian z powrotem do wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab3b-206">Następujące jednostek nie są zawarte w repozytorium Git i nie można skonfigurować przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="8ab3b-207">Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="8ab3b-207">Users</span></span>
> * <span data-ttu-id="8ab3b-208">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="8ab3b-208">Subscriptions</span></span>
> * <span data-ttu-id="8ab3b-209">Właściwości</span><span class="sxs-lookup"><span data-stu-id="8ab3b-209">Properties</span></span>
> * <span data-ttu-id="8ab3b-210">Jednostek portalu deweloperów innych niż style</span><span class="sxs-lookup"><span data-stu-id="8ab3b-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="8ab3b-211">Folder główny zarządzanie interfejsami api</span><span class="sxs-lookup"><span data-stu-id="8ab3b-211">Root api-management folder</span></span>
<span data-ttu-id="8ab3b-212">Katalog główny `api-management` folder zawiera `configuration.json` plik zawierający informacje najwyższego poziomu o wystąpienie usługi o następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="8ab3b-213">Pierwsze cztery ustawienia (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, i `UserRegistrationTermsConsentRequired`) mapowania na następujące ustawienia na **tożsamości** karcie **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="8ab3b-214">Ustawienia tożsamości</span><span class="sxs-lookup"><span data-stu-id="8ab3b-214">Identity setting</span></span> | <span data-ttu-id="8ab3b-215">Mapuje</span><span class="sxs-lookup"><span data-stu-id="8ab3b-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="8ab3b-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="8ab3b-216">RegistrationEnabled</span></span> |<span data-ttu-id="8ab3b-217">**Przekieruj do strony logowania użytkowników anonimowych** wyboru</span><span class="sxs-lookup"><span data-stu-id="8ab3b-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="8ab3b-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="8ab3b-218">UserRegistrationTerms</span></span> |<span data-ttu-id="8ab3b-219">**Warunki użytkowania w rejestracji użytkownika** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8ab3b-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="8ab3b-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="8ab3b-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="8ab3b-221">**Pokaż warunki użytkowania na stronie rejestracja** wyboru</span><span class="sxs-lookup"><span data-stu-id="8ab3b-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="8ab3b-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="8ab3b-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="8ab3b-223">**Wymagaj zgody** wyboru</span><span class="sxs-lookup"><span data-stu-id="8ab3b-223">**Require consent** checkbox</span></span> |

![Ustawienia tożsamości][api-management-identity-settings]

<span data-ttu-id="8ab3b-225">Następnie czterech ustawień (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, i `DelegationValidationKey`) mapowania na następujące ustawienia na **delegowania** karcie **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="8ab3b-226">Ustawienie delegowania</span><span class="sxs-lookup"><span data-stu-id="8ab3b-226">Delegation setting</span></span> | <span data-ttu-id="8ab3b-227">Mapuje</span><span class="sxs-lookup"><span data-stu-id="8ab3b-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="8ab3b-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="8ab3b-228">DelegationEnabled</span></span> |<span data-ttu-id="8ab3b-229">**Delegat logowania & zapisywania** wyboru</span><span class="sxs-lookup"><span data-stu-id="8ab3b-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="8ab3b-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="8ab3b-230">DelegationUrl</span></span> |<span data-ttu-id="8ab3b-231">**Adres URL punktu końcowego delegowania** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8ab3b-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="8ab3b-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="8ab3b-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="8ab3b-233">**Delegowanie subskrypcji produktu** wyboru</span><span class="sxs-lookup"><span data-stu-id="8ab3b-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="8ab3b-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="8ab3b-234">DelegationValidationKey</span></span> |<span data-ttu-id="8ab3b-235">**Delegowanie klucz sprawdzania poprawności** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8ab3b-235">**Delegate Validation Key** textbox</span></span> |

![Ustawienia delegowania][api-management-delegation-settings]

<span data-ttu-id="8ab3b-237">Ustawienie ostatecznego `$ref-policy`, mapy do pliku instrukcje globalne zasady dla wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="8ab3b-238">interfejsy API folderu</span><span class="sxs-lookup"><span data-stu-id="8ab3b-238">apis folder</span></span>
<span data-ttu-id="8ab3b-239">`apis` Folder zawiera folder dla każdego interfejsu API w wystąpieniu usługi, który zawiera następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="8ab3b-240">`apis\<api name>\configuration.json`-to jest Konfiguracja interfejsu API i zawiera informacje dotyczące operacji i adres URL usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="8ab3b-241">Jest to te same informacje, który będzie zwracany w przypadku wywołania [pobrania określonego interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) z `export=true` w `application/json` format.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="8ab3b-242">`apis\<api name>\api.description.html`-to jest opis interfejsu API i odpowiada `description` właściwość [jednostki interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="8ab3b-243">`apis\<api name>\operations\`— Ten folder zawiera `<operation name>.description.html` pliki, które są mapowane na operacje w interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="8ab3b-244">Każdy plik zawiera opis jednej operacji w interfejsie API, który mapuje na `description` właściwość [operacji jednostki](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) w interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="8ab3b-245">folder grupy</span><span class="sxs-lookup"><span data-stu-id="8ab3b-245">groups folder</span></span>
<span data-ttu-id="8ab3b-246">`groups` Folder zawiera folder dla każdej grupy zdefiniowane w wystąpieniu usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="8ab3b-247">`groups\<group name>\configuration.json`— jest to konfiguracja dla grupy.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="8ab3b-248">Jest to te same informacje, który będzie zwracany w przypadku wywołania [Pobierz określoną grupę](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operacji.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="8ab3b-249">`groups\<group name>\description.html`-to jest opis grupy i odpowiada `description` właściwość [grupy jednostki](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="8ab3b-250">folder zasady</span><span class="sxs-lookup"><span data-stu-id="8ab3b-250">policies folder</span></span>
<span data-ttu-id="8ab3b-251">`policies` Folder zawiera deklaracji zasad dla swojego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="8ab3b-252">`policies\global.xml`-zawiera zasady zdefiniowane w zakresie globalnym wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="8ab3b-253">`policies\apis\<api name>\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie interfejsu API są zawarte w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="8ab3b-254">`policies\apis\<api name>\<operation name>\`folder — Jeśli masz wszystkie zasady zdefiniowane w zakresie operacji są zawarte w tym folderze `<operation name>.xml` plików, które mapują do deklaracji zasad dla każdej operacji.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="8ab3b-255">`policies\products\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie produktu są zawarte w tym folderze, który zawiera `<product name>.xml` plików, które mapują do deklaracji zasad dla każdego produktu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="8ab3b-256">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="8ab3b-256">portalStyles folder</span></span>
<span data-ttu-id="8ab3b-257">`portalStyles` Folder zawiera konfigurację i styl arkusze Dostosowywanie portalu deweloperów dla wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="8ab3b-258">`portalStyles\configuration.json`-zawiera nazwy arkuszy stylów używany przez portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="8ab3b-259">`portalStyles\<style name>.css`-każdego `<style name>.css` plik zawiera style portalu dla deweloperów (`Preview.css` i `Production.css` domyślnie).</span><span class="sxs-lookup"><span data-stu-id="8ab3b-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="8ab3b-260">folder produktów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-260">products folder</span></span>
<span data-ttu-id="8ab3b-261">`products` Folder zawiera folder dla każdego produktu z definicją w wystąpieniu usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="8ab3b-262">`products\<product name>\configuration.json`— jest to konfiguracja produktu.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="8ab3b-263">Jest to te same informacje, który będzie zwracany w przypadku wywołania [pobrania określonego produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operacji.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="8ab3b-264">`products\<product name>\product.description.html`-to jest opis produktu i odpowiada `description` właściwość [jednostki produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) w interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="8ab3b-265">szablonów</span><span class="sxs-lookup"><span data-stu-id="8ab3b-265">templates</span></span>
<span data-ttu-id="8ab3b-266">`templates` Folder zawiera konfigurację [szablonów wiadomości e-mail](api-management-howto-configure-notifications.md) wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="8ab3b-267">`<template name>\configuration.json`-to jest konfiguracja dla szablonu wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="8ab3b-268">`<template name>\body.html`-to jest treść szablon wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="8ab3b-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ab3b-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ab3b-269">Next steps</span></span>
<span data-ttu-id="8ab3b-270">Aby uzyskać informacje na inne sposoby zarządzania wystąpienia usługi zobacz:</span><span class="sxs-lookup"><span data-stu-id="8ab3b-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="8ab3b-271">Zarządzanie wystąpienia usługi za pomocą następujących poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab3b-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="8ab3b-272">Wdrożenie usługi dokumentacji poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab3b-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="8ab3b-273">Zarządzanie usługami dokumentacji poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab3b-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="8ab3b-274">Zarządzaj w portalu wydawcy wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="8ab3b-275">Zarządzanie pierwszym interfejsem API</span><span class="sxs-lookup"><span data-stu-id="8ab3b-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="8ab3b-276">Zarządzanie za pomocą interfejsu API REST wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="8ab3b-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="8ab3b-277">Dokumentacja interfejsu API REST zarządzania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8ab3b-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="8ab3b-278">Obejrzyj film wideo</span><span class="sxs-lookup"><span data-stu-id="8ab3b-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




