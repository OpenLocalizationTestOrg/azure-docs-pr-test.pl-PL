### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="d7384-101">Rozwiązywanie problemów z funkcją Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="d7384-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="d7384-102">Jeśli zostanie wyświetlony następujący komunikat o błędzie hello, nie jest zarejestrowany dostawca zasobów w elemencie Microsoft.insights hello:</span><span class="sxs-lookup"><span data-stu-id="d7384-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="d7384-103">Dostawca zasobów hello tooregister, wykonaj następujące kroki w portalu Azure hello hello:</span><span class="sxs-lookup"><span data-stu-id="d7384-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="d7384-104">W okienku nawigacji hello po lewej stronie powitania kliknij *subskrypcji*</span><span class="sxs-lookup"><span data-stu-id="d7384-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="d7384-105">Wybierz subskrypcję hello zidentyfikowany w komunikacie o błędzie hello</span><span class="sxs-lookup"><span data-stu-id="d7384-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="d7384-106">Kliknij pozycję *Dostawcy zasobów*</span><span class="sxs-lookup"><span data-stu-id="d7384-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="d7384-107">Znajdź hello *elemencie Microsoft.insights* dostawcy</span><span class="sxs-lookup"><span data-stu-id="d7384-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="d7384-108">Kliknij przycisk hello *zarejestrować* łącza</span><span class="sxs-lookup"><span data-stu-id="d7384-108">Click hello *Register* link</span></span>

![Rejestrowanie dostawcy zasobów microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="d7384-110">Raz hello *elemencie Microsoft.insights* dostawcy zasobów jest zarejestrowany, ponów próbę wykonania konfigurowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="d7384-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="d7384-111">W programie PowerShell Jeśli zostanie wyświetlony następujący komunikat o błędzie hello należy tooupdate używanej wersji programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d7384-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="d7384-112">Zaktualizuj swoją wersję środowiska PowerShell toohello listopada 2016 (v2.3.0) lub nowszych wersji przy użyciu instrukcji hello w hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d7384-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
