Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny. Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS.

Na przykład hello domeny "contoso.com" może zawierać wiele rekordów DNS, takie jak "mail.contoso.com" (dla serwera poczty) i "www.contoso.com" (dla witryny sieci web).

Podczas tworzenia strefy DNS w usłudze Azure DNS należy uwzględnić następujące kwestie:

* Nazwa Hello hello strefy musi być unikatowa w obrębie grupy zasobów hello i hello strefy nie może już istnieć. W przeciwnym razie hello kończy się niepowodzeniem.
* Witaj, który można ponownie użyć tej samej nazwy strefy w innej grupie zasobów lub innej subskrypcji platformy Azure.
* Gdzie udostępniania wielu strefach hello tej samej nazwie, każde wystąpienie jest przypisany adresów serwerów inną nazwę. Tylko jeden zestaw adresów można skonfigurować za pomocą rejestratora nazw domen hello.

> [!NOTE]
> Nie masz tooown toocreate nazwy domeny strefę DNS z tą nazwą domeny w usłudze Azure DNS. Jednak należy tooown hello domeny tooconfigure hello Azure serwery DNS jako serwery nazw poprawny dla nazwy domeny hello z Rejestratora nazw domen hello hello.
> 
> Aby uzyskać więcej informacji, zobacz [delegować tooAzure domeny DNS](../articles/dns/dns-domain-delegation.md).
