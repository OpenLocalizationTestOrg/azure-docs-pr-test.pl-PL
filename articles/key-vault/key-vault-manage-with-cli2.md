---
title: "Zarządzanie usługą Azure Key Vault przy użyciu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka do automatyzacji typowych zadań w Key Vault za pomocą interfejsu wiersza polecenia 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="015f6-103">Zarządzanie za pomocą interfejsu wiersza polecenia 2.0 magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="015f6-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="015f6-104">Usługa Azure Key Vault jest dostępna w większości regionów.</span><span class="sxs-lookup"><span data-stu-id="015f6-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="015f6-105">Aby uzyskać więcej informacji, zobacz stronę [Cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="015f6-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="015f6-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="015f6-106">Introduction</span></span>
<span data-ttu-id="015f6-107">Ten samouczek ułatwi Ci rozpoczęcie pracy z usługą Azure Key Vault w celu utworzenia wzmocnionego kontenera (magazynu) na platformie Azure do przechowywania kluczy kryptograficznych i kluczy tajnych na platformie Azure oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="015f6-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="015f6-108">Przeprowadza użytkownika przez proces tworzenia magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure przy użyciu interfejsu wiersza polecenia platformy Azure i Platform.</span><span class="sxs-lookup"><span data-stu-id="015f6-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="015f6-109">Następnie pokaże Ci, jak aplikacja może następnie użyć tego klucza lub hasła.</span><span class="sxs-lookup"><span data-stu-id="015f6-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="015f6-110">**Szacowany czas trwania:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="015f6-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="015f6-111">Ten samouczek nie zawiera instrukcji dotyczących sposobu pisania aplikacji Azure, że jeden z kroków zawiera, który pokazuje, jak zezwolić aplikacji na używanie klucza lub klucza tajnego w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="015f6-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="015f6-112">W tym samouczku korzysta z najnowszej 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="015f6-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="015f6-113">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="015f6-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="015f6-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="015f6-114">Prerequisites</span></span>
<span data-ttu-id="015f6-115">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="015f6-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="015f6-116">Subskrypcja platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="015f6-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="015f6-117">Jeśli nie masz, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="015f6-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="015f6-118">Interfejs wiersza polecenia w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="015f6-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="015f6-119">Aby zainstalować najnowszą wersję i nawiązać połączenia z subskrypcją platformy Azure, zobacz [Instalowanie i konfigurowanie Azure 2.0 interfejsu wiersza polecenia i Platform](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="015f6-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="015f6-120">Aplikacja, która zostanie skonfigurowana w celu używania klucza lub hasła utworzonego w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="015f6-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="015f6-121">Przykładowa aplikacja jest dostępna w [Centrum pobierania Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="015f6-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="015f6-122">Aby uzyskać instrukcje, zobacz załączony plik Readme.</span><span class="sxs-lookup"><span data-stu-id="015f6-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="015f6-123">Uzyskiwanie pomocy z interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="015f6-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="015f6-124">Ten samouczek zakłada, że znasz interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="015f6-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="015f6-125">Parametru pomocy lub -h można wyświetlić Pomoc dla określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="015f6-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="015f6-126">Alternatywnie azure help [polecenie] [opcje] format również może zostać użyty do zwrócenia tych samych informacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="015f6-127">Na przykład poniższe polecenia wszystkie zwracają te same informacje:</span><span class="sxs-lookup"><span data-stu-id="015f6-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="015f6-128">W razie wątpliwości o parametry wymagane przez polecenie, zajrzyj do pomocy, przy użyciu — pomoc, -h lub az help [polecenie].</span><span class="sxs-lookup"><span data-stu-id="015f6-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="015f6-129">Możesz przeczytać następujące samouczki, aby zapoznać się z usługą Azure Resource Manager w interfejsu wiersza polecenia platformy Azure i Platform:</span><span class="sxs-lookup"><span data-stu-id="015f6-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="015f6-130">Instalowanie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="015f6-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="015f6-131">Wprowadzenie do usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="015f6-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="015f6-132">Nawiązywanie połączenia z subskrypcjami</span><span class="sxs-lookup"><span data-stu-id="015f6-132">Connect to your subscriptions</span></span>
<span data-ttu-id="015f6-133">Aby zalogować się przy użyciu konta organizacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="015f6-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="015f6-134">lub jeśli chcesz się zalogować, wpisując interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="015f6-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="015f6-135">Jeśli masz wiele subskrypcji i chcesz określić, która ma być używana przez usługę Azure Key Vault, wpisz następujące polecenie, aby zobaczyć subskrypcje przypisane do konta:</span><span class="sxs-lookup"><span data-stu-id="015f6-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="015f6-136">Aby określić subskrypcję, która ma być używana, wpisz polecenie:</span><span class="sxs-lookup"><span data-stu-id="015f6-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="015f6-137">Aby uzyskać więcej informacji o konfigurowaniu Azure Międzyplatformowego interfejsu wiersza polecenia, zobacz [instalowanie interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="015f6-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="015f6-138">Utworzenie nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="015f6-138">Create a new resource group</span></span>
<span data-ttu-id="015f6-139">Podczas korzystania z usługi Azure Resource Manager, wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="015f6-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="015f6-140">W tym samouczku utworzymy nową grupę zasobów "ContosoResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="015f6-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="015f6-141">Pierwszym parametrem jest nazwa grupy zasobów, a drugi parametr jest lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="015f6-142">Dla lokalizacji, użyj polecenia `az account list-locations` do identyfikowania sposobu Określ alternatywną lokalizację do tego, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="015f6-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="015f6-143">Aby uzyskać więcej informacji, wpisz: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="015f6-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="015f6-144">Rejestrowanie dostawcy zasobów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="015f6-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="015f6-145">Upewnij się, że tego dostawcy zasobów usługi Key Vault jest zarejestrowany w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="015f6-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="015f6-146">To tylko należy jednak wykonać jeden raz dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="015f6-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="015f6-147">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="015f6-147">Create a key vault</span></span>
<span data-ttu-id="015f6-148">Użyj `az keyvault create` polecenie, aby utworzyć magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="015f6-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="015f6-149">Ten skrypt ma trzy obowiązkowe parametry: Nazwa grupy zasobów, nazwa magazynu kluczy i lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="015f6-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="015f6-150">Na przykład jeśli używasz nazwy magazynu ContosoKeyVault, nazwę grupy zasobów ContosoResourceGroup i lokalizacji Azja Wschodnia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="015f6-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="015f6-151">Dane wyjściowe tego polecenia są wyświetlane właściwości magazynu kluczy, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="015f6-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="015f6-152">Dwie najważniejsze właściwości to:</span><span class="sxs-lookup"><span data-stu-id="015f6-152">The two most important properties are:</span></span>

* <span data-ttu-id="015f6-153">**Nazwa**: W tym przykładzie jest to ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="015f6-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="015f6-154">Użyje tej nazwy dla innych poleceń usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="015f6-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="015f6-155">**vaultUri**: W tym przykładzie jest to https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="015f6-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="015f6-156">Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="015f6-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="015f6-157">Twoje konto platformy Azure ma teraz uprawnienia do wykonywania dowolnych operacji na tym magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="015f6-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="015f6-158">Nikt inny nie jest do tego upoważniony.</span><span class="sxs-lookup"><span data-stu-id="015f6-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="015f6-159">Dodawanie klucza lub klucza tajnego do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="015f6-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="015f6-160">Usługa Azure Key Vault utworzenie klucza chronionego przez oprogramowanie do, należy użyć `az key create` polecenia i wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="015f6-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="015f6-161">Jednak jeśli masz istniejący klucz w pliku PEM, zapisany jako plik lokalny w pliku o nazwie softkey.pem, który chcesz przekazać do usługi Azure Key Vault, wpisz następujące polecenie, aby zaimportować klucz z. Plik PEM, który chroni klucz przez oprogramowanie w usłudze Key Vault:</span><span class="sxs-lookup"><span data-stu-id="015f6-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="015f6-162">Teraz możesz odwoływać się klucz, który został utworzony lub przekazany do usługi Azure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="015f6-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="015f6-163">Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** aby zawsze uzyskać bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** uzyskać tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="015f6-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="015f6-164">Aby dodać klucza tajnego w magazynie, który jest hasłem o nazwie SQLPassword i ma wartość z Pa$ $w0rd do usługi Azure Key Vault, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="015f6-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="015f6-165">Teraz możesz odwoływać się do hasła dodanego do usługi Azure Key Vault za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="015f6-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="015f6-166">Użyj adresu **https://ContosoVault.vault.azure.net/secrets/SQLPassword**, aby zawsze uzyskać bieżącą wersję, oraz adresu **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**, aby uzyskać tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="015f6-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="015f6-167">Teraz wyświetlić klucz lub klucz tajny, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="015f6-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="015f6-168">Aby wyświetlić klucz, wpisz polecenie: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="015f6-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="015f6-169">Aby wyświetlić klucz tajny, wpisz polecenie: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="015f6-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="015f6-170">Rejestrowanie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="015f6-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="015f6-171">Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="015f6-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="015f6-172">Nie jest specyficzne dla usługi Azure Key Vault, ale został tu zawarty, aby informacje były kompletne.</span><span class="sxs-lookup"><span data-stu-id="015f6-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="015f6-173">Aby ukończyć samouczek, Twoje konto, magazyn i aplikacja, która zostanie zarejestrowana w tym kroku, muszą należeć do tego samego katalogu Azure.</span><span class="sxs-lookup"><span data-stu-id="015f6-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="015f6-174">Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="015f6-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="015f6-175">Aby to zrobić, właściciel aplikacji musi najpierw zarejestrować ją w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="015f6-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="015f6-176">Na koniec rejestracji właściciel aplikacji otrzymuje następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="015f6-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="015f6-177">**Identyfikator aplikacji** (znany także jako Identyfikator klienta) oraz **klucz uwierzytelniania** (znany także jako wspólny klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="015f6-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="015f6-178">Aplikacja musi przedstawić obie te wartości do usługi Azure Active Directory, aby uzyskać token.</span><span class="sxs-lookup"><span data-stu-id="015f6-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="015f6-179">Sposób konfiguracji aplikacji w tym celu zależy od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="015f6-180">W przypadku przykładowej aplikacji usługi Key Vault właściciel aplikacji ustawia te wartości w pliku app.config.</span><span class="sxs-lookup"><span data-stu-id="015f6-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="015f6-181">Aby zarejestrować aplikację w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="015f6-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="015f6-182">Zaloguj się do Portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="015f6-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="015f6-183">Po lewej stronie, kliknij przycisk **usługi Azure Active Directory**, a następnie wybierz katalog, w którym będzie rejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="015f6-184">Musi wybrać ten sam katalog, który zawiera subskrypcję platformy Azure, z którym zostanie utworzony magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="015f6-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="015f6-185">Jeśli nie wiesz, który to katalog, kliknij pozycję **Ustawienia**, zidentyfikuj subskrypcję, za pomocą której został utworzony magazyn kluczy, i zanotuj nazwę katalogu wyświetloną w ostatniej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="015f6-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="015f6-186">Kliknij pozycję **APLIKACJE**.</span><span class="sxs-lookup"><span data-stu-id="015f6-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="015f6-187">Jeśli nie aplikacja nie została dodana do katalogu, ta strona będzie wyświetlany tylko **Dodaj aplikację** łącza.</span><span class="sxs-lookup"><span data-stu-id="015f6-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="015f6-188">Kliknij link lub Alternatywnie możesz kliknąć **dodać** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="015f6-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="015f6-189">W kreatorze **DODAWANIE APLIKACJI** na stronie **Co chcesz zrobić?** kliknij pozycję **Dodawanie aplikacji opracowywanej przez moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="015f6-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="015f6-190">Na **Powiedz nam o aplikacji** , określ nazwę aplikacji i wybrać opcję **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="015f6-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="015f6-191">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="015f6-191">Click the Next icon.</span></span>
6. <span data-ttu-id="015f6-192">Na stronie **Właściwości aplikacji** określ **ADRES URL LOGOWANIA** i **IDENTYFIKATOR URI APLIKACJI** dla swojej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="015f6-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="015f6-193">Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach).</span><span class="sxs-lookup"><span data-stu-id="015f6-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="015f6-194">Nie ma znaczenia, czy taka strona istnieje. Ważne jest, aby każda aplikacja w katalogu miała inny identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="015f6-195">Katalog używa tego ciągu do identyfikowania Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="015f6-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="015f6-196">Kliknij ikonę ukończone, aby zapisać zmiany w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="015f6-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="015f6-197">Na stronie Szybki Start kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="015f6-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="015f6-198">Przewiń do sekcji **Klucze**, wybierz czas trwania, a następnie kliknij przycisk **ZAPISZ**.</span><span class="sxs-lookup"><span data-stu-id="015f6-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="015f6-199">Strona zostanie odświeżona i pojawi się na niej wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="015f6-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="015f6-200">Musisz skonfigurować aplikację przy użyciu tej wartości klucza i wartości **IDENTYFIKATOR KLIENTA**.</span><span class="sxs-lookup"><span data-stu-id="015f6-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="015f6-201">(Instrukcje dotyczące tej konfiguracji będą specyficzne dla aplikacji).</span><span class="sxs-lookup"><span data-stu-id="015f6-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="015f6-202">Skopiuj wartość identyfikatora klienta z tej strony. Użyjesz jej w następnym kroku w celu ustawienia uprawnień dotyczących magazynu.</span><span class="sxs-lookup"><span data-stu-id="015f6-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="015f6-203">Zezwalanie aplikacji na używanie klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="015f6-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="015f6-204">Aby zezwolić aplikacji na dostęp do klucza lub klucza tajnego w magazynie, użyj `az keyvault set-policy` polecenia.</span><span class="sxs-lookup"><span data-stu-id="015f6-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="015f6-205">Na przykład jeśli nazwa Twojego magazynu to ContosoKeyVault i aplikacji, które chcesz autoryzować ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i chcesz zezwolić aplikacji na odszyfrowywanie oraz logowanie z kluczy w magazynie, następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="015f6-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="015f6-206">Jeśli chcesz zezwolić tej samej aplikacji na odczyt kluczy tajnych w magazynie, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="015f6-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="015f6-207">Użycie sprzętowego modułu zabezpieczeń (HSM, hardware security module)</span><span class="sxs-lookup"><span data-stu-id="015f6-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="015f6-208">W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM.</span><span class="sxs-lookup"><span data-stu-id="015f6-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="015f6-209">Moduły HSM są zweryfikowane w trybie FIPS 140-2 poziom 2.</span><span class="sxs-lookup"><span data-stu-id="015f6-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="015f6-210">Jeżeli te wymagania nie odnoszą się do Ciebie, pomiń tę sekcję i przejdź do sekcji [Usuwanie magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="015f6-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="015f6-211">Aby utworzyć te klucze chronione przez moduł HSM, musi mieć subskrypcję magazynu obsługującą klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="015f6-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="015f6-212">Podczas tworzenia keyvault, Dodaj parametr "sku":</span><span class="sxs-lookup"><span data-stu-id="015f6-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="015f6-213">Do tego magazynu możesz dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) oraz klucze chronione modułem HSM.</span><span class="sxs-lookup"><span data-stu-id="015f6-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="015f6-214">Aby utworzyć klucz chroniony przez moduł HSM, ustaw dla parametru docelowego "HSM":</span><span class="sxs-lookup"><span data-stu-id="015f6-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="015f6-215">Następujące polecenie służy do importowania klucza z pliku PEM, na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="015f6-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="015f6-216">To polecenie importuje klucz do modułu HSM w usłudze Key Vault:</span><span class="sxs-lookup"><span data-stu-id="015f6-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="015f6-217">Następne polecenie importuje pakiet „Wprowadź własny klucz” (BYOK, bring your own key).</span><span class="sxs-lookup"><span data-stu-id="015f6-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="015f6-218">Umożliwia to wygenerowanie własnego klucza w lokalnym module HSM i przeniesienie go do modułów HSM w usłudze Key Vault bez opuszczania przez klucz granic modułu HSM:</span><span class="sxs-lookup"><span data-stu-id="015f6-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="015f6-219">Aby uzyskać szczegółowe instrukcje na temat generowania pakietu BYOK, zobacz [sposobu korzystania z usługi Azure Key Vault HSM-Protected klucze](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="015f6-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="015f6-220">Usuwanie magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="015f6-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="015f6-221">Jeśli nie są już potrzebne magazynu kluczy oraz klucz lub klucz tajny, który zawiera magazyn kluczy można usunąć za pomocą `az keyvault delete` polecenia:</span><span class="sxs-lookup"><span data-stu-id="015f6-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="015f6-222">Możesz także usunąć całą grupę zasobów platformy Azure zawierającą magazyn kluczy oraz inne zasoby, które zostały dodane do tej grupy:</span><span class="sxs-lookup"><span data-stu-id="015f6-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="015f6-223">Inne polecenia interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="015f6-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="015f6-224">Inne polecenia użytkownik może przydatne do zarządzania usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="015f6-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="015f6-225">To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="015f6-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="015f6-226">Lista kluczy keyvault az — nazwa magazynu "ContosoKeyVault"</span><span class="sxs-lookup"><span data-stu-id="015f6-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="015f6-227">To polecenie wyświetla pełną listę właściwości dla określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="015f6-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="015f6-228">Pokaż az keyvault klucza--"ContosoKeyVault'--Nazwa"ContosoFirstKey"Nazwa magazynu</span><span class="sxs-lookup"><span data-stu-id="015f6-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="015f6-229">To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="015f6-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="015f6-230">AZ keyvault poufne listy — Nazwa magazynu "ContosoKeyVault"</span><span class="sxs-lookup"><span data-stu-id="015f6-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="015f6-231">Poniżej przedstawiono przykładowy sposób usunięcia określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="015f6-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="015f6-232">usunięcia klucza keyvault az - magazynu name "ContosoKeyVault'--Nazwa"ContosoFirstKey"</span><span class="sxs-lookup"><span data-stu-id="015f6-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="015f6-233">Poniżej przedstawiono przykładowy sposób usunięcia określonego klucza tajnego:</span><span class="sxs-lookup"><span data-stu-id="015f6-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="015f6-234">Usuwanie klucza tajnego parametru keyvault az — magazyn name "ContosoKeyVault'--Nazwa"SQLPassword"</span><span class="sxs-lookup"><span data-stu-id="015f6-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="015f6-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="015f6-235">Next steps</span></span>
<span data-ttu-id="015f6-236">Aby uzyskać pełną dokumentację interfejsu wiersza polecenia Azure dla magazynu kluczy poleceń, zobacz [odwołanie klucza magazynu interfejsu wiersza polecenia](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="015f6-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="015f6-237">Odwołania dotyczące programowania znajdują się w [przewodniku dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="015f6-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
