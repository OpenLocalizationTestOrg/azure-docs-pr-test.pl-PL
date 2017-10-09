---
title: "aaaConfigure usługi Zarządzanie interfejsami API przy użyciu narzędzia Git - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosave i skonfigurować konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git."
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
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="ce1f1-103">Jak toosave i skonfigurować konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="ce1f1-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="ce1f1-104">Każde wystąpienie usługi Zarządzanie interfejsami API utrzymuje bazę danych konfiguracji, który zawiera informacje o konfiguracji hello i metadanych dla wystąpienia usługi hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="ce1f1-105">Można wprowadzać zmiany wystąpienie usługi toohello przez zmianę ustawień w portalu wydawcy hello, za pomocą polecenia cmdlet programu PowerShell lub wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="ce1f1-106">Ponadto toothese metod, można również zarządzać konfiguracji wystąpienia usługi przy użyciu narzędzia Git, takie jak włączanie scenariusze zarządzania usługi:</span><span class="sxs-lookup"><span data-stu-id="ce1f1-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="ce1f1-107">Przechowywanie wersji konfiguracji — Pobierz i przechowywać różne wersje konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="ce1f1-108">Zbiorcze zmiany konfiguracji — zmiany toomultiple części konfiguracji usługi w lokalnym repozytorium i integracji serwera zapasowego toohello zmiany hello z jednej operacji</span><span class="sxs-lookup"><span data-stu-id="ce1f1-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="ce1f1-109">Znanego łańcuch narzędzi Git i przepływ pracy - Użyj narzędzia Git hello i przepływów pracy, które znasz już</span><span class="sxs-lookup"><span data-stu-id="ce1f1-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="ce1f1-110">powitania po diagram zawiera omówienie tooconfigure różne sposoby hello wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Skonfiguruj Git][api-management-git-configure]

