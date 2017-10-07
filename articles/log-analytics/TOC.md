# Omówienie
## [Co to jest usługa Log Analytics?](log-analytics-overview.md)
## [Bezpieczeństwo danych](log-analytics-security.md)

# Wprowadzenie
## [Tworzenie konta usługi Log Analytics](log-analytics-get-started.md)
## [Zarządzanie dostępem](log-analytics-manage-access.md)
## [Dane użycia](log-analytics-usage.md)
## [Log Analytics — często zadawane pytania](log-analytics-faq.md)
## [Dostawcy usług](log-analytics-service-providers.md)

# Instrukcje
## Zbieranie danych
### Połączone źródła
#### [Agenci dla systemu Windows](log-analytics-windows-agents.md)
#### [Agenci dla systemu Linux](log-analytics-agent-linux.md)
#### [Maszyny wirtualne platformy Azure](log-analytics-azure-vm-extension.md)
#### [Zasoby platformy Azure](log-analytics-azure-storage.md)
#### [Operations Manager](log-analytics-om-agents.md)
#### [Configuration Manager](log-analytics-sccm.md)
#### [Brama pakietu OMS](log-analytics-oms-gateway.md)
### Źródła danych
#### [Omówienie źródeł danych](log-analytics-data-sources.md)
#### [Zdarzenia systemu Windows](log-analytics-data-sources-windows-events.md)
#### [Niestandardowe dane JSON](log-analytics-data-sources-json.md)
#### [Zebrane dane wydajności](log-analytics-data-sources-collectd.md)
#### [Alerty programów Nagios i Zabbix](log-analytics-data-sources-alerts-nagios-zabbix.md)
#### [Dziennik systemu](log-analytics-data-sources-syslog.md)
#### [Liczniki wydajności](log-analytics-data-sources-performance-counters.md)
#### [Wydajność aplikacji dla systemu Linux](log-analytics-data-sources-linux-applications.md)
#### [Dzienniki usług IIS](log-analytics-data-sources-iis-logs.md)
#### [Niestandardowe dzienniki](log-analytics-data-sources-custom-logs.md)
#### [Niestandardowe pola](log-analytics-custom-fields.md)

## Zapytania o dane
### [Wyszukiwanie w dzienniku — omówienie](log-analytics-log-searches.md)
### [Dokumentacja wyszukiwania](log-analytics-search-reference.md)
#### [Wyrażenia regularne](log-analytics-log-searches-regex.md)
### [Podejmowanie akcji z poziomu wyników wyszukiwania](log-analytics-log-search-takeaction.md)
### [Grupy komputerów](log-analytics-computer-groups.md)

## Nowe wyszukiwanie w dzienniku
### [Uaktualnianie obszaru roboczego](log-analytics-log-search-upgrade.md)
### [Często zadawane pytania](log-analytics-log-search-faq.md)
### [Wyszukiwanie w dzienniku — omówienie](log-analytics-log-search-new.md)
### [Portale do wyszukiwania w dzienniku](log-analytics-log-search-portals.md)
#### [Za pomocą hello dziennik wyszukiwania portalu](log-analytics-log-search-log-search-portal.md)
### [Przechodzenie ze starszego języka](log-analytics-log-search-transition.md)
### [Flow connector (Łącznik usługi Flow)](log-analytics-flow-tutorial.md)

