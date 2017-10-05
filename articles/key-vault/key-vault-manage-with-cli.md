---
title: "Zarządzanie usługą Azure Key Vault przy użyciu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka w celu automatyzacji typowych zadań w Key Vault za pomocą interfejsu wiersza polecenia"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="e40fc-103">Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e40fc-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="e40fc-104">Usługa Azure Key Vault jest dostępna w większości regionów.</span><span class="sxs-lookup"><span data-stu-id="e40fc-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="e40fc-105">Aby uzyskać więcej informacji, zobacz stronę [Cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e40fc-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="e40fc-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e40fc-106">Introduction</span></span>

<span data-ttu-id="e40fc-107">Ten samouczek ułatwi Ci rozpoczęcie pracy z usługą Azure Key Vault w celu utworzenia wzmocnionego kontenera (magazynu) na platformie Azure do przechowywania kluczy kryptograficznych i kluczy tajnych na platformie Azure oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="e40fc-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="e40fc-108">Przeprowadza użytkownika przez proces tworzenia magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure przy użyciu interfejsu wiersza polecenia platformy Azure i Platform.</span><span class="sxs-lookup"><span data-stu-id="e40fc-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="e40fc-109">Następnie pokaże Ci, jak aplikacja może następnie użyć tego klucza lub hasła.</span><span class="sxs-lookup"><span data-stu-id="e40fc-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="e40fc-110">**Szacowany czas trwania:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="e40fc-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="e40fc-111">Ten samouczek nie zawiera instrukcji dotyczących sposobu pisania aplikacji Azure, że jeden z kroków zawiera, który pokazuje, jak zezwolić aplikacji na używanie klucza lub klucza tajnego w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e40fc-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="e40fc-112">Obecnie nie można skonfigurować usługi Azure Key Vault w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e40fc-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="e40fc-113">Użyj tych instrukcji Międzyplatformowego interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e40fc-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="e40fc-114">Lub, aby uzyskać instrukcje programu Azure PowerShell, zobacz [tym równoważnym samouczku](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="e40fc-115">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e40fc-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e40fc-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e40fc-116">Prerequisites</span></span>

<span data-ttu-id="e40fc-117">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e40fc-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="e40fc-118">Subskrypcja platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e40fc-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="e40fc-119">Jeśli nie masz, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e40fc-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="e40fc-120">Interfejs wiersza polecenia w wersji od 0.9.1 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="e40fc-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="e40fc-121">Aby zainstalować najnowszą wersję i nawiązać połączenia z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia platformy Azure i Platform](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="e40fc-122">Aplikacja, która zostanie skonfigurowana w celu używania klucza lub hasła utworzonego w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="e40fc-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="e40fc-123">Przykładowa aplikacja jest dostępna w [Centrum pobierania Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="e40fc-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="e40fc-124">Aby uzyskać instrukcje, zobacz załączony plik Readme.</span><span class="sxs-lookup"><span data-stu-id="e40fc-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="e40fc-125">Uzyskiwanie pomocy z interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="e40fc-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="e40fc-126">Ten samouczek zakłada, że znasz interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="e40fc-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="e40fc-127">Parametru pomocy lub -h można wyświetlić Pomoc dla określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e40fc-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="e40fc-128">Alternatywnie azure help [polecenie] [opcje] format również może zostać użyty do zwrócenia tych samych informacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="e40fc-129">Na przykład poniższe polecenia wszystkie zwracają te same informacje:</span><span class="sxs-lookup"><span data-stu-id="e40fc-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="e40fc-130">W razie wątpliwości o parametry wymagane przez polecenie, zajrzyj do pomocy, przy użyciu — pomoc, -h lub azure help [polecenie].</span><span class="sxs-lookup"><span data-stu-id="e40fc-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="e40fc-131">Możesz przeczytać następujące samouczki, aby zapoznać się z usługą Azure Resource Manager w interfejsu wiersza polecenia platformy Azure i Platform:</span><span class="sxs-lookup"><span data-stu-id="e40fc-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="e40fc-132">Jak zainstalować i skonfigurować interfejs wiersza polecenia i Platform Azure</span><span class="sxs-lookup"><span data-stu-id="e40fc-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="e40fc-133">Przy użyciu interfejsu wiersza polecenia platformy Azure i Platform z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e40fc-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="e40fc-134">Nawiązywanie połączenia z subskrypcjami</span><span class="sxs-lookup"><span data-stu-id="e40fc-134">Connect to your subscriptions</span></span>

<span data-ttu-id="e40fc-135">Aby zalogować się przy użyciu konta organizacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e40fc-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="e40fc-136">lub jeśli chcesz się zalogować, wpisując interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="e40fc-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="e40fc-137">Metoda logowania działa tylko za pomocą konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e40fc-137">The login method only works with organizational account.</span></span> <span data-ttu-id="e40fc-138">Konta organizacyjnego jest użytkownik, który jest zarządzanych przez swoją organizację, a zdefiniowane w dzierżawie usługi Azure Active Directory w organizacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="e40fc-139">Jeśli aktualnie nie masz konta organizacyjnego i za pomocą konta Microsoft do logowania się do subskrypcji platformy Azure, możesz łatwo utworzyć jedną wykonując poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="e40fc-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="e40fc-140">Zaloguj się do logowania się do [portalu zarządzania Azure](https://manage.windowsazure.com/)i kliknij na usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e40fc-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="e40fc-141">Jeśli katalog nie istnieje, wybierz opcję Utwórz katalog i podaj żądane informacje.</span><span class="sxs-lookup"><span data-stu-id="e40fc-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="e40fc-142">Wybierz katalog, a następnie dodaj nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e40fc-142">Select your directory and add a new user.</span></span> <span data-ttu-id="e40fc-143">Ten nowy użytkownik jest kontem organizacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e40fc-143">This new user is an organizational account.</span></span> <span data-ttu-id="e40fc-144">Podczas tworzenia użytkownika należy podać zarówno adresów e-mail dla użytkownika oraz hasło tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="e40fc-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="e40fc-145">Zapisz te informacje, które jest używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="e40fc-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="e40fc-146">Z portalu wybierz pozycję Ustawienia, a następnie wybierz administratorów.</span><span class="sxs-lookup"><span data-stu-id="e40fc-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="e40fc-147">Wybierz opcję Dodaj i dodania nowego użytkownika jako administratora współpracującego.</span><span class="sxs-lookup"><span data-stu-id="e40fc-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="e40fc-148">Dzięki temu konta organizacyjnego do zarządzania subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e40fc-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="e40fc-149">Ponadto Wyloguj się z portalu Azure i następnie ponowne zalogowanie przy użyciu nowego konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e40fc-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="e40fc-150">Jeśli jest to pierwszy rejestrowania w czasie za pomocą tego konta, pojawi się monit o zmianę hasła.</span><span class="sxs-lookup"><span data-stu-id="e40fc-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="e40fc-151">Aby uzyskać więcej informacji o platformie Microsoft Azure za pomocą konta organizacyjnego, zobacz [utworzyć konto Microsoft Azure jako organizacja](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="e40fc-152">Jeśli masz wiele subskrypcji i chcesz określić, która ma być używana przez usługę Azure Key Vault, wpisz następujące polecenie, aby zobaczyć subskrypcje przypisane do konta:</span><span class="sxs-lookup"><span data-stu-id="e40fc-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="e40fc-153">Aby określić subskrypcję, która ma być używana, wpisz polecenie:</span><span class="sxs-lookup"><span data-stu-id="e40fc-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="e40fc-154">Aby uzyskać więcej informacji o konfigurowaniu Azure Międzyplatformowego interfejsu wiersza polecenia, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia i Platform Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="e40fc-155">Przełącz się do korzystania z usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e40fc-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="e40fc-156">Magazyn kluczy wymaga usługi Azure Resource Manager, dlatego wpisz następujące polecenie, aby włączyć tryb usługi Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e40fc-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="e40fc-157">Utworzenie nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e40fc-157">Create a new resource group</span></span>
<span data-ttu-id="e40fc-158">Podczas korzystania z usługi Azure Resource Manager, wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e40fc-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="e40fc-159">W tym samouczku utworzymy nową grupę zasobów "ContosoResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="e40fc-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="e40fc-160">Pierwszym parametrem jest nazwa grupy zasobów, a drugi parametr jest lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="e40fc-161">Dla lokalizacji, użyj polecenia `azure location list` do identyfikowania sposobu Określ alternatywną lokalizację do tego, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e40fc-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="e40fc-162">Aby uzyskać więcej informacji, wpisz:`azure help location`</span><span class="sxs-lookup"><span data-stu-id="e40fc-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="e40fc-163">Rejestrowanie dostawcy zasobów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e40fc-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="e40fc-164">Upewnij się, że tego dostawcy zasobów usługi Key Vault jest zarejestrowany w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="e40fc-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="e40fc-165">To tylko należy jednak wykonać jeden raz dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="e40fc-166">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e40fc-166">Create a key vault</span></span>

<span data-ttu-id="e40fc-167">Użyj `azure keyvault create` polecenie, aby utworzyć magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="e40fc-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="e40fc-168">Ten skrypt ma trzy obowiązkowe parametry: Nazwa grupy zasobów, nazwa magazynu kluczy i lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="e40fc-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="e40fc-169">Na przykład jeśli używasz nazwy magazynu ContosoKeyVault, nazwę grupy zasobów ContosoResourceGroup i lokalizacji Azja Wschodnia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="e40fc-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="e40fc-170">Dane wyjściowe tego polecenia są wyświetlane właściwości magazynu kluczy, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="e40fc-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="e40fc-171">Dwie najważniejsze właściwości to:</span><span class="sxs-lookup"><span data-stu-id="e40fc-171">The two most important properties are:</span></span>

* <span data-ttu-id="e40fc-172">**Nazwa**: W tym przykładzie jest to ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="e40fc-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="e40fc-173">Ta nazwa będzie używana do innych poleceń cmdlet usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e40fc-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="e40fc-174">**vaultUri**: W tym przykładzie jest to https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="e40fc-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="e40fc-175">Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="e40fc-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="e40fc-176">Twoje konto platformy Azure ma teraz uprawnienia do wykonywania dowolnych operacji na tym magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="e40fc-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="e40fc-177">Nikt inny nie jest do tego upoważniony.</span><span class="sxs-lookup"><span data-stu-id="e40fc-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="e40fc-178">Dodawanie klucza lub klucza tajnego do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e40fc-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="e40fc-179">Usługa Azure Key Vault utworzenie klucza chronionego przez oprogramowanie do, należy użyć `azure key create` polecenia i wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e40fc-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="e40fc-180">Jednak jeśli masz istniejący klucz w pliku PEM, zapisany jako plik lokalny w pliku o nazwie softkey.pem, który chcesz przekazać do usługi Azure Key Vault, wpisz następujące polecenie, aby zaimportować klucz z. Plik PEM, który chroni klucz przez oprogramowanie w usłudze Key Vault:</span><span class="sxs-lookup"><span data-stu-id="e40fc-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="e40fc-181">Teraz możesz odwoływać się klucz, który został utworzony lub przekazany do usługi Azure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="e40fc-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="e40fc-182">Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** aby zawsze uzyskać bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** uzyskać tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="e40fc-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="e40fc-183">Aby dodać klucza tajnego w magazynie, który jest hasłem o nazwie SQLPassword i ma wartość z Pa$ $w0rd do usługi Azure Key Vault, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e40fc-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="e40fc-184">Teraz możesz odwoływać się do hasła dodanego do usługi Azure Key Vault za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="e40fc-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="e40fc-185">Użyj adresu **https://ContosoVault.vault.azure.net/secrets/SQLPassword**, aby zawsze uzyskać bieżącą wersję, oraz adresu **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**, aby uzyskać tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="e40fc-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="e40fc-186">Teraz wyświetlić klucz lub klucz tajny, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="e40fc-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="e40fc-187">Aby wyświetlić klucz, wpisz polecenie: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="e40fc-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="e40fc-188">Aby wyświetlić klucz tajny, wpisz polecenie: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="e40fc-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="e40fc-189">Rejestrowanie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e40fc-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="e40fc-190">Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e40fc-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="e40fc-191">Nie jest specyficzne dla usługi Azure Key Vault, ale został tu zawarty, aby informacje były kompletne.</span><span class="sxs-lookup"><span data-stu-id="e40fc-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e40fc-192">Aby ukończyć samouczek, Twoje konto, magazyn i aplikacja, która zostanie zarejestrowana w tym kroku, muszą należeć do tego samego katalogu Azure.</span><span class="sxs-lookup"><span data-stu-id="e40fc-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="e40fc-193">Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e40fc-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="e40fc-194">Aby to zrobić, właściciel aplikacji musi najpierw zarejestrować ją w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e40fc-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="e40fc-195">Na koniec rejestracji właściciel aplikacji otrzymuje następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="e40fc-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="e40fc-196">**Identyfikator aplikacji** (znany także jako Identyfikator klienta) oraz **klucz uwierzytelniania** (znany także jako wspólny klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="e40fc-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="e40fc-197">Aplikacja musi przedstawić obie te wartości do usługi Azure Active Directory, aby uzyskać token.</span><span class="sxs-lookup"><span data-stu-id="e40fc-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="e40fc-198">Sposób konfiguracji aplikacji w tym celu zależy od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="e40fc-199">W przypadku przykładowej aplikacji usługi Key Vault właściciel aplikacji ustawia te wartości w pliku app.config.</span><span class="sxs-lookup"><span data-stu-id="e40fc-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="e40fc-200">Aby zarejestrować aplikację w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="e40fc-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="e40fc-201">Zaloguj się do Portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e40fc-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="e40fc-202">Po lewej stronie kliknij pozycję **Usługa Active Directory**, a następnie wybierz katalog, w którym chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="e40fc-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="e40fc-203">Musi wybrać ten sam katalog, który zawiera subskrypcję platformy Azure, z którym zostanie utworzony magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="e40fc-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="e40fc-204">Jeśli nie wiesz, który to katalog, kliknij pozycję **Ustawienia**, zidentyfikuj subskrypcję, za pomocą której został utworzony magazyn kluczy, i zanotuj nazwę katalogu wyświetloną w ostatniej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="e40fc-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="e40fc-205">Kliknij pozycję **APLIKACJE**.</span><span class="sxs-lookup"><span data-stu-id="e40fc-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="e40fc-206">Jeśli nie aplikacja nie została dodana do katalogu, ta strona będzie wyświetlany tylko **Dodaj aplikację** łącza.</span><span class="sxs-lookup"><span data-stu-id="e40fc-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="e40fc-207">Kliknij link lub Alternatywnie możesz kliknąć **dodać** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="e40fc-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="e40fc-208">W kreatorze **DODAWANIE APLIKACJI** na stronie **Co chcesz zrobić?** kliknij pozycję **Dodawanie aplikacji opracowywanej przez moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="e40fc-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="e40fc-209">Na **Powiedz nam o aplikacji** , określ nazwę aplikacji i wybrać opcję **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="e40fc-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="e40fc-210">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="e40fc-210">Click the Next icon.</span></span>
6. <span data-ttu-id="e40fc-211">Na stronie **Właściwości aplikacji** określ **ADRES URL LOGOWANIA** i **IDENTYFIKATOR URI APLIKACJI** dla swojej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e40fc-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="e40fc-212">Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach).</span><span class="sxs-lookup"><span data-stu-id="e40fc-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="e40fc-213">Nie ma znaczenia, czy taka strona istnieje. Ważne jest, aby każda aplikacja w katalogu miała inny identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="e40fc-214">Katalog używa tego ciągu do identyfikowania Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e40fc-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="e40fc-215">Kliknij ikonę ukończone, aby zapisać zmiany w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="e40fc-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="e40fc-216">Na stronie Szybki Start kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="e40fc-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="e40fc-217">Przewiń do sekcji **Klucze**, wybierz czas trwania, a następnie kliknij przycisk **ZAPISZ**.</span><span class="sxs-lookup"><span data-stu-id="e40fc-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="e40fc-218">Strona zostanie odświeżona i pojawi się na niej wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="e40fc-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="e40fc-219">Musisz skonfigurować aplikację przy użyciu tej wartości klucza i wartości **IDENTYFIKATOR KLIENTA**.</span><span class="sxs-lookup"><span data-stu-id="e40fc-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="e40fc-220">(Instrukcje dotyczące tej konfiguracji będą specyficzne dla aplikacji).</span><span class="sxs-lookup"><span data-stu-id="e40fc-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="e40fc-221">Skopiuj wartość identyfikatora klienta z tej strony. Użyjesz jej w następnym kroku w celu ustawienia uprawnień dotyczących magazynu.</span><span class="sxs-lookup"><span data-stu-id="e40fc-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="e40fc-222">Zezwalanie aplikacji na używanie klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="e40fc-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="e40fc-223">Aby zezwolić aplikacji na dostęp do klucza lub klucza tajnego w magazynie, użyj `azure keyvault set-policy` polecenia.</span><span class="sxs-lookup"><span data-stu-id="e40fc-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="e40fc-224">Na przykład jeśli nazwa Twojego magazynu to ContosoKeyVault i aplikacji, które chcesz autoryzować ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i chcesz zezwolić aplikacji na odszyfrowywanie oraz logowanie z kluczy w magazynie, następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e40fc-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="e40fc-225">Uruchamiasz w wierszu polecenia systemu Windows, należy zastąpić pojedynczych cudzysłowów podwójnych cudzysłowów i również wprowadzić wewnętrzny cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="e40fc-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="e40fc-226">Na przykład: "[\"odszyfrować\",\"znak\"]".</span><span class="sxs-lookup"><span data-stu-id="e40fc-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="e40fc-227">Jeśli chcesz zezwolić tej samej aplikacji na odczyt kluczy tajnych w magazynie, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e40fc-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="e40fc-228">Użycie sprzętowego modułu zabezpieczeń (HSM, hardware security module)</span><span class="sxs-lookup"><span data-stu-id="e40fc-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="e40fc-229">W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM.</span><span class="sxs-lookup"><span data-stu-id="e40fc-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="e40fc-230">Moduły HSM są zweryfikowane w trybie FIPS 140-2 poziom 2.</span><span class="sxs-lookup"><span data-stu-id="e40fc-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="e40fc-231">Jeżeli te wymagania nie odnoszą się do Ciebie, pomiń tę sekcję i przejdź do sekcji [Usuwanie magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="e40fc-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="e40fc-232">Aby utworzyć te klucze chronione przez moduł HSM, musi mieć subskrypcję magazynu obsługującą klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="e40fc-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="e40fc-233">Podczas tworzenia keyvault, Dodaj parametr "sku":</span><span class="sxs-lookup"><span data-stu-id="e40fc-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="e40fc-234">Do tego magazynu możesz dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) oraz klucze chronione modułem HSM.</span><span class="sxs-lookup"><span data-stu-id="e40fc-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="e40fc-235">Aby utworzyć klucz chroniony przez moduł HSM, ustaw dla parametru docelowego "HSM":</span><span class="sxs-lookup"><span data-stu-id="e40fc-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="e40fc-236">Następujące polecenie służy do importowania klucza z pliku PEM, na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e40fc-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="e40fc-237">To polecenie importuje klucz do modułu HSM w usłudze Key Vault:</span><span class="sxs-lookup"><span data-stu-id="e40fc-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="e40fc-238">Następne polecenie importuje pakiet „Wprowadź własny klucz” (BYOK, bring your own key).</span><span class="sxs-lookup"><span data-stu-id="e40fc-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="e40fc-239">Umożliwia to wygenerowanie własnego klucza w lokalnym module HSM i przeniesienie go do modułów HSM w usłudze Key Vault bez opuszczania przez klucz granic modułu HSM:</span><span class="sxs-lookup"><span data-stu-id="e40fc-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="e40fc-240">Aby uzyskać szczegółowe instrukcje na temat generowania pakietu BYOK, zobacz [sposobu korzystania z usługi Azure Key Vault HSM-Protected klucze](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="e40fc-241">Usuwanie magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="e40fc-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="e40fc-242">Jeśli nie są już potrzebne magazynu kluczy oraz klucz lub klucz tajny, który zawiera można usunąć magazynu kluczy za pomocą polecenia delete azure keyvault:</span><span class="sxs-lookup"><span data-stu-id="e40fc-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="e40fc-243">Możesz także usunąć całą grupę zasobów platformy Azure zawierającą magazyn kluczy oraz inne zasoby, które zostały dodane do tej grupy:</span><span class="sxs-lookup"><span data-stu-id="e40fc-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="e40fc-244">Inne polecenia interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="e40fc-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="e40fc-245">Inne polecenia użytkownik może przydatne do zarządzania usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e40fc-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="e40fc-246">To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="e40fc-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="e40fc-247">To polecenie wyświetla pełną listę właściwości dla określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="e40fc-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="e40fc-248">To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="e40fc-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="e40fc-249">Poniżej przedstawiono przykładowy sposób usunięcia określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="e40fc-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="e40fc-250">Poniżej przedstawiono przykładowy sposób usunięcia określonego klucza tajnego:</span><span class="sxs-lookup"><span data-stu-id="e40fc-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="e40fc-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e40fc-251">Next steps</span></span>
<span data-ttu-id="e40fc-252">Odwołania dotyczące programowania znajdują się w [przewodniku dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e40fc-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