<span data-ttu-id="ce1f1-112">Podczas wprowadzania zmian usługi tooyour przy użyciu portalu wydawcy hello, poleceń cmdlet programu PowerShell lub interfejsu API REST hello zarządza bazą danych konfiguracji usługi za pomocą hello `https://{name}.management.azure-api.net` punktu końcowego, jak pokazano na powitania po prawej stronie powitania diagramu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="ce1f1-113">Hello lewej hello diagram ilustruje sposób zarządzania konfiguracji usługi przy użyciu narzędzia Git i repozytorium Git dla usługi znajduje się w `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="ce1f1-114">Witaj, wykonaj czynności udostępnia przegląd zarządzania wystąpienia usługi Zarządzanie interfejsami API przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="ce1f1-115">Konfiguracja Git dostępu w usłudze</span><span class="sxs-lookup"><span data-stu-id="ce1f1-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="ce1f1-116">Zapisz repozytorium Git tooyour bazy danych konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="ce1f1-117">Klonowanie maszyny lokalnej tooyour repozytorium Git hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="ce1f1-118">Pobierać najnowsze repozytorium hello dół tooyour komputera lokalnego i zatwierdzania i wypychania repozytorium wstecz tooyour zmiany</span><span class="sxs-lookup"><span data-stu-id="ce1f1-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="ce1f1-119">Wdrażanie hello zmiany z Twojego repozytorium do bazy danych konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="ce1f1-120">W tym artykule opisano sposób tooenable znajdują się informacje na powitania pliki i foldery w repozytorium Git hello i użyj Git toomanage konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="ce1f1-121">Konfiguracja Git dostępu w usłudze</span><span class="sxs-lookup"><span data-stu-id="ce1f1-121">Access Git configuration in your service</span></span>
<span data-ttu-id="ce1f1-122">Wyświetlając ikonę Git hello w hello prawym górnym rogu portalu wydawcy hello można szybko wyświetlić stan hello konfiguracji Git.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="ce1f1-123">W tym przykładzie hello komunikatu o stanie wskazuje, że istnieją niezapisane zmiany toohello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="ce1f1-124">Jest to spowodowane hello bazy danych konfiguracji usługi API Management nie został jeszcze zapisany toohello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Stan Git][api-management-git-icon-enable]

<span data-ttu-id="ce1f1-126">tooview i skonfigurować ustawienia konfiguracji Git, możesz kliknąć ikonę Git hello, lub kliknij hello **zabezpieczeń** menu i przejdź toohello **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Włącz GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="ce1f1-128">Wszystkie klucze tajne, które nie są zdefiniowane jako właściwości będą przechowywane w repozytorium hello i pozostanie w jego historii dopóki Wyłącz i ponownie włączyć dostęp Git.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="ce1f1-129">Właściwości zapewniają toomanage bezpiecznym miejscu stałych wartości ciągów, tym klucze tajne, we wszystkich Konfiguracja interfejsu API i zasady, dzięki czemu nie trzeba toostore bezpośrednio w deklaracji z zasad.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="ce1f1-130">Aby uzyskać więcej informacji, zobacz [jak właściwości toouse w ramach zasad usługi Azure API Management](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="ce1f1-131">Aby uzyskać informacji na temat włączania lub wyłączania dostępu Git przy użyciu hello interfejsu API REST, zobacz [Włączanie lub wyłączanie dostępu Git przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="ce1f1-132">repozytorium Git toohello toosave hello usługi konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ce1f1-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="ce1f1-133">pierwszym krokiem Hello przed klonowanie repozytorium hello jest toosave hello bieżący stan hello usługi konfiguracji toohello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="ce1f1-134">Kliknij przycisk **Zapisz konfigurację toorepository**.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-134">Click **Save configuration toorepository**.</span></span>

![Zapisywanie konfiguracji][api-management-save-configuration]

<span data-ttu-id="ce1f1-136">Żądane zmiany na ekranie potwierdzenia hello, a następnie kliknij przycisk **Ok** toosave.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Zapisywanie konfiguracji][api-management-save-configuration-confirm]

<span data-ttu-id="ce1f1-138">Po kilku chwilach konfiguracji hello jest zapisywana i wyświetlany jest stan konfiguracji hello hello repozytorium, w tym hello Data i godzina ostatniej zmiany konfiguracji hello i hello ostatniej synchronizacji konfiguracji usługi hello hello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Stan konfiguracji][api-management-configuration-status]

<span data-ttu-id="ce1f1-140">Po zapisaniu repozytorium toohello hello konfiguracji mogą być klonowane.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="ce1f1-141">Informacje na wykonanie tej operacji przy użyciu hello interfejsu API REST, zobacz [konfiguracji zatwierdzania migawki za pomocą interfejsu API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="ce1f1-142">komputer lokalny tooyour tooclone hello repozytorium</span><span class="sxs-lookup"><span data-stu-id="ce1f1-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="ce1f1-143">tooclone repozytorium należy hello adresu URL tooyour repozytorium, nazwę użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="ce1f1-144">Witaj nazwę użytkownika i adres URL są wyświetlane u góry hello hello **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Klonowania Git][api-management-configuration-git-clone]

<span data-ttu-id="ce1f1-146">Witaj hasło jest generowane u dołu hello hello **repozytorium konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Generowanie hasła][api-management-generate-password]

<span data-ttu-id="ce1f1-148">toogenerate hasła, najpierw upewnij się, że hello **wygaśnięcia** ustawić toohello potrzeby datę i godzinę wygaśnięcia, a następnie kliknij przycisk **Generuj Token**.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Hasło][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="ce1f1-150">Zanotuj to hasło.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-150">Make a note of this password.</span></span> <span data-ttu-id="ce1f1-151">Po wyjściu to hasło hello strona nie zostanie ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="ce1f1-152">Następujące przykłady użycia hello Git Bash Hello narzędzia z [Git dla systemu Windows](http://www.git-scm.com/downloads) , ale można użyć dowolnego narzędzia Git, które znasz.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="ce1f1-153">Otwórz narzędzie Git w folderze żądaną hello i uruchom hello następujące polecenia tooclone hello git repozytorium tooyour komputera lokalnego, za pomocą polecenia hello udostępnionych przez portal wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ce1f1-154">Podaj hello nazwę użytkownika i hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="ce1f1-155">Jeśli wystąpią błędy, spróbuj zmodyfikować Twoje `git clone` polecenia tooinclude hello użytkownika nazwę i hasło, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ce1f1-156">Jeśli to zawiera błąd, spróbuj kodowania hello hasła część polecenia hello URL.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="ce1f1-157">Jeden toodo szybko to tooopen programu Visual Studio, a problem hello następujące polecenie w hello **oknie bezpośrednim**.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="ce1f1-158">tooopen hello **oknie bezpośrednim**, otwórz dowolnego rozwiązania lub projektu w programie Visual Studio (lub Utwórz nową aplikację konsoli puste) i wybierz polecenie **Windows**, **Immediate** z Witaj **debugowania** menu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="ce1f1-159">Użyj hasła hello zakodowany oraz użytkownika nazwę i repozytorium lokalizacji tooconstruct hello git polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ce1f1-160">Gdy jest sklonować repozytorium hello można przeglądać i pracę z nią w lokalnym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="ce1f1-161">Aby uzyskać więcej informacji, zobacz [plików i folderów odniesienia lokalnego repozytorium Git struktury](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="ce1f1-162">tooupdate repozytorium lokalne powitania najbardziej bieżącej konfiguracji wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="ce1f1-163">Jeśli wystąpienie usługi Zarządzanie interfejsami API tooyour zmian w portalu wydawcy hello lub przy użyciu interfejsu API REST hello, musisz zapisać te zmiany toohello repozytorium przed zaktualizowaniem lokalnym repozytorium z hello najnowsze zmiany.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="ce1f1-164">toodo tego, kliknij **Zapisz konfigurację toorepository** na powitania **repozytorium konfiguracji** karcie w portalu wydawcy hello, a następnie wystawiania hello następujące polecenie w lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="ce1f1-165">Przed uruchomieniem `git pull` upewnij się, że są w folderze hello dla lokalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="ce1f1-166">Jeśli został ukończony hello `git clone` polecenia, a następnie należy zmienić hello katalogu tooyour repozytorium, uruchamiając polecenie, takie jak następujące hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="ce1f1-167">zmiany toopush Twojego repozytorium lokalnego repozytorium toohello serwera</span><span class="sxs-lookup"><span data-stu-id="ce1f1-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="ce1f1-168">toopush zmiany z repozytorium lokalnego repozytorium toohello serwera, należy zatwierdzić zmiany, a następnie Wypchnij je toohello serwera repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="ce1f1-169">toocommit zmiany, otwórz Git narzędzia polecenia przełącznika toohello katalogu lokalnego repozytorium, a problem hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="ce1f1-170">zatwierdza wszystkie hello toohello serwera Uruchom toopush hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="ce1f1-171">toodeploy wszystkie wystąpienia usługi konfiguracji zmiany toohello zarządzanie interfejsami API usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="ce1f1-172">Po zatwierdzeniu zmiany lokalne repozytorium serwera toohello zatwierdzonej i wypychanie, można je wdrożyć wystąpienie usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Wdrażanie][api-management-configuration-deploy]

<span data-ttu-id="ce1f1-174">Informacje na wykonanie tej operacji przy użyciu hello interfejsu API REST, zobacz [wdrażanie Git zmienia tooconfiguration bazy danych przy użyciu interfejsu API REST hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="ce1f1-175">Odwołanie struktury plików i folderów z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="ce1f1-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="ce1f1-176">Hello pliki i foldery w repozytorium git lokalne powitania zawierają hello informacji konfiguracyjnych dotyczących hello wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="ce1f1-177">Element</span><span class="sxs-lookup"><span data-stu-id="ce1f1-177">Item</span></span> | <span data-ttu-id="ce1f1-178">Opis</span><span class="sxs-lookup"><span data-stu-id="ce1f1-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce1f1-179">Folder główny zarządzanie interfejsami api</span><span class="sxs-lookup"><span data-stu-id="ce1f1-179">root api-management folder</span></span> |<span data-ttu-id="ce1f1-180">Zawiera konfigurację najwyższego poziomu hello wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="ce1f1-181">interfejsy API folderu</span><span class="sxs-lookup"><span data-stu-id="ce1f1-181">apis folder</span></span> |<span data-ttu-id="ce1f1-182">Zawiera konfigurację hello hello interfejsów API w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="ce1f1-183">folder grupy</span><span class="sxs-lookup"><span data-stu-id="ce1f1-183">groups folder</span></span> |<span data-ttu-id="ce1f1-184">Zawiera konfigurację hello hello grup w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="ce1f1-185">folder zasady</span><span class="sxs-lookup"><span data-stu-id="ce1f1-185">policies folder</span></span> |<span data-ttu-id="ce1f1-186">Zawiera zasady hello w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="ce1f1-187">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="ce1f1-187">portalStyles folder</span></span> |<span data-ttu-id="ce1f1-188">Zawiera konfigurację hello Dostosowywanie portalu deweloperów hello w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="ce1f1-189">folder produktów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-189">products folder</span></span> |<span data-ttu-id="ce1f1-190">Zawiera konfigurację hello hello produktów w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="ce1f1-191">folder szablonów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-191">templates folder</span></span> |<span data-ttu-id="ce1f1-192">Zawiera konfigurację hello hello szablonów wiadomości e-mail w wystąpieniu usługi hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="ce1f1-193">Każdego folderu może zawierać jeden lub więcej plików, a w niektórych przypadkach jeden lub więcej folderów, na przykład folderu dla każdego interfejsu API, produktu lub grupy.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="ce1f1-194">Hello pliki w tych folderach są specyficzne dla typu jednostki hello opisanego przez hello nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="ce1f1-195">Typ pliku</span><span class="sxs-lookup"><span data-stu-id="ce1f1-195">File type</span></span> | <span data-ttu-id="ce1f1-196">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="ce1f1-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="ce1f1-197">JSON</span><span class="sxs-lookup"><span data-stu-id="ce1f1-197">json</span></span> |<span data-ttu-id="ce1f1-198">Informacje o konfiguracji dotyczące hello odpowiednich jednostek</span><span class="sxs-lookup"><span data-stu-id="ce1f1-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="ce1f1-199">HTML</span><span class="sxs-lookup"><span data-stu-id="ce1f1-199">html</span></span> |<span data-ttu-id="ce1f1-200">Opisy jednostek hello, często są wyświetlane w portalu dla deweloperów hello</span><span class="sxs-lookup"><span data-stu-id="ce1f1-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="ce1f1-201">xml</span><span class="sxs-lookup"><span data-stu-id="ce1f1-201">xml</span></span> |<span data-ttu-id="ce1f1-202">Instrukcje zasad</span><span class="sxs-lookup"><span data-stu-id="ce1f1-202">Policy statements</span></span> |
| <span data-ttu-id="ce1f1-203">CSS</span><span class="sxs-lookup"><span data-stu-id="ce1f1-203">css</span></span> |<span data-ttu-id="ce1f1-204">Arkusze stylów do dostosowania portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="ce1f1-205">Tych plików można można utworzyć, usunąć edytować i zarządzane w lokalnym systemie plików, a zmiany hello wdrożone wstecz toohello wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="ce1f1-206">Witaj następujące jednostek nie są zawarte w repozytorium Git hello i nie można skonfigurować przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="ce1f1-207">Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="ce1f1-207">Users</span></span>
> * <span data-ttu-id="ce1f1-208">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="ce1f1-208">Subscriptions</span></span>
> * <span data-ttu-id="ce1f1-209">Właściwości</span><span class="sxs-lookup"><span data-stu-id="ce1f1-209">Properties</span></span>
> * <span data-ttu-id="ce1f1-210">Jednostek portalu deweloperów innych niż style</span><span class="sxs-lookup"><span data-stu-id="ce1f1-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="ce1f1-211">Folder główny zarządzanie interfejsami api</span><span class="sxs-lookup"><span data-stu-id="ce1f1-211">Root api-management folder</span></span>
<span data-ttu-id="ce1f1-212">główny Hello `api-management` folder zawiera `configuration.json` plik zawierający informacje najwyższego poziomu o wystąpienie usługi hello w hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

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

<span data-ttu-id="ce1f1-213">Witaj pierwsze cztery ustawienia (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, i `UserRegistrationTermsConsentRequired`) mapy toohello następujące ustawienia na powitania **tożsamości** kartę w hello **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="ce1f1-214">Ustawienia tożsamości</span><span class="sxs-lookup"><span data-stu-id="ce1f1-214">Identity setting</span></span> | <span data-ttu-id="ce1f1-215">Mapuje zbyt</span><span class="sxs-lookup"><span data-stu-id="ce1f1-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="ce1f1-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="ce1f1-216">RegistrationEnabled</span></span> |<span data-ttu-id="ce1f1-217">**Przekierować użytkowników anonimowych toosign w stronę** wyboru</span><span class="sxs-lookup"><span data-stu-id="ce1f1-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="ce1f1-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="ce1f1-218">UserRegistrationTerms</span></span> |<span data-ttu-id="ce1f1-219">**Warunki użytkowania w rejestracji użytkownika** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="ce1f1-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="ce1f1-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="ce1f1-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="ce1f1-221">**Pokaż warunki użytkowania na stronie rejestracja** wyboru</span><span class="sxs-lookup"><span data-stu-id="ce1f1-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="ce1f1-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="ce1f1-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="ce1f1-223">**Wymagaj zgody** wyboru</span><span class="sxs-lookup"><span data-stu-id="ce1f1-223">**Require consent** checkbox</span></span> |

![Ustawienia tożsamości][api-management-identity-settings]

<span data-ttu-id="ce1f1-225">Witaj obok czterech ustawień (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, i `DelegationValidationKey`) mapy toohello następujące ustawienia na powitania **delegowania** kartę w hello **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="ce1f1-226">Ustawienie delegowania</span><span class="sxs-lookup"><span data-stu-id="ce1f1-226">Delegation setting</span></span> | <span data-ttu-id="ce1f1-227">Mapuje zbyt</span><span class="sxs-lookup"><span data-stu-id="ce1f1-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="ce1f1-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="ce1f1-228">DelegationEnabled</span></span> |<span data-ttu-id="ce1f1-229">**Delegat logowania & zapisywania** wyboru</span><span class="sxs-lookup"><span data-stu-id="ce1f1-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="ce1f1-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="ce1f1-230">DelegationUrl</span></span> |<span data-ttu-id="ce1f1-231">**Adres URL punktu końcowego delegowania** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="ce1f1-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="ce1f1-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="ce1f1-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="ce1f1-233">**Delegowanie subskrypcji produktu** wyboru</span><span class="sxs-lookup"><span data-stu-id="ce1f1-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="ce1f1-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="ce1f1-234">DelegationValidationKey</span></span> |<span data-ttu-id="ce1f1-235">**Delegowanie klucz sprawdzania poprawności** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="ce1f1-235">**Delegate Validation Key** textbox</span></span> |

![Ustawienia delegowania][api-management-delegation-settings]

<span data-ttu-id="ce1f1-237">Witaj końcowego ustawienie `$ref-policy`, mapy pliku instrukcje globalne zasady toohello hello wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="ce1f1-238">interfejsy API folderu</span><span class="sxs-lookup"><span data-stu-id="ce1f1-238">apis folder</span></span>
<span data-ttu-id="ce1f1-239">Witaj `apis` folder zawiera folder dla każdego interfejsu API w wystąpieniu usługi hello zawierającą hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="ce1f1-240">`apis\<api name>\configuration.json`-to jest Konfiguracja hello hello interfejsu API i zawiera informacje o operacji hello i adres URL usługi zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="ce1f1-241">Jest to hello informacje, które będzie zwracany, jeśli zostały toocall [pobrania określonego interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) z `export=true` w `application/json` format.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="ce1f1-242">`apis\<api name>\api.description.html`-to jest opis hello hello interfejsu API i odpowiada toohello `description` właściwości hello [jednostki interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="ce1f1-243">`apis\<api name>\operations\`— Ten folder zawiera `<operation name>.description.html` plików, które mapują toohello operacje w hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="ce1f1-244">Każdy plik zawiera opis hello jednej operacji w hello interfejsu API, który mapuje toohello `description` właściwości hello [operacji jednostki](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) w hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="ce1f1-245">folder grupy</span><span class="sxs-lookup"><span data-stu-id="ce1f1-245">groups folder</span></span>
<span data-ttu-id="ce1f1-246">Witaj `groups` folder zawiera folder dla każdej grupy zdefiniowanej w hello wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="ce1f1-247">`groups\<group name>\configuration.json`-to jest Konfiguracja hello hello grupy.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="ce1f1-248">Jest to hello informacje, które będzie zwracany, jeśli zostały toocall hello [pobrać określonej grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operacji.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="ce1f1-249">`groups\<group name>\description.html`-to jest hello opis grupy hello i odpowiada toohello `description` właściwości hello [grupy jednostki](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="ce1f1-250">folder zasady</span><span class="sxs-lookup"><span data-stu-id="ce1f1-250">policies folder</span></span>
<span data-ttu-id="ce1f1-251">Witaj `policies` folder zawiera hello zasad instrukcje dla swojego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="ce1f1-252">`policies\global.xml`-zawiera zasady zdefiniowane w zakresie globalnym wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="ce1f1-253">`policies\apis\<api name>\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie interfejsu API są zawarte w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="ce1f1-254">`policies\apis\<api name>\<operation name>\`folder — Jeśli masz wszystkie zasady zdefiniowane w zakresie operacji są zawarte w tym folderze `<operation name>.xml` plików, które mapują toohello deklaracji zasad dla każdej operacji.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="ce1f1-255">`policies\products\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie produktu są zawarte w tym folderze, który zawiera `<product name>.xml` plików, które mapują toohello deklaracji zasad dla każdego produktu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="ce1f1-256">portalStyles folder</span><span class="sxs-lookup"><span data-stu-id="ce1f1-256">portalStyles folder</span></span>
<span data-ttu-id="ce1f1-257">Witaj `portalStyles` folder zawiera konfigurację i styl arkusze Dostosowywanie portalu deweloperów hello wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="ce1f1-258">`portalStyles\configuration.json`-zawiera nazwy hello arkuszy stylów hello używane przez hello portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="ce1f1-259">`portalStyles\<style name>.css`-każdego `<style name>.css` plik zawiera style portalu dla deweloperów hello (`Preview.css` i `Production.css` domyślnie).</span><span class="sxs-lookup"><span data-stu-id="ce1f1-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="ce1f1-260">folder produktów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-260">products folder</span></span>
<span data-ttu-id="ce1f1-261">Witaj `products` folder zawiera folder dla każdego produktu zdefiniowane w hello wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="ce1f1-262">`products\<product name>\configuration.json`-to jest Konfiguracja hello hello produktu.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="ce1f1-263">Jest to hello informacje, które będzie zwracany, jeśli zostały toocall hello [pobrania określonego produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operacji.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="ce1f1-264">`products\<product name>\product.description.html`-to jest opis hello hello produktu i odpowiada toohello `description` właściwości hello [jednostki produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) w hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="ce1f1-265">szablonów</span><span class="sxs-lookup"><span data-stu-id="ce1f1-265">templates</span></span>
<span data-ttu-id="ce1f1-266">Witaj `templates` folder zawiera konfigurację hello [szablonów wiadomości e-mail](api-management-howto-configure-notifications.md) hello wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="ce1f1-267">`<template name>\configuration.json`-to jest Konfiguracja hello hello szablonu wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="ce1f1-268">`<template name>\body.html`-to jest treść hello hello szablon wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="ce1f1-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce1f1-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce1f1-269">Next steps</span></span>
<span data-ttu-id="ce1f1-270">Aby uzyskać informacje o innych sposobów toomanage wystąpienia usługi, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ce1f1-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="ce1f1-271">Zarządzanie za pomocą następującego polecenia cmdlet programu PowerShell hello wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="ce1f1-272">Wdrożenie usługi dokumentacji poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce1f1-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="ce1f1-273">Zarządzanie usługami dokumentacji poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce1f1-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="ce1f1-274">Zarządzaj w portalu wydawcy hello wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="ce1f1-275">Zarządzanie pierwszym interfejsem API</span><span class="sxs-lookup"><span data-stu-id="ce1f1-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="ce1f1-276">Zarządzanie za pomocą interfejsu API REST hello wystąpienia usługi</span><span class="sxs-lookup"><span data-stu-id="ce1f1-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="ce1f1-277">Dokumentacja interfejsu API REST zarządzania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ce1f1-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="ce1f1-278">Obejrzyj film wideo</span><span class="sxs-lookup"><span data-stu-id="ce1f1-278">Watch a video overview</span></span>
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




