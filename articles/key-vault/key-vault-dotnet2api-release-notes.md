---
title: Informacje o wersji interfejsu API 2.x .NET magazynu aaaKey | Dokumentacja firmy Microsoft
description: ".NET umożliwia deweloperom toocode tego interfejsu API dla usługi Azure Key Vault"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="934c0-103">Usługi Azure Key Vault .NET 2.0 — przewodnik migracji i informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="934c0-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="934c0-104">Witaj następujące wskazówki i informacje są dla deweloperów korzystających z platformy .NET magazynu kluczy Azure / biblioteki C#.</span><span class="sxs-lookup"><span data-stu-id="934c0-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="934c0-105">W hello przejście od wersji hello 1.0 w wersji toohello 2.0, liczba aktualizacji wprowadzono tego będzie wymagać pracy migracji w kodzie aby toobenefit z ulepszeń funkcjonalności hello i funkcji dodatków, takich jak **magazyn kluczy Certyfikaty** obsługuje.</span><span class="sxs-lookup"><span data-stu-id="934c0-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="934c0-106">Magazyn kluczy certyfikatów</span><span class="sxs-lookup"><span data-stu-id="934c0-106">Key Vault certificates</span></span>

<span data-ttu-id="934c0-107">Obsługa certyfikatów usługi Key Vault umożliwia zarządzanie x509 Twojego certyfikaty i hello następujące zachowania:</span><span class="sxs-lookup"><span data-stu-id="934c0-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="934c0-108">Umożliwia toocreate właściciela certyfikatu certyfikatu za pośrednictwem procesu tworzenia usługi Key Vault lub hello importowania istniejącego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="934c0-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="934c0-109">Dotyczy to zarówno z podpisem własnym, a urząd certyfikacji generowane certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="934c0-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="934c0-110">Umożliwia właściciela certyfikatu usługi Key Vault tooimplement bezpieczne przechowywanie i zarządzania X509 certyfikatów bez interakcji z materiału klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="934c0-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="934c0-111">Umożliwia toocreate właściciela certyfikatu zasadę, która określa, że magazyn kluczy toomanage hello cyklu życia certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="934c0-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="934c0-112">Umożliwia właścicieli certyfikatu tooprovide informacje kontaktowe dla powiadomień dotyczących zdarzeń cyklu życia wygaśnięcia i odnawiania certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="934c0-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="934c0-113">Obsługuje automatycznego odnawiania z wystawców wybranych - Key Vault partnera X509 certyfikatu dostawców / urzędy certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="934c0-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="934c0-114">Uwaga —-współpracę dostawców/urzędów również są dozwolone, ale nie będzie obsługiwał hello automatycznego odnawiania funkcji.</span><span class="sxs-lookup"><span data-stu-id="934c0-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="934c0-115">Obsługa .NET</span><span class="sxs-lookup"><span data-stu-id="934c0-115">.NET support</span></span>

* <span data-ttu-id="934c0-116">**.NET 4.0** nie jest obsługiwana przez wersję hello 2.0 hello .NET usługi Azure Key Vault / biblioteki C#</span><span class="sxs-lookup"><span data-stu-id="934c0-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="934c0-117">**Oprogramowanie .NET core** jest obsługiwana przez wersję hello 2.0 hello .NET usługi Azure Key Vault / biblioteki C#</span><span class="sxs-lookup"><span data-stu-id="934c0-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="934c0-118">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="934c0-118">Namespaces</span></span>

* <span data-ttu-id="934c0-119">Witaj w obszarze nazw **modele** została zmieniona z **Microsoft.Azure.KeyVault** za**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="934c0-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="934c0-120">Witaj **Microsoft.Azure.KeyVault.Internal** przestrzeni nazw jest porzucany.</span><span class="sxs-lookup"><span data-stu-id="934c0-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="934c0-121">przestrzeń nazw zależności zestawu Azure SDK Hello zmieniła się z **Hyak.Common** i **Hyak.Common.Internals** za**Microsoft.Rest** i  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="934c0-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="934c0-122">Zmiana typu</span><span class="sxs-lookup"><span data-stu-id="934c0-122">Type changes</span></span>

* <span data-ttu-id="934c0-123">*Klucz tajny* zmieniony zbyt*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="934c0-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="934c0-124">*Słownik* zmieniony zbyt*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="934c0-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="934c0-125">*Lista<T>, string []* zmieniony zbyt*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="934c0-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="934c0-126">*NextList* zmieniony zbyt *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="934c0-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="934c0-127">Zwracane typy</span><span class="sxs-lookup"><span data-stu-id="934c0-127">Return types</span></span>

