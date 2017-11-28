<span data-ttu-id="29ec8-101">W wersji 3.0 modułu AzureRm.Resources wprowadzono istotne zmiany w sposobie pracy z tagami.</span><span class="sxs-lookup"><span data-stu-id="29ec8-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="29ec8-102">Przed kontynuowaniem sprawdź swoją wersję:</span><span class="sxs-lookup"><span data-stu-id="29ec8-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="29ec8-103">Jeśli masz wersję 3.0 lub nowszą, przykłady z tego tematu zadziałają w Twoim środowisku.</span><span class="sxs-lookup"><span data-stu-id="29ec8-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="29ec8-104">Jeśli nie masz wersji 3.0 lub nowszej, przed kontynuowaniem pracy z tym tematem [zaktualizuj swoją wersję](/powershell/azureps-cmdlets-docs/) za pomocą Galerii programu PowerShell lub Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="29ec8-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="29ec8-105">Aby wyświetlić istniejące tagi dla *grupy zasobów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-105">To see the existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="29ec8-106">Ten skrypt zwraca następujący format:</span><span class="sxs-lookup"><span data-stu-id="29ec8-106">That script returns the following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="29ec8-107">Aby wyświetlić istniejące tagi dla *zasobu o określonym identyfikatorze zasobu*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-107">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="29ec8-108">Aby wyświetlić istniejące tagi dla *zasobu o określonej nazwie i grupie zasobów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-108">Or, to see the existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="29ec8-109">Aby uzyskać *grupy zasobów, które mają konkretny tag*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-109">To get *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="29ec8-110">Aby uzyskać *zasoby, które mają konkretny tag*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-110">To get *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="29ec8-111">Za każdym razem, gdy stosujesz tagi do zasobu lub grupy zasobów, istniejące tagi tego zasobu lub tej grupy zasobów są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="29ec8-111">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="29ec8-112">Dlatego konieczne jest różne podejście w zależności od tego, czy dany zasób lub dana grupa zasobów ma istniejące tagi.</span><span class="sxs-lookup"><span data-stu-id="29ec8-112">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="29ec8-113">Aby dodać tagi do *grupy zasobów bez istniejących tagów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-113">To add tags to a *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="29ec8-114">Aby dodać tagi do *grupy zasobów z istniejącymi tagami*, pobierz istniejące tagi, dodaj nowy tag i ponownie zastosuj tagi:</span><span class="sxs-lookup"><span data-stu-id="29ec8-114">To add tags to a *resource group that has existing tags*, retrieve the existing tags, add the new tag, and reapply the tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="29ec8-115">Aby dodać tagi do *zasobu bez istniejących tagów*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-115">To add tags to a *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="29ec8-116">Aby dodać tagi do *zasobu z istniejącymi tagami*, użyj:</span><span class="sxs-lookup"><span data-stu-id="29ec8-116">To add tags to a *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="29ec8-117">Aby zastosować wszystkie tagi z grupy zasobów do jej zasobów *bez zachowania tagów istniejących w zasobach*, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="29ec8-117">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="29ec8-118">Aby zastosować wszystkie tagi z grupy zasobów do jej zasobów *z zachowaniem tagów istniejących w zasobach, które nie są duplikatami*, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="29ec8-118">To apply all tags from a resource group to its resources, and *retain existing tags on resources that are not duplicates*, use the following script:</span></span>

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

<span data-ttu-id="29ec8-119">Aby usunąć wszystkie tagi, przekaż pustą tablicę skrótów:</span><span class="sxs-lookup"><span data-stu-id="29ec8-119">To remove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



