<span data-ttu-id="6a279-101">Wersja 3.0 moduł AzureRm.Resources hello uwzględnione znaczących zmian w sposób pracy z tagami.</span><span class="sxs-lookup"><span data-stu-id="6a279-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="6a279-102">Przed kontynuowaniem sprawdź swoją wersję:</span><span class="sxs-lookup"><span data-stu-id="6a279-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="6a279-103">Jeśli wyniki wskazują, wersja 3.0 lub nowszej, hello przykłady w tym temacie pracować ze środowiskiem.</span><span class="sxs-lookup"><span data-stu-id="6a279-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="6a279-104">Jeśli nie masz wersji 3.0 lub nowszej, przed kontynuowaniem pracy z tym tematem [zaktualizuj swoją wersję](/powershell/azureps-cmdlets-docs/) za pomocą Galerii programu PowerShell lub Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6a279-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="6a279-105">toosee hello znaczników dla *grupy zasobów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="6a279-106">Czy skrypt zwraca hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="6a279-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="6a279-107">toosee hello znaczników dla *zasób, który ma identyfikator określonego zasobu*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="6a279-108">Lub toosee hello znaczników dla *zasób, który ma nazwę i zasobów do określonej grupy*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="6a279-109">tooget *grup zasobów, które mają określonego tagu*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="6a279-110">tooget *zasoby, które mają konkretnego znacznika*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="6a279-111">Zawsze należy zastosować tagi tooa zasób lub grupa zasobów, należy zastąpić znaczników hello na tym zasób lub grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a279-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="6a279-112">W związku z tym należy użyć innego podejścia opartego na czy hello zasób lub grupa zasobów ma znaczników.</span><span class="sxs-lookup"><span data-stu-id="6a279-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="6a279-113">tooadd znaczniki tooa *grupy zasobów bez znaczników*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="6a279-114">tooadd znaczniki tooa *grupę zasobów, która ma znaczników*, pobrać hello znaczników, Dodaj nowy znacznik hello i ponownie zastosuj tagi hello:</span><span class="sxs-lookup"><span data-stu-id="6a279-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="6a279-115">tooadd znaczniki tooa *zasobu bez znaczników*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="6a279-116">tooadd znaczniki tooa *zasobu, który znaczników*, użyj:</span><span class="sxs-lookup"><span data-stu-id="6a279-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="6a279-117">tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *nie zachować istniejące znaczniki zasobów hello*, użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="6a279-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="6a279-118">tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *zachować istniejące znaczniki na zasoby, które nie są duplikatami*, użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="6a279-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="6a279-119">tooremove wszystkie tagi, Przekaż tablicy skrótów pusta:</span><span class="sxs-lookup"><span data-stu-id="6a279-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



