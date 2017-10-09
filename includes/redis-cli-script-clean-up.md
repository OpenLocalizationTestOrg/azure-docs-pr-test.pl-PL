## <a name="clean-up-deployment"></a><span data-ttu-id="ee5a7-101">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ee5a7-101">Clean up deployment</span></span> 

<span data-ttu-id="ee5a7-102">Po uruchomieniu przykładowym skrypcie hello hello wykonaj polecenie może być grupa zasobów hello tooremove używane, wystąpienia pamięci podręcznej Redis Azure i powiązanych zasobów w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ee5a7-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```