## Analizowanie danych
### [Pulpity nawigacyjne](log-analytics-dashboards.md)
### [Projektant widoków](log-analytics-view-designer.md)
### [Power BI](log-analytics-powerbi.md)
## Tworzenie alertów
### [Informacje o alertach](log-analytics-alerts.md)
### [Akcje alertów](log-analytics-alerts-actions.md)
### Tworzenie reguł alertów
#### [Portal pakietu OMS](log-analytics-alerts-creating.md)
#### [Interfejs API REST](log-analytics-api-alerts.md)
#### [Szablon usługi Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
### [Przykład akcji elementu webhook](log-analytics-alerts-webhooks.md)
### [Rozwiązanie do zarządzania alertami](log-analytics-solution-alert-management.md)
## Korzystanie z rozwiązań
### [Omówienie rozwiązań](log-analytics-add-solutions.md)
### [Rozwiązania docelowe](../operations-management-suite/operations-management-suite-solution-targeting.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Activity Log Analytics](log-analytics-activity.md)
### [Ocena usługi AD](log-analytics-ad-assessment.md)
### [Stan replikacji usługi AD](log-analytics-ad-replication-status.md)
### [Kondycja agenta](../operations-management-suite/oms-solution-agenthealth.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Zarządzanie alertami](log-analytics-solution-alert-management.md)
### [Application Insights Connector](log-analytics-app-insights-connector.md)
### [Azure SQL Analytics](log-analytics-azure-sql.md)
### [Analiza w usłudze Azure Web Apps](log-analytics-azure-web-apps-analytics.md)
### [Pojemność i wydajność](log-analytics-capacity.md)
### [Śledzenie zmian](log-analytics-change-tracking.md)
### [Kontenery](log-analytics-containers.md)
### [Analiza DNS](log-analytics-dns.md)
### [Łącznik zarządzania usługami IT](log-analytics-itsmc-overview.md)
#### [Połączenia zarządzania usługami IT](log-analytics-itsmc-connections.md)
### [Usługa Key Vault](log-analytics-azure-key-vault.md)
### Logic Apps — wiadomości B2B
#### [Logic Apps — rozwiązanie do obsługi wiadomości B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md?toc=%2fazure%2flog-analytics%2ftoc.json)
#### [Logic Apps — niestandardowy schemat śledzenia B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Ocena złośliwego oprogramowania](log-analytics-malware.md)
### [Analiza sieci](log-analytics-azure-networking-analytics.md)
### [Monitor wydajności sieci](log-analytics-network-performance-monitor.md)
### [Office 365](../operations-management-suite/oms-solution-office-365.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Ocena oprogramowania SCOM](log-analytics-scom-assessment.md)
### [Inspekcja zabezpieczeń](../operations-management-suite/oms-security-getting-started.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Usługa Service Fabric używana z programem PowerShell](log-analytics-service-fabric.md)
#### [Usługa Service Fabric używana z usługą Azure Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
### [Mapa usługi](../operations-management-suite/operations-management-suite-service-map.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Ocena serwera SQL](log-analytics-sql-assessment.md)
### [Surface Hub](log-analytics-surface-hubs.md)
### [Zarządzanie aktualizacjami](../operations-management-suite/oms-solution-update-management.md)
### [VMware](log-analytics-vmware.md)
### Analiza systemu Windows
#### [Zgodność aktualizacji](https://technet.microsoft.com/itpro/windows/manage/update-compliance-get-started)
#### [Gotowość do uaktualnienia](https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started)
### [Dane o komunikacji sieciowej](log-analytics-wire-data.md)
## Programowanie
### [Interfejs API modułu zbierającego dane](log-analytics-data-collector-api.md)
### [Polecenia cmdlet programu PowerShell](log-analytics-powershell-workspace-configuration.md)
### [Szablony usługi Resource Manager](log-analytics-template-workspace-configuration.md)
### [Interfejs API wyszukiwania w dzienniku](log-analytics-log-search-api.md)
#### [Python](log-analytics-log-search-api-python.md)
### [Interfejs API alertów](log-analytics-api-alerts.md)

# Dokumentacja
## [Program PowerShell](/powershell/module/azurerm.operationalinsights)
## [REST](/rest/api/loganalytics)

# Zasoby
## [Harmonogram działania dla platformy Azure](https://azure.microsoft.com/roadmap/)
## [Cennik](https://azure.microsoft.com/pricing/details/log-analytics/)
## [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/)
## [Aktualizacje usług](https://azure.microsoft.com/updates/?product=log-analytics)
## [Analiza systemu Windows](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics)
