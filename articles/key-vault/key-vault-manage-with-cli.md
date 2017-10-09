---
title: "aaaManage magazynu kluczy Azure przy użyciu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Korzystanie z tego samouczka tooautomate typowych zadań usługi Key Vault, za pomocą hello interfejsu wiersza polecenia"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="d0da1-103">Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d0da1-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="d0da1-104">Usługa Azure Key Vault jest dostępna w większości regionów.</span><span class="sxs-lookup"><span data-stu-id="d0da1-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="d0da1-105">Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="d0da1-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="d0da1-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d0da1-106">Introduction</span></span>

<span data-ttu-id="d0da1-107">Użyj tego samouczka toohelp otrzymasz wprowadzenie do usługi Azure Key Vault toocreate wzmocnionego kontenera (magazynu) na platformie Azure, toostore i zarządzanie nimi kluczy kryptograficznych i kluczy tajnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="d0da1-108">Przeprowadza użytkownika przez proces hello przy użyciu interfejsu wiersza polecenia platformy Azure i Platform toocreate magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="d0da1-109">Następnie pokaże Ci, jak aplikacja może następnie użyć tego klucza lub hasła.</span><span class="sxs-lookup"><span data-stu-id="d0da1-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="d0da1-110">**Szacowany czas toocomplete:** 20 minut</span><span class="sxs-lookup"><span data-stu-id="d0da1-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="d0da1-111">Ten samouczek nie zawiera instrukcji dotyczących sposobu toowrite hello aplikacji Azure, która zawiera jeden z kroków hello, który pokazuje, jak tooauthorize toouse aplikacji klucza lub klucza tajnego klucza hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="d0da1-112">Obecnie nie można skonfigurować usługi Azure Key Vault w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="d0da1-113">Użyj tych instrukcji Międzyplatformowego interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d0da1-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="d0da1-114">Lub, aby uzyskać instrukcje programu Azure PowerShell, zobacz [tym równoważnym samouczku](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="d0da1-115">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d0da1-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0da1-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0da1-116">Prerequisites</span></span>

<span data-ttu-id="d0da1-117">toocomplete tego samouczka, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d0da1-118">TooMicrosoft subskrypcji Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="d0da1-119">Jeśli nie masz, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="d0da1-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="d0da1-120">Interfejs wiersza polecenia w wersji od 0.9.1 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="d0da1-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="d0da1-121">tooinstall hello najnowszej wersji i połącz tooyour subskrypcji platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia platformy Azure i Platform hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="d0da1-122">Aplikacja, która będzie skonfigurowany toouse hello klucza lub hasła utworzonego w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d0da1-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="d0da1-123">Przykładowa aplikacja jest dostępna z hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="d0da1-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="d0da1-124">Aby uzyskać instrukcje Zobacz hello towarzyszący plik Readme.</span><span class="sxs-lookup"><span data-stu-id="d0da1-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="d0da1-125">Uzyskiwanie pomocy z interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="d0da1-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="d0da1-126">Ten samouczek zakłada, że znasz hello interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="d0da1-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="d0da1-127">Witaj — pomoc lub -h parametr może być używany dla określonych poleceń tooview pomocy.</span><span class="sxs-lookup"><span data-stu-id="d0da1-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="d0da1-128">Alternatywnie hello azure help [polecenie] [opcje] format może być również używane tooreturn hello tych samych informacji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="d0da1-129">Na przykład następujące hello polecenia wszystkie powrotu hello tych samych informacji:</span><span class="sxs-lookup"><span data-stu-id="d0da1-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="d0da1-130">W przypadku wątpliwości dotyczących parametrów hello potrzebne za pomocą polecenia można znaleźć przy użyciu toohelp — pomoc, -h lub azure help [polecenie].</span><span class="sxs-lookup"><span data-stu-id="d0da1-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="d0da1-131">Możesz przeczytać następujące samouczki tooget zapoznać się z usługą Azure Resource Manager w interfejsu wiersza polecenia platformy Azure i Platform hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="d0da1-132">Jak tooinstall i Konfigurowanie interfejsu wiersza polecenia i Platform Azure</span><span class="sxs-lookup"><span data-stu-id="d0da1-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="d0da1-133">Przy użyciu interfejsu wiersza polecenia platformy Azure i Platform z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0da1-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="d0da1-134">Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d0da1-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="d0da1-135">toolog za pomocą konta organizacyjnego, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d0da1-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="d0da1-136">lub jeśli użytkownik chce toolog wpisując interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="d0da1-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="d0da1-137">Metoda logowania Hello działa tylko za pomocą konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0da1-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="d0da1-138">Konta organizacyjnego jest użytkownik, który jest zarządzanych przez swoją organizację, a zdefiniowane w dzierżawie usługi Azure Active Directory w organizacji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="d0da1-139">Jeśli aktualnie nie masz konta organizacyjnego i przy użyciu toolog konta Microsoft w tooyour subskrypcji platformy Azure, można łatwo utworzyć go przy użyciu hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d0da1-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="d0da1-140">Logowania toohello logowania toohello [portalu zarządzania Azure](https://manage.windowsazure.com/)i kliknij na usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0da1-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="d0da1-141">Jeśli katalog nie istnieje, wybierz opcję tworzenia katalogu i podaj hello wymagane informacje.</span><span class="sxs-lookup"><span data-stu-id="d0da1-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="d0da1-142">Wybierz katalog, a następnie dodaj nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0da1-142">Select your directory and add a new user.</span></span> <span data-ttu-id="d0da1-143">Ten nowy użytkownik jest kontem organizacyjnym.</span><span class="sxs-lookup"><span data-stu-id="d0da1-143">This new user is an organizational account.</span></span> <span data-ttu-id="d0da1-144">Podczas tworzenia hello hello użytkownika należy podać zarówno adres e-mail dla hello użytkownika i hasło tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="d0da1-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="d0da1-145">Zapisz te informacje, które jest używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="d0da1-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="d0da1-146">W portalu hello wybierz ustawienia, a następnie wybierz administratorów.</span><span class="sxs-lookup"><span data-stu-id="d0da1-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="d0da1-147">Wybierz opcję Dodaj i dodania nowego użytkownika hello jako współadministrator.</span><span class="sxs-lookup"><span data-stu-id="d0da1-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="d0da1-148">Dzięki temu toomanage konta organizacyjnego hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="d0da1-149">Na koniec Wyloguj hello portalu Azure i następnie ponowne zalogowanie przy użyciu nowego konta organizacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="d0da1-150">Jeśli jest to hello pierwszego czasu logowania się za pomocą tego konta, będzie toochange zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="d0da1-151">Aby uzyskać więcej informacji o platformie Microsoft Azure za pomocą konta organizacyjnego, zobacz [utworzyć konto Microsoft Azure jako organizacja](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="d0da1-152">Jeśli masz wiele subskrypcji i chcesz toospecify określonych toouse jeden dla usługi Azure Key Vault, wpisz powitania po toosee hello subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="d0da1-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="d0da1-153">Następnie toospecify hello subskrypcji toouse, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d0da1-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="d0da1-154">Aby uzyskać więcej informacji o konfigurowaniu Azure Międzyplatformowego interfejsu wiersza polecenia, zobacz [jak tooInstall i Konfigurowanie interfejsu wiersza polecenia i Platform Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="d0da1-155">Przełącz toousing usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0da1-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="d0da1-156">Hello Key Vault wymaga usługi Azure Resource Manager, dlatego wpisz powitania po tryb usługi Resource Manager tooAzure tooswitch:</span><span class="sxs-lookup"><span data-stu-id="d0da1-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="d0da1-157">Utworzenie nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d0da1-157">Create a new resource group</span></span>
<span data-ttu-id="d0da1-158">Podczas korzystania z usługi Azure Resource Manager, wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d0da1-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="d0da1-159">W tym samouczku utworzymy nową grupę zasobów "ContosoResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="d0da1-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="d0da1-160">pierwszy parametr Hello jest nazwa grupy zasobów i hello drugi parametr jest hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="d0da1-161">Dla lokalizacji, użyj polecenia hello `azure location list` tooidentify jak toospecify alternatywną lokalizację toohello co w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d0da1-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="d0da1-162">Aby uzyskać więcej informacji, wpisz:`azure help location`</span><span class="sxs-lookup"><span data-stu-id="d0da1-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="d0da1-163">Rejestrowanie dostawcy zasobów usługi Key Vault hello</span><span class="sxs-lookup"><span data-stu-id="d0da1-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="d0da1-164">Upewnij się, że tego dostawcy zasobów usługi Key Vault jest zarejestrowany w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="d0da1-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="d0da1-165">Wymagane tylko toobe wykonywane raz dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="d0da1-166">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="d0da1-166">Create a key vault</span></span>

<span data-ttu-id="d0da1-167">Użyj hello `azure keyvault create` toocreate polecenie magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="d0da1-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="d0da1-168">Ten skrypt ma trzy obowiązkowe parametry: Nazwa grupy zasobów, nazwa magazynu kluczy i hello lokalizacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="d0da1-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="d0da1-169">Na przykład jeśli używasz nazwy magazynu hello ContosoKeyVault, nazwę grupy zasobów hello ContosoResourceGroup i hello lokalizacji Azja Wschodnia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="d0da1-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="d0da1-170">Hello dane wyjściowe tego polecenia pokazują właściwości magazynu kluczy hello nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="d0da1-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="d0da1-171">Witaj dwie najważniejsze właściwości to:</span><span class="sxs-lookup"><span data-stu-id="d0da1-171">hello two most important properties are:</span></span>

* <span data-ttu-id="d0da1-172">**Nazwa**: W przykładzie hello jest ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="d0da1-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="d0da1-173">Ta nazwa będzie używana do innych poleceń cmdlet usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d0da1-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="d0da1-174">**vaultUri**: W przykładzie hello jest https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="d0da1-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="d0da1-175">Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="d0da1-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="d0da1-176">Konto platformy Azure jest teraz autoryzowanych tooperform żadnych operacji dla tego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="d0da1-177">Nikt inny nie jest do tego upoważniony.</span><span class="sxs-lookup"><span data-stu-id="d0da1-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="d0da1-178">Dodawanie klucza lub magazynu kluczy tajnych toohello</span><span class="sxs-lookup"><span data-stu-id="d0da1-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="d0da1-179">Usługa Azure Key Vault toocreate klucza chronionego przez oprogramowanie dla Ciebie, należy użyć hello `azure key create` polecenia i wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="d0da1-180">Jednak jeśli masz istniejący klucz w pliku PEM, zapisany jako plik lokalny w pliku o nazwie softkey.pem, które mają tooAzure tooupload Key Vault, wpisz powitania po klucz hello tooimport z hello. Plik PEM, który chroni klucz hello przez oprogramowanie w usłudze Key Vault hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="d0da1-181">Teraz możesz odwoływać się hello klucz został utworzony lub przekazany tooAzure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="d0da1-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="d0da1-182">Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="d0da1-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="d0da1-183">tooadd magazynu toohello tajny, który jest hasłem o nazwie SQLPassword i ma hello wartość Pa$ $w0rd tooAzure Key Vault hello typu następujące:</span><span class="sxs-lookup"><span data-stu-id="d0da1-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="d0da1-184">Teraz możesz odwoływać się to hasło, dodać tooAzure Key Vault, za pomocą jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="d0da1-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="d0da1-185">Użyj **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tę konkretną wersję.</span><span class="sxs-lookup"><span data-stu-id="d0da1-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="d0da1-186">Teraz wyświetlić hello klucz lub klucz tajny, który został właśnie utworzony:</span><span class="sxs-lookup"><span data-stu-id="d0da1-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="d0da1-187">tooview Twojego klucza, wpisz:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="d0da1-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="d0da1-188">tooview tajne, typu:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="d0da1-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="d0da1-189">Rejestrowanie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0da1-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="d0da1-190">Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0da1-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="d0da1-191">Nie jest określonym tooAzure Key Vault, ale został tu zawarty, aby informacje były kompletne.</span><span class="sxs-lookup"><span data-stu-id="d0da1-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0da1-192">toocomplete hello samouczek, Twoje konto, Magazyn hello i aplikacji hello, która zarejestruje się w tym kroku musi być w hello tego samego katalogu Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="d0da1-193">Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0da1-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="d0da1-194">toodo hello, właściciel aplikacji hello aplikacji hello najpierw należy zarejestrować w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0da1-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="d0da1-195">Na powitania koniec rejestracji właściciel aplikacji hello pobiera hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="d0da1-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="d0da1-196">**Identyfikator aplikacji** (znanej także jako identyfikator klienta) i **klucz uwierzytelniania** (znanej także jako hello wspólny klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="d0da1-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="d0da1-197">Witaj, aplikacja musi przedstawić obie te wartości tooAzure usługi Active Directory, tooget tokenu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="d0da1-198">Jak aplikacja hello jest skonfigurowany toodo, który zależy od aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="d0da1-199">Dla usługi Key Vault Przykładowa aplikacja hello hello właściciel aplikacji ustawia te wartości w pliku app.config hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="d0da1-200">Aplikacja hello tooregister w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d0da1-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="d0da1-201">Zaloguj się toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d0da1-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="d0da1-202">Powitania po lewej stronie, kliknij przycisk **usługi Active Directory**, a następnie wybierz katalog hello, w którym będzie rejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="d0da1-203">Musisz wybrać hello tym samym katalogu, który zawiera hello subskrypcji platformy Azure, z którym zostanie utworzony magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="d0da1-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="d0da1-204">Jeśli nie znasz katalog ten jest, kliknij przycisk **ustawienia**zidentyfikować hello subskrypcji, z którym zostanie utworzony magazyn kluczy i w ostatniej kolumnie hello wyświetlana nazwa hello Uwaga hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="d0da1-205">Kliknij pozycję **APLIKACJE**.</span><span class="sxs-lookup"><span data-stu-id="d0da1-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="d0da1-206">Brak aplikacja nie została dodana tooyour katalogu, ta strona wyświetli tylko hello **Dodaj aplikację** łącza.</span><span class="sxs-lookup"><span data-stu-id="d0da1-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="d0da1-207">Kliknij łącze hello, lub też kliknąć hello **dodać** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="d0da1-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="d0da1-208">W hello **Dodawanie aplikacji** kreatora, na powitania **co chcesz toodo?** kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="d0da1-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="d0da1-209">Na powitania **Powiedz nam o aplikacji** , określ nazwę aplikacji i wybrać opcję **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (hello domyślną).</span><span class="sxs-lookup"><span data-stu-id="d0da1-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="d0da1-210">Kliknij ikonę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="d0da1-211">Na powitania **właściwości aplikacji** Określ hello **adres URL logowania** i **identyfikator URI aplikacji** dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d0da1-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="d0da1-212">Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach).</span><span class="sxs-lookup"><span data-stu-id="d0da1-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="d0da1-213">Nie ma znaczenia, czy taka strona istnieje; ważne jest, aplikacja hello identyfikator URI dla każdej aplikacji jest różne dla każdej aplikacji w katalogu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="d0da1-214">katalog Hello używa tego ciągu tooidentify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0da1-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="d0da1-215">Kliknij przycisk toosave pełną ikona hello zmiany w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="d0da1-216">Na stronie Szybki Start powitania kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="d0da1-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="d0da1-217">Przewiń toohello **klucze** sekcji, wybierz czas trwania hello, a następnie kliknij przycisk **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="d0da1-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="d0da1-218">Strona Hello odświeżona i pojawi się wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="d0da1-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="d0da1-219">Należy skonfigurować aplikację za pomocą wartości klucza i hello **identyfikator klienta** wartość.</span><span class="sxs-lookup"><span data-stu-id="d0da1-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="d0da1-220">(Instrukcje dotyczące tej konfiguracji będą specyficzne dla aplikacji).</span><span class="sxs-lookup"><span data-stu-id="d0da1-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="d0da1-221">Skopiuj wartość Identyfikatora powitania klienta z tej strony, który będzie używany w hello następny krok tooset uprawnień dotyczących magazynu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="d0da1-222">Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="d0da1-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="d0da1-223">Witaj tooaccess aplikacji hello tooauthorize klucza lub klucza tajnego w magazynie hello, użyj hello `azure keyvault set-policy` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d0da1-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="d0da1-224">Na przykład jeśli nazwa Twojego magazynu to ContosoKeyVault i hello aplikacji ma tooauthorize ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i toodecrypt aplikacji hello tooauthorize i zaloguj się za pomocą kluczy w magazynie, a następnie uruchom hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d0da1-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="d0da1-225">Uruchamiasz w wierszu polecenia systemu Windows, należy zastąpić pojedynczych cudzysłowów podwójnych cudzysłowów i również escape hello wewnętrzny podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="d0da1-226">Na przykład: "[\"odszyfrować\",\"znak\"]".</span><span class="sxs-lookup"><span data-stu-id="d0da1-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="d0da1-227">Jeśli chcesz tooauthorize tego samego hasła tooread aplikacji w magazynie, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="d0da1-228">Jeśli chcesz, aby toouse sprzętowego modułu zabezpieczeń (HSM)</span><span class="sxs-lookup"><span data-stu-id="d0da1-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="d0da1-229">Dla dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello.</span><span class="sxs-lookup"><span data-stu-id="d0da1-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="d0da1-230">Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany.</span><span class="sxs-lookup"><span data-stu-id="d0da1-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="d0da1-231">Jeśli te wymagania nie odnoszą się tooyou, Pomiń tę sekcję i przejdź zbyt[usunąć hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="d0da1-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="d0da1-232">toocreate klucze chronionego przez moduł HSM musi mieć subskrypcję magazynu obsługującą klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="d0da1-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="d0da1-233">Podczas tworzenia hello keyvault, Dodaj parametr "sku" hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="d0da1-234">Można dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) i magazynu toothis klucze chronione przez moduł HSM.</span><span class="sxs-lookup"><span data-stu-id="d0da1-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="d0da1-235">toocreate klucza chronionego przez moduł HSM, zestaw hello przeznaczenia parametru too'HSM ":</span><span class="sxs-lookup"><span data-stu-id="d0da1-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="d0da1-236">Możesz użyć hello następujące polecenia tooimport klucz z pliku PEM na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0da1-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="d0da1-237">To polecenie importuje klucz hello do sprzętowych modułów zabezpieczeń w usłudze Key Vault hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="d0da1-238">Witaj następne polecenie importuje "bring your own key" (BYOK) pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0da1-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="d0da1-239">Umożliwia generowanie klucza w lokalnym module HSM i przeniesienie go tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="d0da1-240">Aby uzyskać szczegółowe instrukcje dotyczące toogenerate pakietu BYOK, zobacz [jak toouse HSM-Protected klucze w usłudze Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="d0da1-241">Usuń hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="d0da1-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="d0da1-242">Jeśli nie są już potrzebne hello magazynu kluczy oraz klucz hello lub klucz tajny, który zawiera można usunąć magazynu kluczy hello za pomocą polecenia delete keyvault hello azure:</span><span class="sxs-lookup"><span data-stu-id="d0da1-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="d0da1-243">Lub usunięciem całej grupy zasobów platformy Azure, w tym magazynie kluczy hello i inne zasoby, które zostały dodane do tej grupy:</span><span class="sxs-lookup"><span data-stu-id="d0da1-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="d0da1-244">Inne polecenia interfejsu wiersza polecenia platformy Azure i Platform</span><span class="sxs-lookup"><span data-stu-id="d0da1-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="d0da1-245">Inne polecenia użytkownik może przydatne do zarządzania usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d0da1-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="d0da1-246">To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="d0da1-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="d0da1-247">To polecenie wyświetla pełną listę właściwości dla określonego klucza hello:</span><span class="sxs-lookup"><span data-stu-id="d0da1-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="d0da1-248">To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości:</span><span class="sxs-lookup"><span data-stu-id="d0da1-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="d0da1-249">Poniżej przedstawiono przykładowy sposób tooremove określonego klucza:</span><span class="sxs-lookup"><span data-stu-id="d0da1-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="d0da1-250">Poniżej przedstawiono przykładowy sposób tooremove określonego klucza tajnego:</span><span class="sxs-lookup"><span data-stu-id="d0da1-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="d0da1-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0da1-251">Next steps</span></span>
<span data-ttu-id="d0da1-252">Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d0da1-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

