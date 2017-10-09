### <a name="troubleshoot-azure-diagnostics"></a>Rozwiązywanie problemów z funkcją Diagnostyka Azure

Jeśli zostanie wyświetlony następujący komunikat o błędzie hello, nie jest zarejestrowany dostawca zasobów w elemencie Microsoft.insights hello:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

Dostawca zasobów hello tooregister, wykonaj następujące kroki w portalu Azure hello hello:

1.  W okienku nawigacji hello po lewej stronie powitania kliknij *subskrypcji*
2.  Wybierz subskrypcję hello zidentyfikowany w komunikacie o błędzie hello
3.  Kliknij pozycję *Dostawcy zasobów*
4.  Znajdź hello *elemencie Microsoft.insights* dostawcy
5.  Kliknij przycisk hello *zarejestrować* łącza

![Rejestrowanie dostawcy zasobów microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Raz hello *elemencie Microsoft.insights* dostawcy zasobów jest zarejestrowany, ponów próbę wykonania konfigurowania diagnostyki.


W programie PowerShell Jeśli zostanie wyświetlony następujący komunikat o błędzie hello należy tooupdate używanej wersji programu PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Zaktualizuj swoją wersję środowiska PowerShell toohello listopada 2016 (v2.3.0) lub nowszych wersji przy użyciu instrukcji hello w hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artykułu.
