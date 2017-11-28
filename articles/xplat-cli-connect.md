---
title: Logowanie do platformy Azure z poziomu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
description: "Połącz z subskrypcją platformy Azure z interfejsu wiersza polecenia platformy Azure (Azure CLI) dla komputerów Mac, Linux i Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="a908f-103">Logowanie do platformy Azure z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a908f-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="a908f-104">Interfejsu wiersza polecenia Azure to zestaw poleceń open source, obsługujący wiele platform do pracy z zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a908f-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="a908f-105">W tym artykule opisano różne sposoby poświadczenia konta Azure interfejsu wiersza polecenia Azure nawiązać połączenia z subskrypcją platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a908f-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="a908f-106">Uruchom `azure login` polecenia interfejsu wiersza polecenia do uwierzytelniania za pomocą usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a908f-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="a908f-107">Ta metoda umożliwia dostęp do poleceń interfejsu wiersza polecenia w obu [polecenia tryby](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="a908f-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="a908f-108">Po uruchomieniu polecenia bez dodatkowych opcji `azure login` wyświetli monit o kontynuowanie interakcyjnie zalogować się za pośrednictwem portalu sieci web.</span><span class="sxs-lookup"><span data-stu-id="a908f-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="a908f-109">Aby uzyskać dodatkowe `azure login` polecenia opcji, zobacz scenariusze w tym artykule, lub typ `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="a908f-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="a908f-110">Jeśli musisz używać polecenia interfejsu wiersza polecenia w trybie zarządzania usługami Azure (nie zalecane dla większości nowych wdrożeń), można pobrać i zainstalować plik ustawień publikowania na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a908f-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="a908f-111">Jeśli nie została jeszcze zainstalowana interfejsu wiersza polecenia, zobacz [instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a908f-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="a908f-112">Jeśli nie masz subskrypcji Azure, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a908f-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="a908f-113">Aby uzyskać ogólne informacje o tożsamości z innego konta i subskrypcji platformy Azure, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a908f-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="a908f-114">Scenariusz 1: azure logowania przy użyciu logowania interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="a908f-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="a908f-115">Z określonymi kontami interfejsu wiersza polecenia wymaga uruchomienia `azure login` , a następnie kontynuuj proces logowania przy użyciu przeglądarki sieci web za pośrednictwem portalu sieci web, w procesie nazywanym *logowania interakcyjnego*.</span><span class="sxs-lookup"><span data-stu-id="a908f-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="a908f-116">Typową przyczyną jest, jeśli masz konto służbowe (nazywane również *konta organizacyjnego*) skonfigurowane wymaganie uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a908f-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="a908f-117">Za pomocą logowania interaktywnego Twojego konta Microsoft, należy użyć polecenia w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a908f-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="a908f-118">Interakcyjne logowanie jest łatwe: typ `azure login` — bez żadnych opcji--jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a908f-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="a908f-119">Dane wyjściowe zostanie wyświetlony ekran podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="a908f-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="a908f-120">Skopiuj kod oferowanych w danych wyjściowych polecenia, a następnie otwórz przeglądarkę do http://aka.ms/devicelogin lub inne strony, jeśli określony.</span><span class="sxs-lookup"><span data-stu-id="a908f-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="a908f-121">(Aby otworzyć przeglądarkę na tym samym komputerze lub na innym komputerze lub urządzeniu). Wprowadź kod, a następnie zostanie wyświetlony monit o wprowadzenie nazwy użytkownika i hasła tożsamości, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="a908f-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="a908f-122">Po zakończeniu tego procesu powłoki poleceń kończy nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="a908f-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="a908f-123">Może wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="a908f-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="a908f-124">Z logowania interakcyjnego uwierzytelnianie i autoryzacja są wykonywane przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a908f-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="a908f-125">Jeśli używasz tożsamość konta Microsoft, proces logowania uzyskuje dostęp do domeny domyślnej usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a908f-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="a908f-126">(Jeśli zostało zarejestrowane w bezpłatne konto platformy Azure, Azure Active Directory tworzone domyślną domenę dla konta.)</span><span class="sxs-lookup"><span data-stu-id="a908f-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="a908f-127">Scenariusz 2: azure Zaloguj się za pomocą nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="a908f-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="a908f-128">Użyj `azure login` polecenia nazwy użytkownika (`-u`) parametru do uwierzytelniania, gdy chcesz użyć służbowego lub konto służbowe, które nie wymaga uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a908f-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="a908f-129">Zostanie wyświetlony monit o hasło w wierszu polecenia (lub hasło można przekazać opcjonalnie jako parametr dodatkowe `azure login` polecenia).</span><span class="sxs-lookup"><span data-stu-id="a908f-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="a908f-130">Poniższy przykład przekazuje nazwę użytkownika konta organizacyjnego:</span><span class="sxs-lookup"><span data-stu-id="a908f-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="a908f-131">Następnie zostanie wyświetlony monit o wprowadzenie hasła:</span><span class="sxs-lookup"><span data-stu-id="a908f-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="a908f-132">Następnie kończy proces logowania.</span><span class="sxs-lookup"><span data-stu-id="a908f-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="a908f-133">Jeśli jest to Twoje pierwsze rejestrowania w czasie przy użyciu tych poświadczeń, należy sprawdzić, które chcesz buforować tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a908f-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="a908f-134">Ten monit występuje także jeśli poprzednio korzystano `azure logout` polecenia (opisane w dalszej części tego artykułu).</span><span class="sxs-lookup"><span data-stu-id="a908f-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="a908f-135">Aby pominąć ten wiersz w scenariuszach automatyzacji, uruchom `azure login` z `-q` parametru.</span><span class="sxs-lookup"><span data-stu-id="a908f-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="a908f-136">Scenariusz 3: azure logowania przy użyciu nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="a908f-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="a908f-137">Jeśli tworzenie nazwy głównej usługi dla aplikacji usługi Active Directory, a nazwy głównej usługi ma uprawnienia do subskrypcji, możesz użyć `azure login` polecenie, aby uwierzytelnić nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a908f-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="a908f-138">W zależności od scenariusza, można podać poświadczenia nazwy głównej usługi jako jawne parametry `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a908f-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="a908f-139">Na przykład następujące polecenie przekazuje główną nazwę usługi i identyfikator dzierżawy usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a908f-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="a908f-140">Następnie monit o podanie hasła.</span><span class="sxs-lookup"><span data-stu-id="a908f-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="a908f-141">Można również podać poświadczenia, za pomocą interfejsu wiersza polecenia kodu skryptu lub aplikacji lub Użyj certyfikatu do uwierzytelnienia nazwy głównej usługi nieinteraktywnie w scenariuszach automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a908f-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="a908f-142">Aby uzyskać szczegółowe informacje i przykłady, zobacz [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a908f-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="a908f-143">Scenariusz 4: Korzystanie z pliku ustawień publikowania</span><span class="sxs-lookup"><span data-stu-id="a908f-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="a908f-144">Jeśli musisz używać poleceń usługi Azure Service Management tryb interfejsu wiersza polecenia (na przykład w celu wdrożenia maszyn wirtualnych platformy Azure w klasycznym modelu wdrażania), możesz połączyć za pomocą pliku ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="a908f-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="a908f-145">Ta metoda instaluje certyfikat na komputerze lokalnym, który umożliwia wykonywanie zadań zarządzania dla tak długo, jak subskrypcja i certyfikat są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="a908f-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="a908f-146">**Aby pobrać plik ustawień publikowania** dla Twojego konta, upewnij się, że interfejsu wiersza polecenia jest w trybie zarządzania usługami, wpisując `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="a908f-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="a908f-147">Następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a908f-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="a908f-148">To uruchomi domyślną przeglądarkę i wyświetli monit o Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a908f-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a908f-149">Po zalogowaniu, `.publishsettings` pliku pliki do pobrania.</span><span class="sxs-lookup"><span data-stu-id="a908f-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="a908f-150">Zanotuj miejsce, w którym plik został zapisany.</span><span class="sxs-lookup"><span data-stu-id="a908f-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="a908f-151">Jeśli Twoje konto jest skojarzone z wieloma dzierżawcami usługi Azure Active Directory, może być monit o wybranie które chcesz pobrać plik ustawień publikowania dla usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a908f-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="a908f-152">Po wybraniu za pomocą strony pobierania lub poprzez odwiedzenie klasycznego portalu Azure, wybrane usługi Active Directory staje się domyślne używane przez stronę klasycznego portalu i pobierania.</span><span class="sxs-lookup"><span data-stu-id="a908f-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="a908f-153">Po ustanowieniu domyślny, zostanie wyświetlony tekst "**kliknij tutaj, aby powrócić do strony wyboru**" w górnej części strony pobierania.</span><span class="sxs-lookup"><span data-stu-id="a908f-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="a908f-154">Użyj podane łącze, aby powrócić do strony wyboru.</span><span class="sxs-lookup"><span data-stu-id="a908f-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="a908f-155">**Aby zaimportować plik ustawień publikowania**, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a908f-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="a908f-156">Po zaimportowaniu Twoje ustawienia publikowania, należy usunąć `.publishsettings` pliku.</span><span class="sxs-lookup"><span data-stu-id="a908f-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="a908f-157">Nie jest już wymagana przez wiersza polecenia platformy Azure, a stanowi zagrożenie bezpieczeństwa, ponieważ może służyć do uzyskania dostępu do Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a908f-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="a908f-158">Tryby polecenia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a908f-158">CLI command modes</span></span>
<span data-ttu-id="a908f-159">Azure CLI dostępne są dwa tryby polecenia do pracy z zasobami Azure z zestawami inne polecenie:</span><span class="sxs-lookup"><span data-stu-id="a908f-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="a908f-160">**Tryb usługi Resource Manager** — w przypadku pracy z zasobami platformy Azure w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a908f-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="a908f-161">Aby ustawić ten tryb, uruchom `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="a908f-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="a908f-162">**Tryb zarządzania usługami** — w przypadku pracy z zasobami platformy Azure w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a908f-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="a908f-163">Aby ustawić ten tryb, uruchom `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="a908f-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="a908f-164">Podczas pierwszej instalacji bieżącej wersji interfejsu wiersza polecenia jest w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a908f-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="a908f-165">Tryb usługi Resource Manager i tryb usługi zarządzania wzajemnie się wykluczają.</span><span class="sxs-lookup"><span data-stu-id="a908f-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="a908f-166">Oznacza to, że zasoby utworzone w trybie jednego nie można zarządzać z innych trybu.</span><span class="sxs-lookup"><span data-stu-id="a908f-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="a908f-167">Wiele subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a908f-167">Multiple subscriptions</span></span>
<span data-ttu-id="a908f-168">Jeśli masz wiele subskrypcji Azure, łączenie Azure udziela dostępu do wszystkich subskrypcji skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a908f-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="a908f-169">Jedna subskrypcja jest wybrana jako domyślna i używane przez interfejs wiersza polecenia Azure podczas wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="a908f-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="a908f-170">Można wyświetlić subskrypcje, łącznie z bieżącej subskrypcji domyślną, używając `azure account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a908f-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="a908f-171">To polecenie zwraca informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a908f-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="a908f-172">Na powyższej liście **bieżącego** bieżącej subskrypcji domyślne jako Azure-sub-1 wskazuje kolumny.</span><span class="sxs-lookup"><span data-stu-id="a908f-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="a908f-173">Aby zmienić domyślne subskrypcji, użyj `azure account set` polecenia, a następnie określ subskrypcję, która ma być domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a908f-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="a908f-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a908f-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="a908f-175">Spowoduje to zmianę domyślnego subskrypcji na Azure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="a908f-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="a908f-176">Zmiana domyślnego subskrypcji aktywne natychmiast i zmiana globalnych; nowe polecenia interfejsu wiersza polecenia Azure, czy uruchamiać z tego samego wystąpienia wiersza polecenia lub inne wystąpienie, użyj nowej subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="a908f-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="a908f-177">Jeśli chcesz użyć innych niż domyślne subskrypcji z wiersza polecenia platformy Azure, ale nie chcesz zmienić bieżące ustawienie domyślne, możesz użyć `--subscription` opcji dla polecenia i podać nazwę subskrypcji chcesz użyć dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="a908f-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="a908f-178">Po nawiązaniu połączenia z subskrypcją platformy Azure, możesz rozpocząć używać polecenia interfejsu wiersza polecenia Azure do pracy z zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a908f-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="a908f-179">Magazyn ustawień interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a908f-179">Storage of CLI settings</span></span>
<span data-ttu-id="a908f-180">Czy możesz zalogować się przy użyciu `azure login` polecenia lub importowania ustawień publikowania, profilu interfejsu wiersza polecenia i dzienniki są przechowywane w `.azure` katalog znajduje się w sieci `user` katalogu.</span><span class="sxs-lookup"><span data-stu-id="a908f-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="a908f-181">Twoje `user` katalogu jest chroniony przez system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="a908f-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="a908f-182">Jednak zaleca się wykonanie dodatkowych czynności w celu zaszyfrowania Twojej `user` katalogu.</span><span class="sxs-lookup"><span data-stu-id="a908f-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="a908f-183">Można to zrobić na następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="a908f-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="a908f-184">W systemie Windows należy zmodyfikować właściwości katalogu lub używać funkcji BitLocker.</span><span class="sxs-lookup"><span data-stu-id="a908f-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="a908f-185">Dla komputerów Mac należy włączyć funkcję FileVault dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="a908f-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="a908f-186">W systemie Ubuntu skorzystaj z funkcji zaszyfrowanego katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="a908f-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="a908f-187">Inne dystrybucje systemu Linux oferuje podobne funkcje.</span><span class="sxs-lookup"><span data-stu-id="a908f-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="a908f-188">Wylogowywanie</span><span class="sxs-lookup"><span data-stu-id="a908f-188">Logging out</span></span>
<span data-ttu-id="a908f-189">Się wylogować, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a908f-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="a908f-190">Jeśli subskrypcji skojarzone z kontem, są uwierzytelniani tylko z usługą Active Directory, wylogowaniu usunięcia informacji o subskrypcji z profilu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a908f-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="a908f-191">Jednak także zaimportowano plik ustawień publikowania dla subskrypcji, rejestrowanie tylko do usunięcia usługi Active Directory powiązane informacje z profilu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a908f-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a908f-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a908f-192">Next steps</span></span>
* <span data-ttu-id="a908f-193">Użycie poleceń interfejsu wiersza polecenia Azure, zobacz [polecenia wiersza polecenia platformy Azure w trybie Menedżera zasobów](virtual-machines/azure-cli-arm-commands.md) i [polecenia wiersza polecenia platformy Azure w trybie zarządzania usługami](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a908f-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="a908f-194">Aby dowiedzieć się więcej o Azure CLI, pobierania kodu źródłowego, zgłaszanie problemów lub przyczyniają się do projektu, odwiedź stronę [repozytorium GitHub dla interfejsu wiersza polecenia Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="a908f-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="a908f-195">Jeśli wystąpią problemy przy użyciu wiersza polecenia platformy Azure lub usługi Azure, odwiedź stronę [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="a908f-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
