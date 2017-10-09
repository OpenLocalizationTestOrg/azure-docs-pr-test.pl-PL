---
title: "Certyfikaty aaaManage klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooadd nowych certyfikatów, certyfikat przerzucania i usuwanie certyfikatów tooor z klastra usługi sieć szkieletowa usług."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="e15fb-103">Dodaj lub Usuń certyfikaty dla klastra usługi sieć szkieletowa na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e15fb-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="e15fb-104">Zalecane jest, zapoznaj się z używaniu certyfikatów X.509 w sieci szkieletowej usług, a następnie należy zapoznać się z hello [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="e15fb-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="e15fb-105">Trzeba zrozumieć, jakie certyfikat klastra jest i do czego służy, przed przejściem dalej.</span><span class="sxs-lookup"><span data-stu-id="e15fb-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="e15fb-106">Usługa sieci szkieletowej pozwala określić dwa klastra certyfikatów, podstawowego i pomocniczego, podczas konfigurowania certyfikatu zabezpieczeń podczas tworzenia klastra, dodanie tooclient certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e15fb-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="e15fb-107">Odwołuje się zbyt[tworzenia klastra platformy azure za pośrednictwem portalu](service-fabric-cluster-creation-via-portal.md) lub [tworzenia klastra platformy azure za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) dla informacji o konfiguracji na czas utworzenia.</span><span class="sxs-lookup"><span data-stu-id="e15fb-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="e15fb-108">Jeśli określisz tylko jeden certyfikat klastra na czas utworzenia, następnie używany jako podstawowy certyfikat hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="e15fb-109">Po utworzeniu klastra można dodać nowego certyfikatu jako dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="e15fb-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="e15fb-110">Bezpieczne klastra należy zawsze certyfikatu co najmniej jeden prawidłowy (nie odwołane i niewygasły) klastra (podstawowe lub pomocnicze) wdrożony (Jeśli nie, hello klaster przestanie działać).</span><span class="sxs-lookup"><span data-stu-id="e15fb-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="e15fb-111">90 dni, zanim wszystkie prawidłowe certyfikaty osiągną wygaśnięcia, generuje hello systemu śledzenia ostrzeżenie, a także zdarzenie kondycji ostrzeżenia w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="e15fb-112">Jest obecnie Brak poczty e-mail ani innych powiadomień, które wysyła sieci szkieletowej usług w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="e15fb-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="e15fb-113">Dodawanie certyfikatu dodatkowej klastra przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="e15fb-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="e15fb-114">Nie można dodać certyfikatu dodatkowej klastra za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e15fb-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="e15fb-115">Masz toouse Azure powershell do tego.</span><span class="sxs-lookup"><span data-stu-id="e15fb-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="e15fb-116">proces Hello jest opisane w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="e15fb-117">Wymiana certyfikatów klastra hello przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="e15fb-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="e15fb-118">Po pomyślnie wdrożeniu certyfikatu klastra pomocniczego, jeśli chcesz tooswap hello podstawowych i pomocniczych, następnie przejdź toohello blok zabezpieczeń i wybierz opcję "Zamiany z podstawowej" hello z hello kontekstu menu tooswap hello dodatkowej certyfikatu z Witaj podstawowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Wymiany certyfikatów][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="e15fb-120">Usuń certyfikat klastra za pomocą portalu hello</span><span class="sxs-lookup"><span data-stu-id="e15fb-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="e15fb-121">Bezpieczne klastra należy zawsze co najmniej jeden prawidłowy (nie odwołane i niewygasły) certyfikat (podstawowe lub pomocnicze) wdrożone w przeciwnym razie hello klaster przestanie działać.</span><span class="sxs-lookup"><span data-stu-id="e15fb-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="e15fb-122">tooremove dodatkowego certyfikatu z użycia zabezpieczeń klastra, Nawiguj toohello zabezpieczeń bloku i wybierz hello "Delete" opcji z menu kontekstowego hello na powitania dodatkowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="e15fb-123">Jeśli tooremove hello certyfikatu, który jest oznaczony jako podstawowy, a następnie konieczne będzie tooswap zamierzeniu go przy użyciu hello dodatkowej najpierw, a następnie usuń hello dodatkowej po ukończeniu uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="e15fb-124">Dodania dodatkowego certyfikatu przy użyciu programu Powershell Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="e15fb-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="e15fb-125">Tych krokach przyjęto założenie, zapoznali się z działania Menedżera zasobów i zostaną wdrożone co najmniej jeden klaster sieci szkieletowej usług za pomocą szablonu usługi Resource Manager i szablon hello użytą tooset zapasowej klastra hello pod ręką.</span><span class="sxs-lookup"><span data-stu-id="e15fb-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="e15fb-126">Zakłada się również, że masz doświadczenia, za pomocą formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="e15fb-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="e15fb-127">Jeśli szukasz przykładowy szablon i parametrów, których można używać toofollow wzdłuż lub jako punkt początkowy, następnie pobierz go z tego [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="e15fb-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="e15fb-128">Edytuj szablon Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="e15fb-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="e15fb-129">W celu ułatwienia następujące wzdłuż próbki 5-VM-1-elementów NodeType-Secure_Step2.JSON zawiera wszystkie zmiany hello wprowadzamy.</span><span class="sxs-lookup"><span data-stu-id="e15fb-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="e15fb-130">przykład Witaj jest dostępny w [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="e15fb-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="e15fb-131">**Upewnij się, że toofollow wszystkie kroki hello**</span><span class="sxs-lookup"><span data-stu-id="e15fb-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="e15fb-132">**Krok 1:** Otwórz szablon usługi Resource Manager hello używane toodeploy należy umieścić w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e15fb-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="e15fb-133">(Jeśli przykładowe hello zostały pobrane z hello powyżej repozytorium, następnie użyć toodeploy 5-VM-1-elementów NodeType-Secure_Step1.JSON bezpiecznego klastra i następnie otwarcia tego szablonu).</span><span class="sxs-lookup"><span data-stu-id="e15fb-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="e15fb-134">**Krok 2:** Dodaj **dwa nowe parametry** "secCertificateThumbprint" i "secCertificateUrlValue" typu "string" toohello parametru części szablonu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="e15fb-135">Można skopiować hello następującego fragmentu kodu i dodaj go toohello szablonu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="e15fb-136">W zależności od źródła hello szablonu może już tych zdefiniowana, jeśli tak przenosić toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="e15fb-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="e15fb-137">**Krok 3:** wprowadzanie zmian toohello **Microsoft.ServiceFabric/clusters** zasobu, zlokalizować definicji zasobu "Microsoft.ServiceFabric/clusters" hello w szablonie.</span><span class="sxs-lookup"><span data-stu-id="e15fb-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="e15fb-138">We właściwościach tej definicji, można znaleźć "Certyfikatu" JSON tagu, który powinien wyglądać jak powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="e15fb-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="e15fb-139">Dodaj nowy znacznik "thumbprintSecondary" i nadaj mu wartość "[parameters('secCertificateThumbprint')]".</span><span class="sxs-lookup"><span data-stu-id="e15fb-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="e15fb-140">Tak, teraz hello definicji zasobu powinna wyglądać hello następujące (w zależności od źródła hello szablonu, może nie być dokładnie takie same jak poniższy fragment hello).</span><span class="sxs-lookup"><span data-stu-id="e15fb-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="e15fb-141">Jeśli chcesz zbyt**przerzucania hello cert**, następnie określ hello nowego certyfikatu jako podstawowego i przenoszenie hello podstawowy bieżącego pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="e15fb-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="e15fb-142">Powoduje to hello przerzucania bieżącego podstawowego certyfikatu toohello nowy certyfikat w jednym kroku wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e15fb-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="e15fb-143">**Krok 4:** wprowadzanie zmian zbyt**wszystkie** hello **Microsoft.Compute/virtualMachineScaleSets** definicji zasobów — zlokalizuj hello Microsoft.Compute/virtualMachineScaleSets zasobów Definicja.</span><span class="sxs-lookup"><span data-stu-id="e15fb-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="e15fb-144">Przewiń toohello "publisher": "Microsoft.Azure.ServiceFabric", w obszarze "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="e15fb-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="e15fb-145">W ustawieniach hello usługi sieć szkieletowa wydawcy powinna zostać wyświetlona podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="e15fb-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="e15fb-147">Dodaj hello nowego certyfikatu wpisów tooit</span><span class="sxs-lookup"><span data-stu-id="e15fb-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="e15fb-148">właściwości Hello powinna wyglądać tak jak to</span><span class="sxs-lookup"><span data-stu-id="e15fb-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="e15fb-150">Jeśli chcesz zbyt**przerzucania hello cert**, następnie określ hello nowego certyfikatu jako podstawowego i przenoszenie hello podstawowy bieżącego pomocniczym.</span><span class="sxs-lookup"><span data-stu-id="e15fb-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="e15fb-151">Powoduje to hello przerzucania bieżącego certyfikatu toohello nowy certyfikat w jednym kroku wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e15fb-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="e15fb-152">właściwości Hello powinna wyglądać tak jak to</span><span class="sxs-lookup"><span data-stu-id="e15fb-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="e15fb-154">**Krok 5:** zmiany zbyt**wszystkie** hello **Microsoft.Compute/virtualMachineScaleSets** definicji zasobów — Znajdź hello Microsoft.Compute/virtualMachineScaleSets zasobów Definicja.</span><span class="sxs-lookup"><span data-stu-id="e15fb-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="e15fb-155">Przewiń toohello "vaultCertificates":, w obszarze "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="e15fb-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="e15fb-156">powinien on wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="e15fb-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="e15fb-158">Dodaj hello secCertificateUrlValue tooit.</span><span class="sxs-lookup"><span data-stu-id="e15fb-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="e15fb-159">Użyj następującego fragmentu hello:</span><span class="sxs-lookup"><span data-stu-id="e15fb-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="e15fb-160">Teraz hello wynikowa Json powinien wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="e15fb-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="e15fb-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="e15fb-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="e15fb-162">Upewnij się, że zostało wpisane kroki 4 i 5, dla wszystkich definicji zasobu Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="e15fb-163">Jeśli pominiesz jeden z nich hello certyfikatu nie zostaną zainstalowane na tym VMSS i może spowodować nieprzewidywalne skutki w klastrze, w tym klastrze hello przechodzi w dół (Jeśli na końcu nie prawidłowe certyfikaty, można użyć w tym klastrze hello zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e15fb-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="e15fb-164">Dlatego Sprawdź, przed kontynuacją.</span><span class="sxs-lookup"><span data-stu-id="e15fb-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="e15fb-165">Edytuj szablon pliku tooreflect hello nowe parametry dodanych powyżej</span><span class="sxs-lookup"><span data-stu-id="e15fb-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="e15fb-166">Jeśli używasz hello próbki z hello [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow wraz, można uruchomić zmiany toomake w hello próbki 5-VM — 1-elementów NodeType — Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="e15fb-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="e15fb-167">Edytowanie parametru szablonu usługi Resource Manager pliku, dodaj dwa nowe parametry hello secCertificateThumbprint i secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="e15fb-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="e15fb-168">Wdrażanie hello tooAzure szablonu</span><span class="sxs-lookup"><span data-stu-id="e15fb-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="e15fb-169">Użytkownik jest teraz gotowy toodeploy tooAzure Twojego szablonu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="e15fb-170">Otwórz wiersz polecenia w wersji 1 + Azure PS.</span><span class="sxs-lookup"><span data-stu-id="e15fb-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="e15fb-171">Zaloguj się za tooyour konto platformy Azure i wybierz hello określonej subskrypcji platformy azure.</span><span class="sxs-lookup"><span data-stu-id="e15fb-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="e15fb-172">Jest to ważny krok do pracowników, mających toomore dostępu niż jedną subskrypcją platformy azure.</span><span class="sxs-lookup"><span data-stu-id="e15fb-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="e15fb-173">Test toodeploying poprzedniego szablonu hello go.</span><span class="sxs-lookup"><span data-stu-id="e15fb-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="e15fb-174">Użyj hello klastra jest obecnie wdrożona do tej samej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e15fb-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="e15fb-175">Wdrażanie grupy zasobów tooyour szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="e15fb-176">Użyj hello klastra jest obecnie wdrożona do tej samej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e15fb-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="e15fb-177">Uruchom polecenie New-AzureRmResourceGroupDeployment hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="e15fb-178">Nie trzeba toospecify hello trybu, ponieważ hello wartość domyślna to **przyrostowe**.</span><span class="sxs-lookup"><span data-stu-id="e15fb-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="e15fb-179">Po ustawieniu trybu tooComplete przypadkowo można usunąć zasoby, które nie znajdują się w szablonie.</span><span class="sxs-lookup"><span data-stu-id="e15fb-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="e15fb-180">Dlatego nie jest używana w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="e15fb-181">W tym miejscu jest wypełniony się przykładem hello tego samego środowiska powershell.</span><span class="sxs-lookup"><span data-stu-id="e15fb-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="e15fb-182">Po zakończeniu wdrażania hello połączyć tooyour klastra przy użyciu hello nowego certyfikatu i wykonywania niektórych zapytań.</span><span class="sxs-lookup"><span data-stu-id="e15fb-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="e15fb-183">Jeśli jesteś toodo stanie.</span><span class="sxs-lookup"><span data-stu-id="e15fb-183">If you are able toodo.</span></span> <span data-ttu-id="e15fb-184">Następnie można usunąć starego certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="e15fb-185">Jeśli używasz certyfikatu z podpisem własnym, nie zapomnij tooimport ich do lokalnego magazynu certyfikatów TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="e15fb-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="e15fb-186">Dla wygody Oto hello polecenia tooconnect tooa bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="e15fb-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="e15fb-187">Dla wygody Oto hello polecenia tooget klastra kondycji</span><span class="sxs-lookup"><span data-stu-id="e15fb-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="e15fb-188">Wdrażanie klastra toohello certyfikaty aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e15fb-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="e15fb-189">Możesz użyć hello same kroki zgodnie z opisem w kroki 5 powyżej certyfikatów hello toohave wdrożone z toohello keyvault węzłów.</span><span class="sxs-lookup"><span data-stu-id="e15fb-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="e15fb-190">Możesz po prostu należy zdefiniować i użyć innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e15fb-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="e15fb-191">Dodanie lub usunięcie certyfikatów klienta</span><span class="sxs-lookup"><span data-stu-id="e15fb-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="e15fb-192">W dodatku toohello klastra certyfikatów można dodać operacji zarządzania tooperform certyfikaty klienta w klastrze usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="e15fb-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="e15fb-193">Możesz dodać dwa rodzaje certyfikatów klienta — administratora lub w trybie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="e15fb-194">Następnie mogą być używane toocontrol dostępu toohello administratora operacji i operacje kwerend w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="e15fb-195">Domyślnie certyfikaty klastra hello są dodawane toohello Admin certyfikaty listy dozwolonych.</span><span class="sxs-lookup"><span data-stu-id="e15fb-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="e15fb-196">można określić dowolną liczbę certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="e15fb-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="e15fb-197">Każdy dodanie/usunięcie powoduje klastra sieci szkieletowej usług toohello aktualizacji konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e15fb-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="e15fb-198">Dodawanie certyfikatów klienta — administratora lub w trybie tylko do odczytu za pomocą portalu</span><span class="sxs-lookup"><span data-stu-id="e15fb-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="e15fb-199">Przejdź do bloku zabezpieczeń toohello, a następnie wybierz hello "+ uwierzytelniania" przycisk u góry bloku zabezpieczeń hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="e15fb-200">W bloku "Dodaj uwierzytelniania" hello wybierz hello "Typ uwierzytelniania" - "Tylko do odczytu" lub "Admin klienta"</span><span class="sxs-lookup"><span data-stu-id="e15fb-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="e15fb-201">Teraz wybierz metodę autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="e15fb-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="e15fb-202">Czy powinna wyszukiwać ten certyfikat za pomocą hello nazwa podmiotu lub odcisku palca hello wskazuje tooService sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="e15fb-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="e15fb-203">Ogólnie rzecz biorąc go nie jest dobrym rozwiązaniem toouse hello autoryzacji metodą nazwy podmiotu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Dodawanie certyfikatu klienta][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="e15fb-205">Usunięcie certyfikatów klienta — administratora lub tylko do odczytu za pomocą hello portalu</span><span class="sxs-lookup"><span data-stu-id="e15fb-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="e15fb-206">tooremove dodatkowego certyfikatu z użycia zabezpieczeń klastra, Nawiguj toohello zabezpieczeń bloku i wybierz hello "Delete" opcji z menu kontekstowego hello na powitania określonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e15fb-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e15fb-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e15fb-207">Next steps</span></span>
<span data-ttu-id="e15fb-208">Przeczytaj następujące artykuły, aby uzyskać więcej informacji na temat zarządzania klastrem:</span><span class="sxs-lookup"><span data-stu-id="e15fb-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="e15fb-209">Proces uaktualniania klastra sieci szkieletowej usług oraz oczekiwań od użytkownika</span><span class="sxs-lookup"><span data-stu-id="e15fb-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="e15fb-210">Ustawienia dostępu opartego na rolach dla klientów</span><span class="sxs-lookup"><span data-stu-id="e15fb-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


