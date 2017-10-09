---
title: "aaaManage magazynu kluczy Azure przy użyciu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Korzystanie z tego samouczka tooautomate typowych zadań usługi Key Vault, za pomocą hello 2.0 interfejsu wiersza polecenia"
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
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="c70eb-103">Zarządzanie za pomocą interfejsu wiersza polecenia 2.0 magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="c70eb-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="c70eb-104">Usługa Azure Key Vault jest dostępna w większości regionów.</span><span class="sxs-lookup"><span data-stu-id="c70eb-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="c70eb-105">Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c70eb-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="c70eb-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c70eb-106">Introduction</span></span>
<span data-ttu-id="c70eb-107">Użyj tego samouczka toohelp otrzymasz wprowadzenie do usługi Azure Key Vault toocreate wzmocnionego kontenera (magazynu) na platformie Azure, toostore i zarządzanie nimi kluczy kryptograficznych i kluczy tajnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="c70eb-108">Przeprowadza użytkownika przez proces hello przy użyciu interfejsu wiersza polecenia platformy Azure i Platform toocreate magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="c70eb-109">Następnie pokaże Ci, jak aplikacja może następnie użyć tego klucza lub hasła.</span><span class="sxs-lookup"><span data-stu-id="c70eb-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="c70eb-110">**Szacowany czas toocomplete:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="c70eb-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="c70eb-111">Ten samouczek nie zawiera instrukcji dotyczących sposobu toowrite hello aplikacji Azure, która zawiera jeden z kroków hello, który pokazuje, jak tooauthorize toouse aplikacji klucza lub klucza tajnego klucza hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="c70eb-112">Ten samouczek używa hello najnowsze 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="c70eb-113">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c70eb-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c70eb-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c70eb-114">Prerequisites</span></span>
<span data-ttu-id="c70eb-115">toocomplete tego samouczka, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c70eb-116">TooMicrosoft subskrypcji Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="c70eb-117">Jeśli nie masz, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="c70eb-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="c70eb-118">Interfejs wiersza polecenia w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c70eb-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="c70eb-119">tooinstall hello najnowszej wersji i połącz tooyour subskrypcji platformy Azure, zobacz [Instalowanie i konfigurowanie hello Azure 2.0 interfejsu wiersza polecenia i Platform](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c70eb-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="c70eb-120">Aplikacja, która będzie skonfigurowany toouse hello klucza lub hasła utworzonego w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c70eb-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="c70eb-121">Przykładowa aplikacja jest dostępna z hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="c70eb-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="c70eb-122">Aby uzyskać instrukcje Zobacz hello towarzyszący plik Readme.</span><span class="sxs-lookup"><span data-stu-id="c70eb-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="c70eb-123">Uzyskiwanie pomocy z interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="c70eb-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="c70eb-124">Ten samouczek zakłada, że znasz hello interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="c70eb-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="c70eb-125">Witaj — pomoc lub -h parametr może być używany dla określonych poleceń tooview pomocy.</span><span class="sxs-lookup"><span data-stu-id="c70eb-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="c70eb-126">Alternatywnie hello azure help [polecenie] [opcje] format może być również używane tooreturn hello tych samych informacji.</span><span class="sxs-lookup"><span data-stu-id="c70eb-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="c70eb-127">Na przykład następujące hello polecenia wszystkie powrotu hello tych samych informacji:</span><span class="sxs-lookup"><span data-stu-id="c70eb-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="c70eb-128">W przypadku wątpliwości dotyczących parametrów hello potrzebne za pomocą polecenia można znaleźć przy użyciu toohelp — pomoc, -h lub az help [polecenie].</span><span class="sxs-lookup"><span data-stu-id="c70eb-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="c70eb-129">Możesz przeczytać następujące samouczki tooget zapoznać się z usługą Azure Resource Manager w interfejsu wiersza polecenia platformy Azure i Platform hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="c70eb-130">Instalowanie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c70eb-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="c70eb-131">Wprowadzenie do usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c70eb-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="c70eb-132">Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c70eb-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="c70eb-133">toolog za pomocą konta organizacyjnego, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c70eb-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="c70eb-134">lub jeśli użytkownik chce toolog wpisując interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="c70eb-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="c70eb-135">Jeśli masz wiele subskrypcji i chcesz toospecify określonych toouse jeden dla usługi Azure Key Vault, wpisz powitania po toosee hello subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="c70eb-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="c70eb-136">Następnie toospecify hello subskrypcji toouse, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c70eb-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="c70eb-137">Aby uzyskać więcej informacji o konfigurowaniu Azure Międzyplatformowego interfejsu wiersza polecenia, zobacz [instalowanie interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c70eb-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="c70eb-138">Utworzenie nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c70eb-138">Create a new resource group</span></span>
<span data-ttu-id="c70eb-139">Podczas korzystania z usługi Azure Resource Manager, wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c70eb-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="c70eb-140">W tym samouczku utworzymy nową grupę zasobów "ContosoResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="c70eb-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="c70eb-141">pierwszy parametr Hello jest nazwa grupy zasobów i hello drugi parametr jest hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c70eb-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="c70eb-142">Dla lokalizacji, użyj polecenia hello `az account list-locations` tooidentify jak toospecify alternatywną lokalizację toohello co w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c70eb-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="c70eb-143">Aby uzyskać więcej informacji, wpisz: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="c70eb-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="c70eb-144">Rejestrowanie dostawcy zasobów usługi Key Vault hello</span><span class="sxs-lookup"><span data-stu-id="c70eb-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="c70eb-145">Upewnij się, że tego dostawcy zasobów usługi Key Vault jest zarejestrowany w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="c70eb-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="c70eb-146">Wymagane tylko toobe wykonywane raz dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c70eb-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="c70eb-147">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="c70eb-147">Create a key vault</span></span>
<span data-ttu-id="c70eb-148">Użyj hello `az keyvault create` toocreate polecenie magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c70eb-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="c70eb-149">Ten skrypt ma trzy obowiązkowe parametry: Nazwa grupy zasobów, nazwa magazynu kluczy i hello lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="c70eb-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="c70eb-150">Na przykład jeśli używasz nazwy magazynu hello ContosoKeyVault, nazwę grupy zasobów hello ContosoResourceGroup i hello lokalizacji Azja Wschodnia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="c70eb-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="c70eb-151">Hello dane wyjściowe tego polecenia pokazują właściwości magazynu kluczy hello nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="c70eb-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="c70eb-152">Witaj dwie najważniejsze właściwości to:</span><span class="sxs-lookup"><span data-stu-id="c70eb-152">hello two most important properties are:</span></span>

* <span data-ttu-id="c70eb-153">**Nazwa**: W przykładzie hello jest ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="c70eb-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="c70eb-154">Użyje tej nazwy dla innych poleceń usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c70eb-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="c70eb-155">**vaultUri**: W przykładzie hello jest https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="c70eb-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="c70eb-156">Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c70eb-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="c70eb-157">Konto platformy Azure jest teraz autoryzowanych tooperform żadnych operacji dla tego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="c70eb-158">Nikt inny nie jest do tego upoważniony.</span><span class="sxs-lookup"><span data-stu-id="c70eb-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="c70eb-159">Dodawanie klucza lub magazynu kluczy tajnych toohello</span><span class="sxs-lookup"><span data-stu-id="c70eb-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="c70eb-160">Usługa Azure Key Vault toocreate klucza chronionego przez oprogramowanie dla Ciebie, należy użyć hello `az key create` polecenia i wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="c70eb-161">Jednak jeśli masz istniejący klucz w pliku PEM, zapisany jako plik lokalny w pliku o nazwie softkey.pem, które mają tooAzure tooupload Key Vault, wpisz powitania po klucz hello tooimport z hello. Plik PEM, który chroni klucz hello przez oprogramowanie w usłudze Key Vault hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="c70eb-162">Teraz możesz odwoływać się hello klucz został utworzony lub przekazany tooAzure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c70eb-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="c70eb-163">Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="c70eb-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="c70eb-164">tooadd magazynu toohello tajny, który jest hasłem o nazwie SQLPassword i ma hello wartość Pa$ $w0rd tooAzure Key Vault hello typu następujące:</span><span class="sxs-lookup"><span data-stu-id="c70eb-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="c70eb-165">Teraz możesz odwoływać się to hasło, dodać tooAzure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c70eb-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="c70eb-166">Użyj **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="c70eb-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="c70eb-167">Teraz wyświetlić hello klucz lub klucz tajny, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="c70eb-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="c70eb-168">tooview Twojego klucza, wpisz:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c70eb-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="c70eb-169">tooview tajne, typu:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c70eb-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="c70eb-170">Rejestrowanie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c70eb-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="c70eb-171">Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c70eb-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="c70eb-172">Nie jest określonym tooAzure Key Vault, ale został tu zawarty, aby informacje były kompletne.</span><span class="sxs-lookup"><span data-stu-id="c70eb-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c70eb-173">toocomplete hello samouczek, Twoje konto, Magazyn hello i aplikacji hello, która zarejestruje się w tym kroku musi być w hello tego samego katalogu Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="c70eb-174">Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c70eb-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="c70eb-175">toodo hello, właściciel aplikacji hello aplikacji hello najpierw należy zarejestrować w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c70eb-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="c70eb-176">Na powitania koniec rejestracji właściciel aplikacji hello pobiera hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c70eb-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="c70eb-177">**Identyfikator aplikacji** (znanej także jako identyfikator klienta) i **klucz uwierzytelniania** (znanej także jako hello wspólny klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="c70eb-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="c70eb-178">Witaj, aplikacja musi przedstawić obie te wartości tooAzure usługi Active Directory, tooget tokenu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="c70eb-179">Jak aplikacja hello jest skonfigurowany toodo, który zależy od aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c70eb-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="c70eb-180">Dla usługi Key Vault Przykładowa aplikacja hello hello właściciel aplikacji ustawia te wartości w pliku app.config hello.</span><span class="sxs-lookup"><span data-stu-id="c70eb-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="c70eb-181">Aplikacja hello tooregister w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c70eb-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="c70eb-182">Zaloguj się toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c70eb-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="c70eb-183">Powitania po lewej stronie, kliknij przycisk **usługi Azure Active Directory**, a następnie wybierz katalog hello, w którym będzie rejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c70eb-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="c70eb-184">Musisz wybrać hello tym samym katalogu, który zawiera hello subskrypcji platformy Azure, z którym zostanie utworzony magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="c70eb-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="c70eb-185">Jeśli nie znasz katalog ten jest, kliknij przycisk **ustawienia**zidentyfikować hello subskrypcji, z którym zostanie utworzony magazyn kluczy i w ostatniej kolumnie hello wyświetlana nazwa hello Uwaga hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="c70eb-186">Kliknij pozycję **APLIKACJE**.</span><span class="sxs-lookup"><span data-stu-id="c70eb-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="c70eb-187">Brak aplikacja nie została dodana tooyour katalogu, ta strona wyświetli tylko hello **Dodaj aplikację** łącza.</span><span class="sxs-lookup"><span data-stu-id="c70eb-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="c70eb-188">Kliknij łącze hello, lub też kliknąć hello **dodać** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="c70eb-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="c70eb-189">W hello **Dodawanie aplikacji** kreatora, na powitania **co chcesz toodo?** kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="c70eb-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="c70eb-190">Na powitania **Powiedz nam o aplikacji** , określ nazwę aplikacji i wybrać opcję **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (hello domyślną).</span><span class="sxs-lookup"><span data-stu-id="c70eb-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="c70eb-191">Kliknij ikonę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="c70eb-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="c70eb-192">Na powitania **właściwości aplikacji** Określ hello **adres URL logowania** i **identyfikator URI aplikacji** dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c70eb-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="c70eb-193">Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach).</span><span class="sxs-lookup"><span data-stu-id="c70eb-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="c70eb-194">Nie ma znaczenia, czy taka strona istnieje; ważne jest, aplikacja hello identyfikator URI dla każdej aplikacji jest różne dla każdej aplikacji w katalogu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="c70eb-195">katalog Hello używa tego ciągu tooidentify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c70eb-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="c70eb-196">Kliknij przycisk toosave pełną ikona hello zmiany w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="c70eb-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="c70eb-197">Na stronie Szybki Start powitania kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="c70eb-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="c70eb-198">Przewiń toohello **klucze** sekcji, wybierz czas trwania hello, a następnie kliknij przycisk **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="c70eb-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="c70eb-199">Strona Hello odświeżona i pojawi się wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="c70eb-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="c70eb-200">Należy skonfigurować aplikację za pomocą wartości klucza i hello **identyfikator klienta** wartość.</span><span class="sxs-lookup"><span data-stu-id="c70eb-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="c70eb-201">(Instrukcje dotyczące tej konfiguracji będą specyficzne dla aplikacji).</span><span class="sxs-lookup"><span data-stu-id="c70eb-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="c70eb-202">Skopiuj wartość Identyfikatora powitania klienta z tej strony, który będzie używany w hello następny krok tooset uprawnień dotyczących magazynu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="c70eb-203">Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="c70eb-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="c70eb-204">Witaj tooaccess aplikacji hello tooauthorize klucza lub klucza tajnego w magazynie hello, użyj hello `az keyvault set-policy` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c70eb-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="c70eb-205">Na przykład jeśli nazwa Twojego magazynu to ContosoKeyVault i hello aplikacji ma tooauthorize ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i toodecrypt aplikacji hello tooauthorize i zaloguj się za pomocą kluczy w magazynie, a następnie uruchom hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c70eb-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="c70eb-206">Jeśli chcesz tooauthorize tego samego hasła tooread aplikacji w magazynie, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="c70eb-207">Jeśli chcesz, aby toouse sprzętowego modułu zabezpieczeń (HSM)</span><span class="sxs-lookup"><span data-stu-id="c70eb-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="c70eb-208">Dla dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello.</span><span class="sxs-lookup"><span data-stu-id="c70eb-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="c70eb-209">Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany.</span><span class="sxs-lookup"><span data-stu-id="c70eb-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="c70eb-210">Jeśli te wymagania nie odnoszą się tooyou, Pomiń tę sekcję i przejdź zbyt[usunąć hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="c70eb-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="c70eb-211">toocreate klucze chronionego przez moduł HSM musi mieć subskrypcję magazynu obsługującą klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="c70eb-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="c70eb-212">Podczas tworzenia hello keyvault, Dodaj parametr "sku" hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="c70eb-213">Można dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) i magazynu toothis klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="c70eb-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="c70eb-214">toocreate klucza chronionego przez moduł HSM, zestaw hello przeznaczenia parametru too'HSM ":</span><span class="sxs-lookup"><span data-stu-id="c70eb-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="c70eb-215">Możesz użyć hello następujące polecenia tooimport klucz z pliku PEM na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c70eb-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="c70eb-216">To polecenie importuje klucz hello do sprzętowych modułów zabezpieczeń w usłudze Key Vault hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="c70eb-217">Witaj następne polecenie importuje "bring your own key" (BYOK) pakietu.</span><span class="sxs-lookup"><span data-stu-id="c70eb-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="c70eb-218">Umożliwia generowanie klucza w lokalnym module HSM i przeniesienie go tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="c70eb-219">Aby uzyskać szczegółowe instrukcje dotyczące toogenerate pakietu BYOK, zobacz [jak toouse HSM-Protected klucze w usłudze Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c70eb-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="c70eb-220">Usuń hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="c70eb-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="c70eb-221">Jeśli nie są już potrzebne hello magazynu kluczy oraz klucz hello lub klucz tajny, który zawiera, można usunąć magazynu kluczy hello za pomocą hello `az keyvault delete` polecenia:</span><span class="sxs-lookup"><span data-stu-id="c70eb-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="c70eb-222">Lub usunięciem całej grupy zasobów platformy Azure, w tym magazynie kluczy hello i inne zasoby, które zostały dodane do tej grupy:</span><span class="sxs-lookup"><span data-stu-id="c70eb-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="c70eb-223">Inne polecenia interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="c70eb-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="c70eb-224">Inne polecenia użytkownik może przydatne do zarządzania usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c70eb-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="c70eb-225">To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="c70eb-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="c70eb-226">Lista kluczy keyvault az — nazwa magazynu "ContosoKeyVault"</span><span class="sxs-lookup"><span data-stu-id="c70eb-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="c70eb-227">To polecenie wyświetla pełną listę właściwości dla określonego klucza hello:</span><span class="sxs-lookup"><span data-stu-id="c70eb-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="c70eb-228">Pokaż az keyvault klucza--"ContosoKeyVault'--Nazwa"ContosoFirstKey"Nazwa magazynu</span><span class="sxs-lookup"><span data-stu-id="c70eb-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="c70eb-229">To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="c70eb-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="c70eb-230">AZ keyvault poufne listy — Nazwa magazynu "ContosoKeyVault"</span><span class="sxs-lookup"><span data-stu-id="c70eb-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="c70eb-231">Poniżej przedstawiono przykładowy sposób tooremove określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="c70eb-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="c70eb-232">usunięcia klucza keyvault az - magazynu name "ContosoKeyVault'--Nazwa"ContosoFirstKey"</span><span class="sxs-lookup"><span data-stu-id="c70eb-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="c70eb-233">Poniżej przedstawiono przykładowy sposób tooremove określonego klucza tajnego:</span><span class="sxs-lookup"><span data-stu-id="c70eb-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="c70eb-234">Usuwanie klucza tajnego parametru keyvault az — magazyn name "ContosoKeyVault'--Nazwa"SQLPassword"</span><span class="sxs-lookup"><span data-stu-id="c70eb-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="c70eb-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c70eb-235">Next steps</span></span>
<span data-ttu-id="c70eb-236">Aby uzyskać pełną dokumentację interfejsu wiersza polecenia Azure dla magazynu kluczy poleceń, zobacz [odwołanie klucza magazynu interfejsu wiersza polecenia](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="c70eb-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="c70eb-237">Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c70eb-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
