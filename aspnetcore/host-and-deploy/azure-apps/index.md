---
title: Distribuire le app ASP.NET Core in Servizio app di Azure
author: guardrex
description: Questo articolo contiene collegamenti a risorse di hosting e distribuzione di Azure.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: c55a5202643bb947b3f38f67aec55ee5cf7b1496
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244749"
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a>Distribuire le app ASP.NET Core in Servizio app di Azure

Il [servizio app di Azure](https://azure.microsoft.com/services/app-service/) è un [servizio di piattaforma di cloud computing Microsoft](https://azure.microsoft.com/) per l'hosting di app Web, inclusa ASP.NET Core.

## <a name="useful-resources"></a>Risorse utili

[Documentazione di App Web](/azure/app-service/) di Azure è la home page della documentazione, delle esercitazioni, degli esempi, delle guide introduttive e di altre risorse per le app di Azure. Due importanti esercitazioni relative all'hosting di app ASP.NET Core sono:

[Guida introduttiva: Creare un'app Web ASP.NET Core in Azure](/azure/app-service/app-service-web-get-started-dotnet)  
Usare Visual Studio per creare e distribuire un'app Web ASP.NET Core nel servizio app di Azure in Windows.

[Guida introduttiva: Creare un'app Web .NET Core nel Servizio app in Linux](/azure/app-service/containers/quickstart-dotnetcore)  
Usare la riga di comando per creare e distribuire un'app Web ASP.NET Core nel servizio app di Azure in Linux.

Gli articoli seguenti sono disponibili nella documentazione di ASP.NET Core:

<xref:tutorials/publish-to-azure-webapp-using-vs>  
Informazioni su come pubblicare un'app ASP.NET Core in Servizio app di Azure con Visual Studio.

<xref:host-and-deploy/azure-apps/azure-continuous-deployment>  
Informazioni su come creare un'app Web ASP.NET Core tramite Visual Studio e distribuirla nel Servizio app di Azure usando Git per la distribuzione continua.

[Creare la prima pipeline con Azure Pipelines](/azure/devops/pipelines/get-started-yaml)  
Impostare una build CI per un'app ASP.NET Core e quindi creare una versione di distribuzione continua in Servizio App di Azure.

[Azure Web App sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) (Sandbox per app Web di Azure)  
Individuare le limitazioni di esecuzione di runtime di Servizio app di Azure applicate dalla piattaforma per le app Azure.

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a>Configurazione dell'applicazione

I pacchetti NuGet seguenti offrono funzionalità di registrazione automatica per le app distribuite nel Servizio app di Azure:

* [Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) usa [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) per fornire l'integrazione di ASP.NET Core con il Servizio app di Azure. La funzionalità di registrazione aggiunte vengono fornite dal pacchetto `Microsoft.AspNetCore.AzureAppServicesIntegration`.
* [Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) esegue [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) per aggiungere i provider di registrazione diagnostica del servizio app di Azure nel pacchetto `Microsoft.Extensions.Logging.AzureAppServices`.
* [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) offre implementazioni di logger per il supporto dei registri di diagnostica del servizio app di Azure e delle funzionalità del flusso di registrazione.

Se destinati a .NET Core e aventi come riferimento il [metapacchetto Microsoft.AspNetCore.All](xref:fundamentals/metapackage), i pacchetti precedenti sono inclusi. I pacchetti non sono presenti nel [metapacchetto Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app). Se destinati a .NET Framework o aventi come riferimento il metapacchetto `Microsoft.AspNetCore.App`, fare riferimento ai singoli pacchetti di registrazione.

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a>Eseguire l'override della configurazione delle app usando il portale di Azure

L'area **Impostazioni app** del pannello **Impostazioni applicazione** consente di impostare le variabili di ambiente per l'app. Le variabili di ambiente possono essere utilizzate dal [provider di configurazione delle variabili di ambiente](xref:fundamentals/configuration/index#environment-variables-configuration-provider).

Quando nel portale di Azure viene creata o modificata un'impostazione dell'app e viene selezionato il pulsante **Salva**, l'app Azure viene riavviata. La variabile di ambiente risulterà disponibile per l'app dopo il riavvio del servizio.

Quando un'app usa l'[host Web](xref:fundamentals/host/web-host) e compila l'host con [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), le variabili di ambiente che consentono di configurare l'host usano il prefisso `ASPNETCORE_`. Per altre informazioni, vedere <xref:fundamentals/host/web-host> e il [provider di configurazione delle variabili di ambiente](xref:fundamentals/configuration/index#environment-variables-configuration-provider).

Quando un'app usa l'[host generico](xref:fundamentals/host/generic-host), le variabili di ambiente non vengono caricate nella configurazione di un'app per impostazione predefinita e il provider di configurazione deve essere aggiunto dallo sviluppatore. Lo sviluppatore determina il prefisso delle variabili di ambiente quando viene aggiunto il provider di configurazione. Per altre informazioni, vedere <xref:fundamentals/host/generic-host> e il [provider di configurazione delle variabili di ambiente](xref:fundamentals/configuration/index#environment-variables-configuration-provider).

## <a name="proxy-server-and-load-balancer-scenarios"></a>Scenari con server proxy e servizi di bilanciamento del carico

Il middleware di integrazione di IIS, che consente di configurare il middleware delle intestazioni inoltrate, e il modulo ASP.NET Core sono configurati per inoltrare lo schema (HTTP/HTTPS) e l'indirizzo IP remoto di origine della richiesta. Potrebbero essere necessari interventi di configurazione aggiuntivi per le app ospitate dietro ulteriori server proxy e servizi di bilanciamento del carico. Per altre informazioni, vedere [Configurare ASP.NET Core per l'utilizzo di server proxy e servizi di bilanciamento del carico](xref:host-and-deploy/proxy-load-balancer).

## <a name="monitoring-and-logging"></a>Monitoraggio e registrazione

Per informazioni sul monitoraggio, la registrazione e la risoluzione dei problemi, vedere gli articoli seguenti:

[Procedura: Eseguire il monitoraggio delle app nel servizio app di Azure](/azure/app-service/web-sites-monitor)  
Informazioni su come esaminare le quote e le metriche per le app e i piani del servizio app.

[Abilitare la registrazione diagnostica per le app Web nel servizio app di Azure](/azure/app-service/web-sites-enable-diagnostic-log)  
Informazioni su come abilitare e accedere alla registrazione diagnostica per i codici di stato HTTP, le richieste non riuscite e l'attività del server Web.

<xref:fundamentals/error-handling>  
Riconoscimento degli approcci comuni di gestione degli errori nelle app ASP.NET Core.

<xref:host-and-deploy/azure-apps/troubleshoot>  
Informazioni su come diagnosticare i problemi delle distribuzioni del servizio app di Azure con le app ASP.NET Core.

<xref:host-and-deploy/azure-iis-errors-reference>  
Informazioni sugli errori comuni di configurazione della distribuzione per le app ospitate dal servizio app di Azure o da IIS con suggerimenti per la risoluzione.

## <a name="data-protection-key-ring-and-deployment-slots"></a>KeyRing di protezione dati e slot di distribuzione

Le [chiavi di protezione dati](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) sono salvate in modo permanente nella cartella *%HOME%\ASP.NET\DataProtection-Keys*. La cartella è associata all'archiviazione di rete e sincronizzata in tutti i computer che ospitano l'app. Le chiavi non vengono protette quando sono inattive. La cartella offre il KeyRing a tutte le istanze di un'app in un singolo slot di distribuzione. Gli slot di distribuzione separati, ad esempio gli slot di gestione temporanea e di produzione, non condividono un KeyRing.

Nel passaggio da uno slot di distribuzione all'altro, tutti i sistemi che usano la protezione dati non saranno in grado di decrittografare i dati archiviati usando il KeyRing all'interno dello slot precedente. Il middleware dei cookie di ASP.NET usa la protezione dati per proteggere i cookie. Di conseguenza, gli utenti vengono disconnessi da un'app che usa il middleware dei cookie di ASP.NET standard. Per una soluzione di KeyRing indipendente dallo slot, usare un provider di KeyRing esterno, ad esempio:

* Archiviazione BLOB di Azure
* Azure Key Vault
* Archivio SQL
* Cache Redis

Per ulteriori informazioni, vedere <xref:security/data-protection/implementation/key-storage-providers>.

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a>Distribuire la versione di anteprima di ASP.NET Core in Servizio app di Azure

Adottare uno degli approcci seguenti:

* [Installare l'estensione del sito di anteprima](#install-the-preview-site-extension).
* [Distribuire l'app autonoma](#deploy-the-app-self-contained).
* [Usare Docker con app Web per contenitori](#use-docker-with-web-apps-for-containers).

### <a name="install-the-preview-site-extension"></a>Installare l'estensione del sito di anteprima

Se si verifica un problema con l'estensione del sito di anteprima, aprire un problema in [GitHub](https://github.com/aspnet/azureintegration/issues/new).

1. Dal portale di Azure passare al pannello Servizi App.
1. Selezionare l'app Web.
1. Digitare "ex" nella casella di ricerca o scorrere verso il basso l'elenco dei riquadri di gestione fino a **STRUMENTI DI LAVORO**.
1. Selezionare **STRUMENTI DI LAVORO** > **Extensions** (Estensioni).
1. Selezionare **Aggiungi**.
1. Selezionare l'estensione **ASP.NET Core &lt;x.y&gt; (x86) Runtime** dall'elenco, dove `<x.y>` è la versione di anteprima di ASP.NET Core (ad esempio, **ASP.NET Core 2.2 (x86) Runtime**). Il runtime x86 è consigliato per le [distribuzioni dipendenti dal framework](/dotnet/core/deploying/#framework-dependent-deployments-fdd) che si basano sull'hosting out-of-process dal modulo ASP.NET Core.
1. Selezionare **OK** per accettare le condizioni legali.
1. Per installare l'estensione, selezionare **OK**.

Al termine dell'operazione, viene installata l'anteprima più recente di .NET Core. Verificare l'installazione:

1. Selezionare **Strumenti avanzati** in **STRUMENTI DI LAVORO**.
1. Selezionare **Vai** nel pannello **Strumenti avanzati**.
1. Selezionare l'elemento di menu **Console di debug** > **PowerShell**.
1. Eseguire il comando seguente dal prompt di PowerShell. Sostituire la versione di runtime di ASP.NET Core per `<x.y>` nel comando:

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x86\
   ```
   Se il runtime dell'anteprima installata si applica ad ASP.NET Core 2.2, il comando è:
   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x86\
   ```
   Il comando restituisce `True` quando è installato il runtime di anteprima x64.

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> L'architettura della piattaforma (x86 o x64) di un'app di Servizi app è impostata nel pannello **Impostazioni applicazione** in **Impostazioni generali** per le app ospitate in un livello di hosting con calcolo di serie A o migliore. Se l'app viene eseguita in modalità in-process e l'architettura della piattaforma è configurata per 64 bit (x64), il modulo ASP.NET Core usa il runtime dell'anteprima a 64 bit, se presente. Installare l'estensione **ASP.NET Core &lt;x.y&gt; (x64) Runtime** (ad esempio, **ASP.NET Core 2.2 (x64) Runtime**).
>
> Dopo aver installato il runtime di anteprima x64, eseguire il comando seguente nella finestra di comando di PowerShell di Kudu per verificare l'installazione. Sostituire la versione di runtime di ASP.NET Core per `<x.y>` nel comando:
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x64\
> ```
> Se il runtime dell'anteprima installata si applica ad ASP.NET Core 2.2, il comando è:
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x64\
> ```
> Il comando restituisce `True` quando è installato il runtime di anteprima x64.

::: moniker-end

> [!NOTE]
> Le **estensioni di ASP.NET Core** abilitano funzionalità aggiuntive per ASP.NET Core nei Servizi app di Azure, ad esempio la registrazione di Azure. L'estensione viene installata automaticamente durante la distribuzione da Visual Studio. Se l'estensione non è installata, installarla per l'app.

**Usare l'estensione del sito di anteprima con un modello ARM**

Se per creare e distribuire le app si usa un modello ARM, è possibile usare il tipo di risorsa `siteextensions` per aggiungere l'estensione del sito a un'app Web. Ad esempio:

[!code-json[](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a>Distribuire l'app autonoma

Una [distribuzione autonoma](/dotnet/core/deploying/#self-contained-deployments-scd) che ha come destinazione un runtime di anteprima include il runtime di anteprima nella distribuzione.

Per la distribuzione di un'app autonoma:

* Il sito nel Servizio app di Azure non richiede l'[estensione del sito di anteprima](#install-the-preview-site-extension).
* L'app deve essere pubblicata seguendo un approccio diverso rispetto alla procedura di pubblicazione per una [distribuzione dipendente dal framework](/dotnet/core/deploying#framework-dependent-deployments-fdd).

#### <a name="publish-from-visual-studio"></a>Pubblicare da Visual Studio

1. Selezionare **Compila** > **Pubblica {nome applicazione}** sulla barra degli strumenti di Visual Studio.
1. Nella finestra di dialogo **Selezionare una destinazione di pubblicazione.** verificare che sia selezionata la voce **Servizio app**.
1. Selezionare **Avanzate**. Viene visualizzata la finestra di dialogo **Pubblica**.
1. Nella finestra di dialogo **Pubblica**:
   * Verificare che sia selezionata la configurazione **Rilascio**.
   * Aprire l'elenco a discesa **Modalità di distribuzione** e selezionare **Completa**.
   * Selezionare il runtime di destinazione dall'elenco a discesa **Runtime di destinazione**. Il valore predefinito è `win-x86`.
   * Se durante la distribuzione è necessario rimuovere i file aggiuntivi, aprire **Opzioni pubblicazione file** e selezionare la casella di controllo che consente di rimuovere i file aggiuntivi nella destinazione.
   * Selezionare **Salva**.
1. Creare un nuovo sito o aggiornare un sito esistente seguendo le istruzioni rimanenti della pubblicazione guidata.

#### <a name="publish-using-command-line-interface-cli-tools"></a>Pubblicare usando gli strumenti dell'interfaccia della riga di comando

1. Nel file di progetto specificare uno o più [identificatori di runtime (RID)](/dotnet/core/rid-catalog). Usare `<RuntimeIdentifier>` (singolare) per un unico RID o `<RuntimeIdentifiers>` (plurale) per specificare un elenco di RID delimitato da punto e virgola. Nell'esempio seguente è specificato il RID `win-x86`:

   ```xml
   <PropertyGroup>
     <TargetFramework>netcoreapp2.1</TargetFramework>
     <RuntimeIdentifier>win-x86</RuntimeIdentifier>
   </PropertyGroup>
   ```
1. Da una shell dei comandi eseguire il comando [dotnet publish](/dotnet/core/tools/dotnet-publish) per pubblicare l'app in configurazione Rilascio per il runtime dell'host. Nell'esempio seguente l'app viene pubblicata per il RID `win-x86`. Il RID fornito per l'opzione `--runtime` deve essere specificato nella proprietà `<RuntimeIdentifier>` (o `<RuntimeIdentifiers>`) del file di progetto.

   ```console
   dotnet publish --configuration Release --runtime win-x86
   ```
1. Spostare il contenuto della directory *bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* nel sito del Servizio app.

### <a name="use-docker-with-web-apps-for-containers"></a>Usare Docker con app Web per contenitori

L'[hub Docker](https://hub.docker.com/r/microsoft/aspnetcore/) contiene le immagini di Docker più recenti per la versione di anteprima. Le immagini possono essere usate come immagini di base. Usare l'immagine e distribuirla alle app Web per i contenitori normalmente.

## <a name="protocol-settings-https"></a>Impostazioni del protocollo (HTTPS)

Le associazioni di protocollo protette consentono di specificare un certificato da usare per rispondere alle richieste su HTTPS. L'associazione richiede un certificato privato valido (*PFX*) rilasciato per il nome host specifico. Per altre informazioni, vedere [Esercitazione: Associare un certificato SSL personalizzato esistente ad app Web di Azure](/azure/app-service/app-service-web-tutorial-custom-ssl).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Panoramica di App Web (video di 5 minuti)](/azure/app-service/app-service-web-overview)
* [Azure App Service: The Best Place to Host your .NET Apps ](https://channel9.msdn.com/events/dotnetConf/2017/T222) (Servizio app di Azure: la soluzione migliore per l'hosting delle app .NET) (video di 55 minuti)
* [Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience) (Azure Friday: diagnostica e risoluzione dei problemi del servizio app di Azure) (video di 12 minuti)
* [Panoramica della diagnostica del servizio app di Azure](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

Il servizio app di Azure in Windows Server usa [Internet Information Services (IIS)](https://www.iis.net/). Gli argomenti seguenti riguardano la tecnologia IIS sottostante:

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [Libreria di Microsoft TechNet: Windows Server](/windows-server/windows-server-versions)
