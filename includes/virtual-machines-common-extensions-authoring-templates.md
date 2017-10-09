## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="506a5-101">Omówienie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="506a5-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="506a5-102">Szablony usługi Azure Resource Manager pozwala toodeclaratively Określ hello Azure IaaS infrastruktury w języku Json, definiując hello zależności między zasobami.</span><span class="sxs-lookup"><span data-stu-id="506a5-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="506a5-103">Szczegółowe omówienie szablony Menedżera zasobów Azure przeczytaj artykuł toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="506a5-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="506a5-104">Omówienie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="506a5-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="506a5-105">Przykładowy szablon fragment dotyczący rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="506a5-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="506a5-106">Wdrażanie rozszerzeń maszyny Wirtualnej, zgodnie z częścią szablonu usługi Azure Resource Manager wymaga toodeclaratively Określ Konfiguracja rozszerzenia hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="506a5-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="506a5-107">Oto hello format służący do określania hello konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="506a5-107">Here is hello format for specifying hello extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="506a5-108">Jak widać z powyższych hello hello rozszerzenia szablonu zawiera dwie główne części:</span><span class="sxs-lookup"><span data-stu-id="506a5-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="506a5-109">Rozszerzenie nazwy, wydawcy i wersji</span><span class="sxs-lookup"><span data-stu-id="506a5-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="506a5-110">Konfiguracja rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="506a5-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="506a5-111">Identyfikowanie hello wydawcy, typ i typeHandlerVersion dla dowolnego rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="506a5-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="506a5-112">Rozszerzenia maszyny Wirtualnej platformy Azure są opublikowane przez firmę Microsoft i zaufane 3 wydawców firm i każde rozszerzenie jest unikatowo identyfikowana przez jej wydawcę, typ i hello typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="506a5-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="506a5-113">Te można określić jako następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="506a5-113">These can be determined as following:</span></span>  