* <span data-ttu-id="934c0-128">**KeyList** i **SecretList** zwróci *IPage<T>*  zamiast *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="934c0-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="934c0-129">wygenerowany Hello **BackupKeyAsync** zwróci *BackupKeyResult* zawierającą *wartość* (kopie zapasowe obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="934c0-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="934c0-130">Przed hello metoda została opakowana i zwracanie tylko wartości hello.</span><span class="sxs-lookup"><span data-stu-id="934c0-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="934c0-131">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="934c0-131">Exceptions</span></span>

* <span data-ttu-id="934c0-132">*KeyVaultClientException* zostanie zmieniona zbyt*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="934c0-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="934c0-133">Błąd usługi Hello została zmieniona z *wyjątku. Błąd* zbyt*wyjątku. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="934c0-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="934c0-134">Usunięte informacje dodatkowe z hello komunikat o błędzie dla **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="934c0-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="934c0-135">Konstruktory</span><span class="sxs-lookup"><span data-stu-id="934c0-135">Constructors</span></span>

* <span data-ttu-id="934c0-136">Zamiast akceptowanie *HttpClient* jako argument konstruktora akceptuje tylko Konstruktor hello *HttpClientHandler* lub *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="934c0-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="934c0-137">Pobranych pakietów</span><span class="sxs-lookup"><span data-stu-id="934c0-137">Downloaded packages</span></span>

<span data-ttu-id="934c0-138">Gdy klient przetwarza zależności na następujących hello Key Vault zostały pobrane</span><span class="sxs-lookup"><span data-stu-id="934c0-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="934c0-139">Poprzedniej liście pakietu</span><span class="sxs-lookup"><span data-stu-id="934c0-139">Previous package list</span></span>

* <span data-ttu-id="934c0-140">Wersja pakietu id="Hyak.Common" = "1.0.2" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-141">Wersja pakietu id="Microsoft.Azure.Common" = "2.0.4" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-142">Wersja pakietu id="Microsoft.Azure.Common.Dependencies" = "1.0.0" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-143">Wersja pakietu id="Microsoft.Azure.KeyVault" = "1.0.0" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-144">Wersja pakietu id="Microsoft.Bcl" = "1.1.9" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-145">Wersja pakietu id="Microsoft.Bcl.Async" = "1.0.168" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-146">Wersja pakietu id="Microsoft.Bcl.Build" = "1.0.14" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-147">Wersja pakietu id="Microsoft.Net.Http" = "2.2.22" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="934c0-148">Bieżąca lista pakietów</span><span class="sxs-lookup"><span data-stu-id="934c0-148">Current package list</span></span>

* <span data-ttu-id="934c0-149">Wersja pakietu id="Microsoft.Azure.KeyVault" = "2.0.0-preview" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-150">Wersja pakietu id="Microsoft.Rest.ClientRuntime" = "2.2.0" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="934c0-151">Wersja pakietu id="Microsoft.Rest.ClientRuntime.Azure" = "3.2.0" targetFramework = "net45"</span><span class="sxs-lookup"><span data-stu-id="934c0-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="934c0-152">Klasa zmiany</span><span class="sxs-lookup"><span data-stu-id="934c0-152">Class changes</span></span>

* <span data-ttu-id="934c0-153">**UnixEpoch** klasy został usunięty.</span><span class="sxs-lookup"><span data-stu-id="934c0-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="934c0-154">**Base64UrlConverter** klasy jest zmieniana zbyt**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="934c0-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="934c0-155">Inne zmiany</span><span class="sxs-lookup"><span data-stu-id="934c0-155">Other changes</span></span>

* <span data-ttu-id="934c0-156">Dodano obsługę dla konfiguracji hello KV zasady ponawiania operacji na błędów przejściowych toothis wersji hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="934c0-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="934c0-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="934c0-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="934c0-158">Dla operacji hello, które zwrócił *magazynu*, typ zwracany hello został klasę, która zawiera właściwość magazynu.</span><span class="sxs-lookup"><span data-stu-id="934c0-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="934c0-159">Witaj zwracany typ jest teraz *magazynu*.</span><span class="sxs-lookup"><span data-stu-id="934c0-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="934c0-160">*PermissionsToKeys* i *PermissionsToSecrets* są teraz *Permissions.Keys* i *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="934c0-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="934c0-161">Niektóre hello zwracać typów zmiany dotyczą toohello kontroli — płaszczyzna również.</span><span class="sxs-lookup"><span data-stu-id="934c0-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="934c0-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="934c0-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="934c0-163">pakietów Hello jest zbyt podzielony**Microsoft.Azure.KeyVault.Extensions** i **Microsoft.Azure.KeyVault.Cryptography** hello operacji kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="934c0-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

