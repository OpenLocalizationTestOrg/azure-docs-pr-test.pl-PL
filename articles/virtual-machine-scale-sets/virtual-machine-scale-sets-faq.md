---
title: "często zadawane pytania dotyczące zestawach skali maszyn wirtualnych aaaAzure | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące zestawy skalowania maszyny wirtualnej."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="191a9-103">Zestawach skali maszyny wirtualnej platformy Azure — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="191a9-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="191a9-104">Odpowiedzi ustawia toofrequently zadawane pytania dotyczące skalowania maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="191a9-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="191a9-105">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="191a9-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="191a9-106">Jakie są najlepsze rozwiązania dotyczące skalowania automatycznego Azure?</span><span class="sxs-lookup"><span data-stu-id="191a9-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="191a9-107">Aby uzyskać najlepsze rozwiązania dotyczące skalowania automatycznego, zobacz [najlepsze rozwiązania w przypadku maszyn wirtualnych, skalowanie automatyczne](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="191a9-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="191a9-108">Gdzie można znaleźć nazwy metryki Skalowanie automatyczne, który wykorzystuje metryki oparta na hoście</span><span class="sxs-lookup"><span data-stu-id="191a9-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="191a9-109">Metryki nazw dla Skalowanie automatyczne, który wykorzystuje metryki oparta na hoście, zobacz [obsługiwane metryki z monitorem Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="191a9-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="191a9-110">Czy istnieją przykładami Skalowanie automatyczne w oparciu o długości kolejek i tematów usługi Azure Service Bus?</span><span class="sxs-lookup"><span data-stu-id="191a9-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="191a9-111">Tak.</span><span class="sxs-lookup"><span data-stu-id="191a9-111">Yes.</span></span> <span data-ttu-id="191a9-112">Przykłady Skalowanie automatyczne w oparciu o długości kolejek i tematów usługi Azure Service Bus, zobacz [metryki wspólnej Skalowanie automatyczne Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="191a9-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="191a9-113">Dla kolejki usługi Service Bus Użyj następującego formatu JSON hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="191a9-114">Kolejki magazynu należy użyć powitania po JSON:</span><span class="sxs-lookup"><span data-stu-id="191a9-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="191a9-115">Zastąp wartości przykładowe zasobu Uniform Resource Identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="191a9-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="191a9-116">Czy należy skalowania automatycznego przy użyciu metryk oparta na hoście lub rozszerzenia diagnostyki?</span><span class="sxs-lookup"><span data-stu-id="191a9-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="191a9-117">Ustawienia skalowania automatycznego można tworzyć na metryki poziomu hosta toouse maszyny Wirtualnej lub metryki na podstawie systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="191a9-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="191a9-118">Aby uzyskać listę obsługiwanych metryki, zobacz [metryki wspólnej Skalowanie automatyczne Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="191a9-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="191a9-119">Aby uzyskać pełny przykład dla zestawy skalowania maszyny wirtualnej, zobacz [konfiguracji automatycznego skalowania zaawansowanych przy użyciu szablonów usługi Resource Manager dla zestawy skalowania maszyny wirtualnej](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="191a9-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="191a9-120">Witaj w przykładzie użyto hello poziomie hosta Procesora metryk i metrykę liczba wiadomości.</span><span class="sxs-lookup"><span data-stu-id="191a9-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="191a9-121">Jak ustawić reguły alertów na zestaw skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="191a9-122">Alerty można tworzyć na metryki dla zestawy skalowania maszyny wirtualnej za pomocą programu PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="191a9-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="191a9-123">Aby uzyskać więcej informacji, zobacz [Azure PowerShell Monitor szybki start przykłady](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) i [Azure Monitor i platform interfejsu wiersza polecenia Szybki start przykłady](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="191a9-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="191a9-124">Element TargetResourceId zestawu skali maszyny wirtualnej hello Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="191a9-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="191a9-125">/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/Providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="191a9-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="191a9-126">Można wybrać dowolnego licznika wydajności maszyny Wirtualnej jako tooset metryki hello alert dla.</span><span class="sxs-lookup"><span data-stu-id="191a9-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="191a9-127">Aby uzyskać więcej informacji, zobacz [metryki systemu operacyjnego gościa dla maszyn wirtualnych Menedżera zasobów systemu Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) i [metryki systemu operacyjnego gościa dla maszyn wirtualnych systemu Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) w hello [Azure Monitor Skalowanie automatyczne wspólnej metryki](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artykułu.</span><span class="sxs-lookup"><span data-stu-id="191a9-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="191a9-128">Jak skonfigurować automatycznego skalowania w skali maszyny wirtualnej ustawić przy użyciu programu PowerShell?</span><span class="sxs-lookup"><span data-stu-id="191a9-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="191a9-129">tooset się automatycznego skalowania w skali maszyny wirtualnej ustawić przy użyciu programu PowerShell, zobacz hello blogu [konfiguracji tooadd tooan skalowania automatycznego skalowania maszyny wirtualnej platformy Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="191a9-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="191a9-130">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="191a9-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="191a9-131">Jak bezpiecznie wysłać toohello certyfikatów maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="191a9-132">Jak udostępnić toorun zestaw skali maszyny wirtualnej witryny sieci Web, gdzie hello SSL dla witryny sieci Web hello jest dostarczany bezpiecznie z konfiguracji certyfikatu?</span><span class="sxs-lookup"><span data-stu-id="191a9-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="191a9-133">(hello typowych operacji obrotu certyfikatu może być prawie hello jak w przypadku operacji aktualizacji konfiguracji.) Czy masz przykładem toodo to?</span><span class="sxs-lookup"><span data-stu-id="191a9-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="191a9-134">toosecurely wysłać toohello certyfikatów maszyny Wirtualnej, należy zainstalować certyfikat klienta, bezpośrednio do magazynu certyfikatów systemu Windows z magazynu kluczy powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="191a9-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="191a9-135">Użyj następującego formatu JSON hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="191a9-136">Kod Hello obsługuje system Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="191a9-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="191a9-137">Aby uzyskać więcej informacji, zobacz [Tworzenie lub aktualizacja zestawu skalowania maszyn wirtualnych](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="191a9-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="191a9-138">Przykład certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="191a9-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="191a9-139">Tworzenie certyfikatu z podpisem własnym w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="191a9-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="191a9-140">Użyj następującego polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="191a9-141">To polecenie umożliwia hello dane wejściowe dla szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="191a9-142">Przykład toocreate certyfikatu z podpisem własnym w magazynie kluczy, zobacz temat [scenariusze zabezpieczeń klastra sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="191a9-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="191a9-143">Zmień hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="191a9-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="191a9-144">Dodaj tę właściwość za**virtualMachineProfile**, jako część hello zasobów zestawu skalowania maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="191a9-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="191a9-145">Czy mogę określić toouse pary kluczy SSH do uwierzytelniania SSH o skali maszyny wirtualnej systemu Linux ustawiony na podstawie szablonu usługi Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="191a9-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="191a9-146">Tak.</span><span class="sxs-lookup"><span data-stu-id="191a9-146">Yes.</span></span> <span data-ttu-id="191a9-147">Witaj interfejsu API REST dla **osProfile** jest podobne toohello standardowa maszyna wirtualna interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="191a9-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="191a9-148">Obejmują **osProfile** w szablonie:</span><span class="sxs-lookup"><span data-stu-id="191a9-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="191a9-149">Ten blok JSON jest używany w [hello 101-vm-sshkey GitHub szybki start szablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="191a9-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="191a9-150">Witaj profilu systemu operacyjnego jest również używana w [grelayhost.json hello GitHub szybki start szablonu](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="191a9-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="191a9-151">Aby uzyskać więcej informacji, zobacz [Tworzenie lub aktualizacja zestawu skalowania maszyn wirtualnych](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="191a9-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="191a9-152">Jak usunąć przestarzałe certyfikatów?</span><span class="sxs-lookup"><span data-stu-id="191a9-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="191a9-153">tooremove przestarzałe certyfikaty i Usuń hello starego certyfikatu z listy certyfikatów magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="191a9-154">Pozostaw wszystkie certyfikaty hello mają tooremain na komputerze, na liście hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="191a9-155">Nie powoduje usunięcia certyfikatu hello z wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="191a9-156">Ponadto nie dodaje hello certyfikatu toonew maszyn wirtualnych, które są tworzone w zestawie skalowania maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="191a9-157">tooremove hello certyfikatu z istniejących maszyn wirtualnych, zapis skryptu niestandardowego rozszerzenia toomanually Usuń hello certyfikaty z magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="191a9-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="191a9-158">Jak iniekcję istniejącego klucza publicznego SSH do warstwy zestawu skali hello maszyny wirtualnej w SSH podczas inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="191a9-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="191a9-159">Toostore hello SSH publicznego klucza wartości w usłudze Azure Key Vault, a następnie używać ich w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="191a9-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="191a9-160">Jeśli hello maszyny wirtualne są udostępniane tylko za pomocą klucza publicznego SSH, nie potrzebujesz tooput hello kluczy publicznych w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="191a9-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="191a9-161">Klucze publiczne nie są poufne.</span><span class="sxs-lookup"><span data-stu-id="191a9-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="191a9-162">Klucze publiczne SSH w postaci zwykłego tekstu można podać podczas tworzenia maszyny Wirtualnej systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="191a9-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="191a9-163">Nazwa elementu linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="191a9-163">linuxConfiguration element name</span></span> | <span data-ttu-id="191a9-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="191a9-164">Required</span></span> | <span data-ttu-id="191a9-165">Typ</span><span class="sxs-lookup"><span data-stu-id="191a9-165">Type</span></span> | <span data-ttu-id="191a9-166">Opis</span><span class="sxs-lookup"><span data-stu-id="191a9-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="191a9-167">SSH</span><span class="sxs-lookup"><span data-stu-id="191a9-167">ssh</span></span> | <span data-ttu-id="191a9-168">Nie</span><span class="sxs-lookup"><span data-stu-id="191a9-168">No</span></span> | <span data-ttu-id="191a9-169">Collection</span><span class="sxs-lookup"><span data-stu-id="191a9-169">Collection</span></span> | <span data-ttu-id="191a9-170">Określa hello konfiguracji kluczy SSH w systemie operacyjnym Linux</span><span class="sxs-lookup"><span data-stu-id="191a9-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="191a9-171">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="191a9-171">path</span></span> | <span data-ttu-id="191a9-172">Tak</span><span class="sxs-lookup"><span data-stu-id="191a9-172">Yes</span></span> | <span data-ttu-id="191a9-173">Ciąg</span><span class="sxs-lookup"><span data-stu-id="191a9-173">String</span></span> | <span data-ttu-id="191a9-174">Określa ścieżkę pliku Linux hello gdzie kluczy SSH hello lub certyfikat powinien być zlokalizowany</span><span class="sxs-lookup"><span data-stu-id="191a9-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="191a9-175">Kontenerem</span><span class="sxs-lookup"><span data-stu-id="191a9-175">keyData</span></span> | <span data-ttu-id="191a9-176">Tak</span><span class="sxs-lookup"><span data-stu-id="191a9-176">Yes</span></span> | <span data-ttu-id="191a9-177">Ciąg</span><span class="sxs-lookup"><span data-stu-id="191a9-177">String</span></span> | <span data-ttu-id="191a9-178">Określa klucz publiczny SSH algorytmem Base64</span><span class="sxs-lookup"><span data-stu-id="191a9-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="191a9-179">Na przykład zobacz [hello 101-vm-sshkey GitHub szybki start szablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="191a9-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="191a9-180">Po uruchomieniu `Update-AzureRmVmss` po dodaniu więcej niż jeden certyfikat z hello klucza magazynu, są widoczne hello następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="191a9-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="191a9-181">AzureRmVmss aktualizacji: Klucz tajny listy zawiera powtórzony wystąpienia /subscriptions/ < identyfikator Moje subskrypcji > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, który jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="191a9-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="191a9-182">Może się to zdarzyć, Jeśli spróbujesz toore — Dodaj hello sam magazynu zamiast używania nowego certyfikatu w magazynie dla hello istniejący źródłowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="191a9-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="191a9-183">Witaj `Add-AzureRmVmssSecret` polecenie nie działa poprawnie, w przypadku dodawania dodatkowych kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="191a9-184">tooadd więcej kluczy tajnych ze hello tego samego magazynu kluczy, lista $vmss.properties.osProfile.secrets[0].vaultCertificates hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="191a9-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="191a9-185">Aby hello oczekiwano strukturze wejściowej, zobacz [Tworzenie lub aktualizacja maszyny wirtualnej ustawić](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="191a9-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="191a9-186">Znajdź klucz tajny hello w obiekcie zestawu skali maszyny wirtualnej hello, który znajduje się w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="191a9-187">Następnie należy dodać skojarzony z magazynem hello listy toohello odwołania (adres URL hello i nazwa magazynu tajny hello) certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="191a9-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="191a9-188">Obecnie nie można usunąć certyfikaty z maszyn wirtualnych za pomocą API zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="191a9-189">Nowe maszyny wirtualne nie będą miały hello stary certyfikat.</span><span class="sxs-lookup"><span data-stu-id="191a9-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="191a9-190">Maszyny wirtualne w tym hello certyfikatów, które są już wdrożone będzie jednak hello stary certyfikat.</span><span class="sxs-lookup"><span data-stu-id="191a9-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="191a9-191">Czy można push skalowania maszyny wirtualnej toohello certyfikaty ustawić bez konieczności podawania hasła hello, gdy hello certyfikat znajduje się w magazynie tajny hello?</span><span class="sxs-lookup"><span data-stu-id="191a9-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="191a9-192">Nie trzeba toohard kod hasła w skryptach.</span><span class="sxs-lookup"><span data-stu-id="191a9-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="191a9-193">Dynamiczne mogą pobierać hasła z uprawnieniami hello użycie toorun hello wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="191a9-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="191a9-194">Jeśli masz skrypt, który przenosi certyfikat z magazynu kluczy tajnych magazynu hello hello tajny magazynu `get certificate` polecenie wyświetla również hello hasło pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="191a9-195">Jak właściwości kluczy tajnych hello virtualMachineProfile.osProfile skali maszyny wirtualnej ustawić pracy?</span><span class="sxs-lookup"><span data-stu-id="191a9-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="191a9-196">Dlaczego należy hello sourceVault wartość, gdy toospecify hello bezwzględnym identyfikatorem URI certyfikatu za pomocą właściwości certificateUrl hello?</span><span class="sxs-lookup"><span data-stu-id="191a9-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="191a9-197">Odwołanie certyfikatu Windows Remote Management (WinRM) musi być obecny w hello właściwości kluczy tajnych hello profilu systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="191a9-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="191a9-198">Celem Hello wskazujący hello źródłowy magazyn jest zasady listę kontroli dostępu (ACL) kontroli dostępu tooenforce, które istnieją w modelu usługi w chmurze Azure użytkownika.</span><span class="sxs-lookup"><span data-stu-id="191a9-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="191a9-199">Jeśli hello źródłowy magazyn nie zostanie określona, użytkowników, którzy nie mają uprawnień dostępu lub toodeploy kluczy tajnych tooa magazynu kluczy będą mogli toothrough obliczeniowe dostawcy zasobów (CRP).</span><span class="sxs-lookup"><span data-stu-id="191a9-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="191a9-200">Listy ACL istnieje nawet w przypadku zasobów, które nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="191a9-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="191a9-201">Jeśli podasz nieprawidłowe źródło identyfikator magazynu, ale adres URL magazynu kluczy prawidłowy podczas sondowania operacji hello jest zgłaszany błąd.</span><span class="sxs-lookup"><span data-stu-id="191a9-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="191a9-202">Jeśli dodać tooan kluczy tajnych istniejący zestaw skali maszyny wirtualnej, są klucze tajne hello dodane do istniejących maszyn wirtualnych, lub tylko na nowe?</span><span class="sxs-lookup"><span data-stu-id="191a9-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="191a9-203">Certyfikaty są dodawane tooall maszyn wirtualnych, nawet istniejący już przetworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="191a9-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="191a9-204">Jeśli właściwość upgradePolicy Twojego skalowania maszyny wirtualnej jest ustawiona zbyt**ręczne**, certyfikat hello jest dodawany toohello maszyny Wirtualnej, podczas przeprowadzania ręcznej aktualizacji hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="191a9-205">Gdzie umieścić certyfikaty dla maszyn wirtualnych systemu Linux?</span><span class="sxs-lookup"><span data-stu-id="191a9-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="191a9-206">toolearn toodeploy certyfikatów dla maszyn wirtualnych systemu Linux, zobacz temat [wdrażanie tooVMs certyfikaty z magazynu zarządzanego przez klienta klucza](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="191a9-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="191a9-207">Jak dodać nowy magazyn certyfikatów tooa nowego certyfikatu obiekt?</span><span class="sxs-lookup"><span data-stu-id="191a9-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="191a9-208">tooadd magazyn certyfikatów tooan istniejący klucz tajny, zobacz poniższy przykład PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="191a9-209">Użyj tylko jeden obiekt tajny.</span><span class="sxs-lookup"><span data-stu-id="191a9-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="191a9-210">Co się stanie toocertificates, jeśli można odtworzyć z obrazu maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="191a9-211">Czy można odtworzyć z obrazu maszyny Wirtualnej, certyfikaty zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="191a9-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="191a9-212">Ponownym hello usuwa cały dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="191a9-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="191a9-213">Co się stanie po usunięciu certyfikatu z magazynu kluczy hello?</span><span class="sxs-lookup"><span data-stu-id="191a9-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="191a9-214">Jeśli klucz tajny hello zostanie usunięty z magazynu kluczy hello, a następnie uruchom `stop deallocate` dla wszystkich maszyn wirtualnych, a następnie uruchom je ponownie, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="191a9-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="191a9-215">Witaj błąd występuje, ponieważ hello CRP wymaga kluczy tajnych hello tooretrieve z magazynu kluczy hello, ale nie jest.</span><span class="sxs-lookup"><span data-stu-id="191a9-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="191a9-216">W tym scenariuszu można usunąć certyfikatów hello z modelu zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="191a9-217">Witaj CRP składnika nie jest trwały kluczy tajnych klienta.</span><span class="sxs-lookup"><span data-stu-id="191a9-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="191a9-218">Po uruchomieniu `stop deallocate` dla wszystkich maszyn wirtualnych w zestawie skalowania maszyn wirtualnych hello, pamięć podręczna hello zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="191a9-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="191a9-219">W tym scenariuszu kluczy tajnych są pobierane z hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="191a9-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="191a9-220">Ten problem nie wystąpić w trakcie skalowania, ponieważ nie istnieje w pamięci podręcznej kopię klucza tajnego hello w sieci szkieletowej usług Azure (w modelu sieci szkieletowej pojedynczej dzierżawy hello).</span><span class="sxs-lookup"><span data-stu-id="191a9-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="191a9-221">Dlaczego ma toospecify hello dokładnej lokalizacji dla adresu URL certyfikatu hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), jak określono w [scenariusze zabezpieczeń klastra sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="191a9-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="191a9-222">Witaj dokumentacji usługi Azure Key Vault stany tego Pobierz klucz tajny interfejsu API REST powinien zwrócić hello najnowszą wersję hello klucz tajny, jeśli nie określono wersji hello powitalne.</span><span class="sxs-lookup"><span data-stu-id="191a9-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="191a9-223">Metoda</span><span class="sxs-lookup"><span data-stu-id="191a9-223">Method</span></span> | <span data-ttu-id="191a9-224">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="191a9-224">URL</span></span>
--- | ---
<span data-ttu-id="191a9-225">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="191a9-225">GET</span></span> | <span data-ttu-id="191a9-226">https://mykeyvault.Vault.Azure.NET/secrets/ {klucz tajny name} / {klucz tajny version}? api-version = {wersja interfejsu api}</span><span class="sxs-lookup"><span data-stu-id="191a9-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="191a9-227">Zastąp {*nazwa klucza tajnego*} o nazwie hello i Zastąp {*wersja klucza tajnego*} z wersją hello SECRET hello ma tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="191a9-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="191a9-228">wersję klucza tajnego Hello może zostać wyłączone.</span><span class="sxs-lookup"><span data-stu-id="191a9-228">hello secret version might be excluded.</span></span> <span data-ttu-id="191a9-229">W takim przypadku jest pobierana hello bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="191a9-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="191a9-230">Dlaczego ma toospecify hello certyfikatu wersji, podczas korzystania z usługi Key Vault?</span><span class="sxs-lookup"><span data-stu-id="191a9-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="191a9-231">Celem Hello hello Key Vault wymaganie toospecify hello certyfikatu wersji jest toomake go wyczyścić użytkownika toohello certyfikat, który jest wdrożony na swoich maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="191a9-232">Jeśli tworzenie maszyny Wirtualnej, a następnie zaktualizuj klucz tajny w magazynie kluczy hello hello nowy certyfikat nie jest pobrany tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="191a9-233">Pojawiły się maszyny wirtualne i nowych maszyn wirtualnych Uzyskaj nowy klucz tajny hello tooreference.</span><span class="sxs-lookup"><span data-stu-id="191a9-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="191a9-234">tooavoid, są wymagane tooreference wersję klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="191a9-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="191a9-235">Mojego zespołu współpracuje z kilka certyfikatów, które są dystrybuowane toous jako .cer kluczy publicznych.</span><span class="sxs-lookup"><span data-stu-id="191a9-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="191a9-236">Co to jest hello zalecane podejście do wdrażania tych zestaw skali maszyny wirtualnej tooa certyfikatów?</span><span class="sxs-lookup"><span data-stu-id="191a9-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="191a9-237">toodeploy cer kluczy publicznych tooa zestaw skali maszyny wirtualnej, można wygenerować pliku PFX, który zawiera tylko pliki cer.</span><span class="sxs-lookup"><span data-stu-id="191a9-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="191a9-238">toodo, użyj `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="191a9-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="191a9-239">Na przykład załadować plik cer hello jako obiekt x509Certificate2 w języku C# lub programu PowerShell, a następnie wywołaj metodę hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="191a9-240">Aby uzyskać więcej informacji, zobacz [metody X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="191a9-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="191a9-241">Nie ma opcji toopass użytkowników w certyfikatach jako ciąg base64.</span><span class="sxs-lookup"><span data-stu-id="191a9-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="191a9-242">Większość dostawców zasobów ma tę opcję.</span><span class="sxs-lookup"><span data-stu-id="191a9-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="191a9-243">przekazywanie certyfikatu jako ciąg base64 tooemulate hello najnowszej wersji adresu URL w szablonie usługi Resource Manager może wyodrębnić.</span><span class="sxs-lookup"><span data-stu-id="191a9-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="191a9-244">Obejmują następujące właściwości JSON w szablonie usługi Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="191a9-245">Certyfikaty toowrap są dostępne w obiektów JSON w magazynów kluczy?</span><span class="sxs-lookup"><span data-stu-id="191a9-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="191a9-246">Zestawy skalowania maszyn wirtualnych i maszyn wirtualnych certyfikaty muszą być ujęte w obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="191a9-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="191a9-247">Obsługujemy również hello typu zawartości application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="191a9-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="191a9-248">Aby uzyskać instrukcje na temat używania application/x-pkcs12, zobacz [certyfikatów PFX w usłudze Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="191a9-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="191a9-249">Obecnie nie obsługujemy .cer plików.</span><span class="sxs-lookup"><span data-stu-id="191a9-249">We currently do not support .cer files.</span></span> <span data-ttu-id="191a9-250">pliki .cer toouse, eksportowanie ich do kontenerów pfx.</span><span class="sxs-lookup"><span data-stu-id="191a9-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="191a9-251">Zgodność</span><span class="sxs-lookup"><span data-stu-id="191a9-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="191a9-252">Czy na pewno zgodnych zestawach skali maszyn wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="191a9-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="191a9-253">Zestawy skalowania maszyny wirtualnej są alokowania warstwę interfejsu API na powitania CRP.</span><span class="sxs-lookup"><span data-stu-id="191a9-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="191a9-254">Oba te składniki są częścią platforma obliczeniowa hello w hello Azure drzewa usługi.</span><span class="sxs-lookup"><span data-stu-id="191a9-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="191a9-255">Z punktu widzenia zgodności zestawy skalowania maszyny wirtualnej są integralną częścią hello platformy obliczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="191a9-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="191a9-256">One udostępniać zespołu, narzędzia procesów, metodę wdrażania, opcji zabezpieczeń, just in time (JIT) kompilacji, monitorowanie, alerty i itd., CRP hello, sama.</span><span class="sxs-lookup"><span data-stu-id="191a9-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="191a9-257">Zestawy skalowania maszyny wirtualnej są Payment Card Industry (PCI)-zgodne, ponieważ hello CRP jest częścią hello bieżące poświadczenie PCI danych zabezpieczeń Standard (DSS).</span><span class="sxs-lookup"><span data-stu-id="191a9-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="191a9-258">Aby uzyskać więcej informacji, zobacz [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="191a9-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="191a9-259">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="191a9-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="191a9-260">Jak usunąć rozszerzenia zestawu skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="191a9-261">toodelete skalowania maszyny wirtualnej ustawić rozszerzenia, użyj hello poniższy przykład środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="191a9-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="191a9-262">Można znaleźć wartości extensionName hello w `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="191a9-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="191a9-263">Istnieje już zestawu skalowania maszyny wirtualnej na przykład szablon, która integruje się z pakietem Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="191a9-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="191a9-264">Na przykład szablon, która integruje się z pakietem Operations Management Suite zestawu skalowania maszyn wirtualnych, zobacz drugi przykład Witaj w [wdrażanie klastra usługi sieć szkieletowa usług Azure i Włącz monitorowanie przy użyciu analizy dzienników](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="191a9-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="191a9-265">Rozszerzenia prawdopodobnie toorun równolegle na zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="191a9-266">Powoduje to, że moje toofail rozszerzenie skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="191a9-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="191a9-267">Co można zrobić toofix to?</span><span class="sxs-lookup"><span data-stu-id="191a9-267">What can I do toofix this?</span></span>

<span data-ttu-id="191a9-268">toolearn o sekwencjonowania rozszerzenia w zestawy skalowania maszyny wirtualnej, zobacz [sekwencjonowania rozszerzenia w zestawy skalowania maszyny wirtualnej platformy Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="191a9-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="191a9-269">Sposób resetowania hasła powitania dla maszyn wirtualnych w zestawu skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191a9-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="191a9-270">tooreset hello hasła dla maszyn wirtualnych w skali sieci maszyny wirtualnej zestawu, użyj rozszerzenia dostępu do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="191a9-271">Użyj hello poniższy przykład środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="191a9-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="191a9-272">Jak dodać rozszerzenie tooall maszyn wirtualnych w zestawu skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="191a9-273">Jeśli zasady aktualizacji ustawiono zbyt**automatyczne**, ponowne wdrożenie szablonu hello z nowymi właściwościami rozszerzenia hello aktualizacji wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="191a9-274">Jeśli zasady aktualizacji ustawiono zbyt**ręczne**, najpierw zaktualizuj rozszerzenie hello, a następnie ręcznie zaktualizuj wszystkie wystąpienia w maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="191a9-275">Jeśli hello rozszerzenia skojarzone z istniejącego zestawu skalowania maszyny wirtualnej zostaną zaktualizowane, czy istniejące maszyny wirtualne, których dotyczy problem?</span><span class="sxs-lookup"><span data-stu-id="191a9-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="191a9-276">(To znaczy będzie hello maszyn wirtualnych *nie* modelu zestawu skali maszyny wirtualnej hello dopasowania?) Czy są one zignorowane?</span><span class="sxs-lookup"><span data-stu-id="191a9-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="191a9-277">Gdy istniejącej maszyny zabliźnione usługi lub odtworzyć z obrazu, są hello skrypty, które są aktualnie skonfigurowane na zestaw skali maszyny wirtualnej hello wykonywane, lub hello skrypty, które zostały skonfigurowane stosowania hello najpierw utworzenia maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="191a9-278">Jeśli ustawione definicji rozszerzenia hello w skali maszyny wirtualnej hello zaktualizować modelu oraz zbyt ustawiono właściwość upgradePolicy hello**automatyczne**, aktualizuje hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="191a9-279">Jeśli właściwość upgradePolicy hello ustawiono zbyt**ręczne**, rozszerzenia są oznaczone jako niezgodny hello modelu.</span><span class="sxs-lookup"><span data-stu-id="191a9-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="191a9-280">W przypadku istniejącej maszyny Wirtualnej zabliźnione usługi, jest widoczny jako ponowne uruchomienie komputera, a hello rozszerzenia nie są ponownie.</span><span class="sxs-lookup"><span data-stu-id="191a9-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="191a9-281">Jeśli go zostanie odtworzone z obrazu, to tak, zastępując dysk systemu operacyjnego hello hello obrazu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="191a9-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="191a9-282">Wszelkie specjalizacji z najnowszego modelu hello, takie jak rozszerzenia, są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="191a9-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="191a9-283">Jak dołączyć do domeny tooan usługi Azure AD zestaw skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="191a9-284">toojoin domeny usługi Azure Active Directory (Azure AD) tooan zestaw skali maszyny wirtualnej, można określić rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="191a9-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="191a9-285">toodefine rozszerzenie, należy użyć właściwości JsonADDomainExtension hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="191a9-286">Moje rozszerzenia zestawu skali maszyny wirtualnej jest w trakcie tooinstall coś, co wymaga ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="191a9-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="191a9-287">Na przykład "commandToExecute": "powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature — nazwa FS-Resource-Manager-IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="191a9-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="191a9-288">Jeśli rozszerzenia zestawu skali maszyny wirtualnej jest w trakcie tooinstall coś, co wymaga ponownego uruchomienia, można użyć hello Azure Automation konfiguracji żądanego stanu (DSC automatyzacji) rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="191a9-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="191a9-289">Jeśli system operacyjny hello jest Windows Server 2012 R2, Azure ściąga w Instalatorze Windows Management Framework (WMF) 5.0 hello jest uruchamiany ponownie, a następnie kontynuuje hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="191a9-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="191a9-290">Jak włączyć ochrony przed złośliwym oprogramowaniem w zestawu skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191a9-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="191a9-291">tooturn na ochrony przed złośliwym oprogramowaniem w skali sieci maszyny wirtualnej ustawić, użyj hello poniższy przykład środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="191a9-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="191a9-292">Potrzebuję tooexecute niestandardowego skryptu, który znajduje się na koncie magazynu prywatnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="191a9-293">Witaj, skrypt zostanie uruchomiony pomyślnie, hello magazynu jest publiczny, ale podczas toouse dostępu sygnatury dostępu Współdzielonego, działanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="191a9-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="191a9-294">Ten komunikat jest wyświetlany: "Brak parametrów obowiązkowych współużytkowanego podpisu dostępu".</span><span class="sxs-lookup"><span data-stu-id="191a9-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="191a9-295">Łącze + SAS działa prawidłowo z przeglądarki sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="191a9-296">tooexecute niestandardowego skryptu, który znajduje się na koncie magazynu prywatne, określić ustawienia chronionego klucz konta magazynu hello i nazwę.</span><span class="sxs-lookup"><span data-stu-id="191a9-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="191a9-297">Aby uzyskać więcej informacji, zobacz [niestandardowe rozszerzenie skryptu systemu Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="191a9-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="191a9-298">Sieć</span><span class="sxs-lookup"><span data-stu-id="191a9-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="191a9-299">Jest to tooassign można ustawić skali tooa grupy zabezpieczeń sieci (NSG), dzięki czemu będą stosować tooall hello kart sieciowych maszyny Wirtualnej w zestawie hello?</span><span class="sxs-lookup"><span data-stu-id="191a9-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="191a9-300">Tak.</span><span class="sxs-lookup"><span data-stu-id="191a9-300">Yes.</span></span> <span data-ttu-id="191a9-301">Grupa zabezpieczeń sieci można stosować bezpośrednio zestawu skalowania tooa, umieszczając odwołanie do sekcji Networkinterfaceconfiguration hello hello profilu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="191a9-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="191a9-302">Przykład:</span><span class="sxs-lookup"><span data-stu-id="191a9-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="191a9-303">W jaki sposób wymiany wirtualnych adresów IP dla zestawach skali maszyn wirtualnych w hello sam subskrypcji i tego samego regionu?</span><span class="sxs-lookup"><span data-stu-id="191a9-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="191a9-304">Jeśli masz dwie wirtualne zestawach skali maszyn z przodu końców modułu równoważenia obciążenia Azure i są w hello tej samej subskrypcji i regionu, można cofnąć hello publicznych adresów IP z każdej z nich i przypisz toohello innych.</span><span class="sxs-lookup"><span data-stu-id="191a9-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="191a9-305">Zobacz [wymiany wirtualnych adresów IP: zielony niebieski wdrożenia usługi Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) np.</span><span class="sxs-lookup"><span data-stu-id="191a9-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="191a9-306">Opóźnienie to oznaczać, chociaż jako hello zasoby są alokację przydzielone na poziomie sieci hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="191a9-307">Opcja szybsza jest toouse bramy aplikacji Azure z dwóch pul zaplecza i reguły routingu.</span><span class="sxs-lookup"><span data-stu-id="191a9-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="191a9-308">Alternatywnie można udostępniać aplikacji z [usługi aplikacji Azure](https://azure.microsoft.com/en-us/services/app-service/) który zapewnia obsługę szybkie przełączanie między miejscami tymczasową i produkcyjną.</span><span class="sxs-lookup"><span data-stu-id="191a9-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="191a9-309">Jak określić zakres prywatny toouse adresy IP, statycznych alokacji prywatnego adresu IP?</span><span class="sxs-lookup"><span data-stu-id="191a9-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="191a9-310">Adresy IP są wybierane w podsieci, który określisz.</span><span class="sxs-lookup"><span data-stu-id="191a9-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="191a9-311">Metoda alokacji Hello adresów IP zestawu skali maszyny wirtualnej jest zawsze "dynamiczny", ale nie oznacza to, że można zmienić tych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="191a9-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="191a9-312">W takim przypadku "dynamiczny" tylko oznacza nieokreślenia hello adresu IP w żądaniu PUT.</span><span class="sxs-lookup"><span data-stu-id="191a9-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="191a9-313">Określ hello statycznych skonfigurowane przy użyciu hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="191a9-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="191a9-314">Jak wdrożyć maszynę wirtualną skali zestaw tooan istniejącej sieci wirtualnej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="191a9-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="191a9-315">toodeploy skalowania maszyny wirtualnej tooan istniejącej sieci wirtualnej platformy Azure, zobacz [wdrażania maszyny wirtualnej skali zestaw tooan istniejącej sieci wirtualnej](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="191a9-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="191a9-316">Jak dodać adres IP hello hello pierwsza maszyna wirtualna w skali maszyny wirtualnej ustawiony toohello wynik szablonu?</span><span class="sxs-lookup"><span data-stu-id="191a9-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="191a9-317">adres IP hello tooadd hello pierwszej maszyny Wirtualnej w maszynie wirtualnej skali zestaw toohello danych wyjściowych szablonu, zobacz [ARM: Pobierz VMSS prywatnych adresów IP](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="191a9-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="191a9-318">Przyspieszony sieciowych można używać zestawów skalowania?</span><span class="sxs-lookup"><span data-stu-id="191a9-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="191a9-319">Tak.</span><span class="sxs-lookup"><span data-stu-id="191a9-319">Yes.</span></span> <span data-ttu-id="191a9-320">toouse przyspieszony sieci, ustawienia enableAcceleratedNetworking tootrue Twojego skali zestawu elementów Networkinterfaceconfiguration.</span><span class="sxs-lookup"><span data-stu-id="191a9-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="191a9-321">Na przykład</span><span class="sxs-lookup"><span data-stu-id="191a9-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="191a9-322">Jak można skonfigurować hello serwery DNS używane przez zestaw skali</span><span class="sxs-lookup"><span data-stu-id="191a9-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="191a9-323">toocreate zestawu skalowania maszyny Wirtualnej z niestandardowej konfiguracji DNS, dodać sekcji Networkinterfaceconfiguration zestawu skalowania toohello dnsSettings JSON pakietów.</span><span class="sxs-lookup"><span data-stu-id="191a9-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="191a9-324">Przykład:</span><span class="sxs-lookup"><span data-stu-id="191a9-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="191a9-325">Jak można skonfigurować skali tooassign zestaw publiczny tooeach adres IP maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="191a9-326">toocreate zestawu skalowania maszyny Wirtualnej, która przypisuje publicznego tooeach adres IP maszyny Wirtualnej, upewnij się, że wersja hello interfejsu API hello Microsoft.Compute/virtualMAchineScaleSets zasobów jest 2017-03-30 i Dodaj _publicipaddressconfiguration_ pakietów JSON elementy Ipconfiguration sekcji zestawu skalowania toohello.</span><span class="sxs-lookup"><span data-stu-id="191a9-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="191a9-327">Przykład:</span><span class="sxs-lookup"><span data-stu-id="191a9-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="191a9-328">Z wielu bram aplikacji można skonfigurować toowork zestaw skalowania?</span><span class="sxs-lookup"><span data-stu-id="191a9-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="191a9-329">Tak.</span><span class="sxs-lookup"><span data-stu-id="191a9-329">Yes.</span></span> <span data-ttu-id="191a9-330">Możesz dodać hello identyfikator zasobu w dla wielu toohello pule adresów zaplecza bramy aplikacji _applicationGatewayBackendAddressPools_ liście hello _Ipconfiguration_ sekcji zestawu skali profil sieci.</span><span class="sxs-lookup"><span data-stu-id="191a9-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="191a9-331">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="191a9-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="191a9-332">W przypadku jakich może utworzyć skali maszyny wirtualnej ustawić z mniej niż dwóch maszyn wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="191a9-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="191a9-333">Jedną z przyczyn toocreate zestawu skalowania maszyn wirtualnych z mniej niż dwóch maszyn wirtualnych zostałaby użyta właściwości elastycznej hello toouse skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="191a9-334">Na przykład można wdrożyć zestaw skali maszyny wirtualnej o zero toodefine maszyn wirtualnych infrastruktury bez płatności koszty maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="191a9-335">Następnie gdy wszystko jest gotowe toodeploy maszyn wirtualnych, Zwiększ hello "pojemność" liczba wystąpień produkcji toohello zestaw hello maszyny wirtualnej skali.</span><span class="sxs-lookup"><span data-stu-id="191a9-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="191a9-336">Kolejny powód, które można tworzyć skali maszyny wirtualnej ustawić z mniej niż dwóch maszyn wirtualnych jest, jeśli jesteś danego mniej dostępności niż przy użyciu zestawu z maszynami wirtualnymi odrębny dostępności.</span><span class="sxs-lookup"><span data-stu-id="191a9-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="191a9-337">Zestawy skalowania maszyny wirtualnej nadaj toowork sposób z jednostkami niesortowalne obliczeniowe, które są zamienne.</span><span class="sxs-lookup"><span data-stu-id="191a9-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="191a9-338">Ta jednolitość jest główną różnicą dla zestawy skalowania maszyny wirtualnej i zestawów dostępności.</span><span class="sxs-lookup"><span data-stu-id="191a9-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="191a9-339">Wiele obciążeń bezstanowych nie Śledź pojedyncze jednostki.</span><span class="sxs-lookup"><span data-stu-id="191a9-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="191a9-340">Spadnie hello obciążenie, można dół Jednostka obliczeniowa tooone i następnie skalowanie w górę toomany podczas zwiększa obciążenie hello.</span><span class="sxs-lookup"><span data-stu-id="191a9-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="191a9-341">Jak zmienić hello liczbę maszyn wirtualnych w zestawie skalowania maszyn wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="191a9-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="191a9-342">toochange hello liczbę maszyn wirtualnych w zestawie skalowania maszyn wirtualnych, zobacz [zmienić hello liczba wystąpień zestawu skali maszyny wirtualnej](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="191a9-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="191a9-343">Jak określić niestandardowe alerty po osiągnięciu progów niektórych?</span><span class="sxs-lookup"><span data-stu-id="191a9-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="191a9-344">Masz pewną swobodę określania w sposób obsługi alertów dla określonej wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="191a9-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="191a9-345">Na przykład można zdefiniować niestandardowych elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="191a9-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="191a9-346">Poniższy przykład elementu webhook Hello jest z szablonem usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="191a9-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="191a9-347">W tym przykładzie alert przechodzi tooPagerduty.com po osiągnięciu progu.</span><span class="sxs-lookup"><span data-stu-id="191a9-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="191a9-348">Operacje i stosowanie poprawek</span><span class="sxs-lookup"><span data-stu-id="191a9-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="191a9-349">Jak utworzyć skali w istniejącej grupie zasobów?</span><span class="sxs-lookup"><span data-stu-id="191a9-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="191a9-350">Tworzenie zestawów skali w istniejący zasób grupy nie jest jeszcze możliwe z hello portalu Azure, ale można określić istniejącą grupę zasobów, podczas wdrażania skali ustawiony na podstawie szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="191a9-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="191a9-351">Można również określić istniejącą grupę zasobów podczas tworzenia skali ustawić za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="191a9-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="191a9-352">Grupa zasobów tooanother zestawu skali możemy przenieść?</span><span class="sxs-lookup"><span data-stu-id="191a9-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="191a9-353">Tak, można przenosić skalę zestawu zasobów tooa nowej subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="191a9-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="191a9-354">Jak zaktualizować tooI tooa nowy obraz zestawu Moje skalowania maszyn wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="191a9-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="191a9-355">Jak zarządzać stosowanie poprawek</span><span class="sxs-lookup"><span data-stu-id="191a9-355">How do I manage patching?</span></span>

<span data-ttu-id="191a9-356">Zobacz tooupdate Twojego skalowania maszyny wirtualnej ustawić nowy obraz tooa i stosowanie poprawek toomanage, [Uaktualnij zestaw skali maszyny wirtualnej](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="191a9-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="191a9-357">Tooreset operacja odtworzenia z obrazu hello Maszynę wirtualną można używać bez zmieniania hello obrazu?</span><span class="sxs-lookup"><span data-stu-id="191a9-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="191a9-358">(Czyli chcę Resetowanie ustawień toofactory maszyny Wirtualnej zamiast tooa nowy obraz.)</span><span class="sxs-lookup"><span data-stu-id="191a9-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="191a9-359">Tak, można użyć tooreset operacja odtworzenia z obrazu hello maszyny Wirtualnej bez zmieniania hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="191a9-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="191a9-360">Jednak jeśli zestawu skalowania maszyn wirtualnych, sieci odwołuje się do obrazu platformy z `version = latest`, maszyny Wirtualnej można aktualizować tooa nowszego systemu operacyjnego obrazu podczas wywoływania `reimage`.</span><span class="sxs-lookup"><span data-stu-id="191a9-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="191a9-361">Aby uzyskać więcej informacji, zobacz [Zarządzanie wszystkich maszyn wirtualnych w zestawie skalowania maszyn wirtualnych](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="191a9-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="191a9-362">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="191a9-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="191a9-363">Jak włączyć diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="191a9-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="191a9-364">tooturn na diagnostyki rozruchu, najpierw utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="191a9-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="191a9-365">Następnie, umieść ten blok JSON do zestawu skalowania maszyny wirtualnej **virtualMachineProfile**i zaktualizuj zestaw skali maszyny wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="191a9-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="191a9-366">Podczas tworzenia nowej maszyny Wirtualnej hello InstanceView właściwość hello wirtualna Wyświetla szczegóły hello hello zrzut ekranu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="191a9-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="191a9-367">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="191a9-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="191a9-368">Właściwości maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191a9-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="191a9-369">Jak uzyskać informacje dotyczące właściwości dla każdej maszyny Wirtualnej bez wykonywania wywołań wielu?</span><span class="sxs-lookup"><span data-stu-id="191a9-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="191a9-370">Na przykład jak może uzyskać hello domeny błędów dla każdego hello 100 maszyn wirtualnych w zestawu skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="191a9-371">informacje dotyczące właściwości tooget dla każdej maszyny Wirtualnej bez wykonywania wielu wywołań, należy wywołać `ListVMInstanceViews` za pomocą interfejsu API REST `GET` na powitania następującego identyfikatora URI zasobu:</span><span class="sxs-lookup"><span data-stu-id="191a9-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="191a9-372">/Subscriptions/ < IDENTYFIKATOR_SUBSKRYPCJI > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $rozwiń = instanceView & $select = instanceView</span><span class="sxs-lookup"><span data-stu-id="191a9-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="191a9-373">Można przekazywać argumenty inne rozszerzenie toodifferent maszyn wirtualnych w zestawie skalowania maszyn wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="191a9-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="191a9-374">Nie, nie można przekazywać argumenty inne rozszerzenie toodifferent maszyn wirtualnych w zestawie skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="191a9-375">Jednak rozszerzenia może działać przy hello unikatowy właściwości hello są uruchamiane na przykład na powitania nazwa komputera maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="191a9-376">Rozszerzenia również mogą wysyłać zapytania metadanych wystąpienia na http://169.254.169.254 tooget więcej informacji na temat hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="191a9-377">Dlaczego są luki pomiędzy Moje nazw maszyn maszyny Wirtualnej zestawu skali maszyny wirtualnej i identyfikatory maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191a9-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="191a9-378">Na przykład: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="191a9-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="191a9-379">Brak przerw między nazw maszyn maszyny Wirtualnej zestawu skali maszyny wirtualnej i identyfikatory maszyny Wirtualnej ponieważ zestawu skalowania maszyn wirtualnych, sieci **nadmiernej aprowizacji** właściwość jest ustawiona wartość domyślna toohello **true**.</span><span class="sxs-lookup"><span data-stu-id="191a9-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="191a9-380">Jeśli nadmiarowe Inicjowanie obsługi administracyjnej jest ustawiona zbyt**true**, VMs więcej niż żądana są tworzone.</span><span class="sxs-lookup"><span data-stu-id="191a9-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="191a9-381">Dodatkowe maszyny wirtualne są usuwane.</span><span class="sxs-lookup"><span data-stu-id="191a9-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="191a9-382">W takim przypadku uzyskania wdrożenia większą niezawodność, ale na powitania koszt ciągłe nazewnictwa i ciągłe translatora adresów sieciowych (NAT) reguły.</span><span class="sxs-lookup"><span data-stu-id="191a9-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="191a9-383">Tę właściwość można ustawić za**false**.</span><span class="sxs-lookup"><span data-stu-id="191a9-383">You can set this property too**false**.</span></span> <span data-ttu-id="191a9-384">Dla zestawów skalowania małych maszyny wirtualnej to nie znacząco wpłynąć na niezawodność wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="191a9-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="191a9-385">Jaka jest różnica hello usuwania maszyny Wirtualnej w zestawie skalowania maszyn wirtualnych i dealokowanie hello maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="191a9-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="191a9-386">Po jednym za pośrednictwem hello innych wybrać?</span><span class="sxs-lookup"><span data-stu-id="191a9-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="191a9-387">Witaj podstawowa różnica między usuwania maszyny Wirtualnej w zestawie skalowania maszyn wirtualnych i dealokowanie hello maszyny Wirtualnej jest to, że `deallocate` nie powoduje usunięcia hello wirtualnych dysków twardych (VHD).</span><span class="sxs-lookup"><span data-stu-id="191a9-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="191a9-388">Są skojarzone z uruchomioną kosztów magazynowania `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="191a9-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="191a9-389">Może używać co najmniej hello innych jednego hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="191a9-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="191a9-390">Ma toostop płatności kosztów obliczeń, ale ma stan dysku hello tookeep hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="191a9-391">Szybciej, niż można skalować w poziomie zestaw skali maszyny wirtualnej ma toostart zestaw maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="191a9-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="191a9-392">Scenariusz pokrewne toothis zostały utworzone własnego aparatu skalowania automatycznego i chcesz szybsze skali end-to-end.</span><span class="sxs-lookup"><span data-stu-id="191a9-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="191a9-393">Masz zestaw skali maszyny wirtualnej, która nierównomiernie jest dystrybuowana do domen błędów lub domen aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="191a9-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="191a9-394">Może to być, ponieważ selektywnie usunąć maszyn wirtualnych lub maszyn wirtualnych zostały usunięte po nadmiarowe Inicjowanie obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="191a9-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="191a9-395">Uruchomiona `stop deallocate` następuje `start` na maszynie wirtualnej hello równomiernie zestaw skalowania rozdziela hello maszyn wirtualnych w domenach awarii lub domen aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="191a9-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

