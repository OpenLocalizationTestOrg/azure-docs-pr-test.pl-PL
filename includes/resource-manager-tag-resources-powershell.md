Wersja 3.0 moduł AzureRm.Resources hello uwzględnione znaczących zmian w sposób pracy z tagami. Przed kontynuowaniem sprawdź swoją wersję:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Jeśli wyniki wskazują, wersja 3.0 lub nowszej, hello przykłady w tym temacie pracować ze środowiskiem. Jeśli nie masz wersji 3.0 lub nowszej, przed kontynuowaniem pracy z tym tematem [zaktualizuj swoją wersję](/powershell/azureps-cmdlets-docs/) za pomocą Galerii programu PowerShell lub Instalatora platformy sieci Web.

```powershell
Version
-------
3.5.0
```

toosee hello znaczników dla *grupy zasobów*, użyj:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Czy skrypt zwraca hello następującego formatu:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello znaczników dla *zasób, który ma identyfikator określonego zasobu*, użyj:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Lub toosee hello znaczników dla *zasób, który ma nazwę i zasobów do określonej grupy*, użyj:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *grup zasobów, które mają określonego tagu*, użyj:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *zasoby, które mają konkretnego znacznika*, użyj:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Zawsze należy zastosować tagi tooa zasób lub grupa zasobów, należy zastąpić znaczników hello na tym zasób lub grupa zasobów. W związku z tym należy użyć innego podejścia opartego na czy hello zasób lub grupa zasobów ma znaczników. 

tooadd znaczniki tooa *grupy zasobów bez znaczników*, użyj:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd znaczniki tooa *grupę zasobów, która ma znaczników*, pobrać hello znaczników, Dodaj nowy znacznik hello i ponownie zastosuj tagi hello:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd znaczniki tooa *zasobu bez znaczników*, użyj:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd znaczniki tooa *zasobu, który znaczników*, użyj:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *nie zachować istniejące znaczniki zasobów hello*, użyj następującego skryptu hello:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *zachować istniejące znaczniki na zasoby, które nie są duplikatami*, użyj następującego skryptu hello:

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

tooremove wszystkie tagi, Przekaż tablicy skrótów pusta:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



