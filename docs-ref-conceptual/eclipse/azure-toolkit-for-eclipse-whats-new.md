---
title: Novidades no Kit de Ferramentas do Azure para Eclipse
description: Saiba mais sobre os recursos mais recentes do Kit de Ferramentas do Azure para Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: ed21f4308b2f6e45f022608a2ba32fe7db6922d3
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Novidades no Kit de Ferramentas do Azure para Eclipse

## <a name="azure-toolkit-for-eclipse-releases"></a>Versões do Kit de Ferramentas do Azure para Eclipse
Este artigo contém informações sobre as várias versões e atualizações mais recentes do Kit de Ferramentas do Azure para Eclipse.

> [!NOTE]
> Confira a seguinte página da Web para obter as informações mais recentes:
> 
> <https://github.com/Microsoft/azure-tools-for-java/releases>

> [!NOTE]
> Há também um kit de ferramentas do Azure para o IDE do IntelliJ. Para obter mais informações, confira [Kit de Ferramentas do Azure para IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14 de abril de 2017
O Kit de Ferramentas do Azure para Eclipse, versão de abril de 2017, inclui as seguintes melhorias:

* **Experiência aprimorada de entrada no Azure**: o Kit de Ferramentas do Azure para Eclipse agora dá suporte a dois métodos para fazer logon em sua conta do Azure: *Interativo* e *Automatizado*. Para obter mais informações, consulte [Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse].
* **Publicando usando contêineres do Docker**: agora você pode publicar seus aplicativos Web como contêineres do Docker usando o Kit de ferramentas do Azure para Eclipse. Para obter mais informações, consulte [Como publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse].
* **Gerenciamento de Conta de Armazenamento**: o Kit de ferramentas do Azure para Eclipse agora dá suporte ao gerenciamento de suas contas de armazenamento na Exibição do Azure Explorer. Para obter mais informações, consulte [Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse].
* **Gerenciamento de Máquina Virtual**: o Kit de ferramentas do Azure para Eclipse agora dá suporte ao gerenciamento de suas máquinas virtuais na Exibição do Azure Explorer. Para obter mais informações, consulte [Gerenciar Máquinas Virtuais usando o Azure Explorer para Eclipse].
* **Remoção de suporte a depuração remota**. A depuração remota de aplicativos Web Java no Serviço de Aplicativo do Azure foi removida do Kit de ferramentas do Azure para Eclipse; isso foi necessário para resolver alguns problemas que os clientes estavam tendo ao usar o Kit de ferramentas.

### <a name="august-26-2016"></a>26 de agosto de 2016
O Kit de Ferramentas do Azure para Eclipse, versão de agosto de 2016, inclui os seguintes aprimoramentos:

* **Distribuições personalizadas do JDK**. Agora, o Kit de Ferramentas do Azure para Eclipse oferece suporte à especificação e à implantação de uma versão do JDK arbitrária para o contêiner WebApp do Azure:
  * Além dos JDKs fornecidos pelo Azure, também é possível escolher dentre uma ampla seleção de versões do Zulu OpenJDK disponibilizadas no Azure pelo Azul Systems.
  * Você também pode especificar sua própria distribuição JDK se carregar um arquivo ZIP em sua conta de armazenamento.
* **Aprimoramentos no modo de exibição do Azure Explorer**:
  * Suporte para gerenciamento de máquinas virtuais usando o novo modelo de Resource Manager do Azure: você pode listar, criar e excluir máquinas virtuais baseadas no resource manager sem sair do IDE.
  * Suporte para gerenciamento de blobs da Conta de armazenamento usando o Resource Manager do Azure, que complementa a funcionalidade existente para gerenciar contas de armazenamento "clássico".
* **Microsoft JDBC Driver 6.0 para SQL Server**. Esta atualização inclui o driver JDBC do Microsoft SQL Server (v 6.0), que é agora incluído como uma biblioteca que você pode adicionar facilmente aos seus projetos Java, substituindo a versão mais antiga.

### <a name="june-29-2016"></a>29 de junho de 2016
O Kit de Ferramentas do Azure para Eclipse, versão de junho de 2016, inclui os seguintes aprimoramentos:

* **Requisito do Java 8**. O Kit de ferramentas do Azure para Eclipse agora exige o Java 8, embora esse requisito seja somente para o kit de ferramentas - seus aplicativos podem continuar a usar todas as versões do Java com suporte do Azure.
* **Suporte para os JDKs do Java mais recentes**. Agora há suporte para as versões mais recentes de JDKs do Java pelo Kit de Ferramentas do Azure para Eclipse.
* **Suporte para o SDK do Azure v2.9.1**. A versão mais recente do SDK do Azure agora é o pré-requisito mínimo para o Kit de Ferramentas do Azure para Eclipse.
* **Exemplos Integrados**. O Kit de Ferramentas do Azure para Eclipse agora apresenta vários aplicativos de exemplo para ajudar os desenvolvedores a começar.
* **Integração de Ferramentas HDInsight**. As Ferramentas de HDInsight do Azure agora estão incluídas no Kit de Ferramentas do Azure para Eclipse. Para saber mais, confira [Plug-in das Ferramentas do HDInsight para Eclipse].
* **Depuração remota de aplicativos Web do Java**. O Kit de Ferramentas do Azure para Eclipse agora dá suporte a depuração remota de aplicativos Web do Java no Serviço de Aplicativo do Azure.
* **Suporte para a versão Luna do Eclipse.** A nova versão mínima exigida pelo IDE do Eclipse é a Luna.

### <a name="april-12-2016"></a>12 de abril de 2016
O Kit de Ferramentas do Azure para Eclipse, versão de abril de 2016, inclui as seguintes melhorias:

* **Suporte para o SDK do Azure v2.9.0**. A versão mais recente do SDK do Azure agora é o pré-requisito mínimo para o Kit de Ferramentas do Azure para Eclipse.
* **Diversas melhorias de usabilidade, capacidade de resposta e desempenho relacionadas ao suporte do aplicativo Web do Azure**. Uma série de otimizações de desempenho na forma como o Kit de Ferramentas se comunica com o Azure resulta em uma interface do usuário mais dinâmica.
* **Capacidade de excluir um contêiner do aplicativo Web existente no Azure por meio do Eclipse**. O Kit de Ferramentas do Azure para Eclipse agora permite a exclusão de um contêiner da Web existente do Azure sem a necessidade de sair do Eclipse.

### <a name="march-7-2016"></a>7 de março de 2016
O Kit de Ferramentas do Azure para Eclipse, versão de março de 2016, inclui os seguintes aprimoramentos:

* **Suporte para implantação rápida de aplicativos Java leves**. O Kit de Ferramentas do Azure para Eclipse agora dá suporte à implantação rápida de aplicativos Java leves em contêineres de aplicativos Web do Azure, por isso, implantar aplicativos Java agora leva apenas segundos em vez de minutos.
* **Suporte para gerenciamento de aplicativo Web usando a exibição do Azure Explorer**. A exibição do Azure Explorer no Kit de Ferramentas agora dá suporte para listar, iniciar e interromper aplicativos Web do Azure.
* **Distribuições atualizadas Tomcat, Jetty e Zulu OpenJDK**. O Kit de Ferramentas do Azure para Eclipse dá suporte para versões atualizadas do Tomcat, Jetty e Zulu OpenJDK para implantações de Java em serviços de nuvem do Azure.

### <a name="january-4-2016"></a>4 de janeiro de 2016
O Kit de Ferramentas do Azure para Eclipse, versão de janeiro de 2016, inclui os seguintes aprimoramentos:

* **Suporte para as atualizações do Zulu OpenJDK**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Distribuições do Tomcat e Jetty atualizadas**. As distribuições do Jetty e Tomcat, disponíveis no Microsoft Azure para uso com o Kit de Ferramentas do Azure para Eclipse, foram atualizadas.
* **Paridade de Recursos entre os Kits de Ferramentas para o Eclipse e para o IntelliJ do Azure**. O Kit de Ferramentas do Azure para o Eclipse e o [Kit de Ferramentas do Azure para IntelliJ] agora dão suporte ao mesmo conjunto de recursos.

### <a name="september-1-2015"></a>1º de setembro de 2015
O Kit de Ferramentas do Azure para Eclipse, versão de setembro de 2015, inclui os seguintes aprimoramentos:

* **Suporte para as atualizações do Zulu OpenJDK**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Distribuições do Tomcat e Jetty atualizadas**. As distribuições do Jetty e Tomcat, disponíveis no Microsoft Azure para uso com o Kit de Ferramentas do Azure para Eclipse, foram atualizadas. (Essas distribuições permitem aos desenvolvedores criar projetos rápidos de desenvolvimento e teste com o Kit de Ferramentas do Azure para Eclipse.
* **Suporte para referências automaticamente atualizadas do Tomcat e Jetty**. Além das versões específicas do Tomcat e do Jetty que estão disponíveis no Azure, agora os desenvolvedores podem fazer referencia a uma distribuição conhecida como a "Mais recente (atualização automática)", que será atualizada automaticamente para a distribuição mais recente de cada versão principal do Jetty ou do Tomcat na próxima vez que as instâncias de função forem recicladas. (A reciclagem ocorre automaticamente, mas os desenvolvedores podem dispará-la manualmente pelo Portal do Azure.) Esse novo recurso significa que os desenvolvedores não precisam reimplantar seus aplicativos para atualizarem o software do servidor. (
* Atualmente, essa funcionalidade é destinada apenas para fins de desenvolvimento e teste ou para aplicativos não essenciais, e não é recomendada para produção.)
* **Exibição do Azure Explorer para blobs, filas e tabelas no armazenamento do Azure**. Isso permite que os desenvolvedores realizem um conjunto de tarefas comuns com seus artefatos de armazenamento diretamente do IDE do Eclipse. Por exemplo: excluir, carregar ou baixar blobs.

### <a name="august-1-2015"></a>1º de agosto de 2015
O Kit de Ferramentas do Azure para Eclipse, versão de agosto de 2015, inclui os seguintes aprimoramentos:

* **Gerenciamento de chave de instrumentação do Application Insights**. Esta atualização permite que você adquira, crie e gerencie suas chaves de instrumentação do Application Insights diretamente do IDE do Eclipse.
* **Microsoft JDBC Driver 4.1 para SQL Server**. Esta atualização inclui suporte para o driver JDBC mais recente do Microsoft SQL Server.
* **Versão 2.7 do SDK do Azure**. Esta atualização mais recente para o SDK do Azure é o novo pré-requisito para o Kit de Ferramentas, quando é instalado no Windows. (Observe que isso não é necessário em sistemas operacionais diferente do Windows).
* **Suporte para a atualização do Zulu OpenJDK v7**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].

### <a name="may-1-2015"></a>1º de maio de 2015
O Kit de Ferramentas do Azure para Eclipse, versão de maio de 2015, inclui os seguintes aprimoramentos:

* **Interface de usuário aprimorada para seleção de servidor**. Esta versão simplifica o uso do kit de ferramentas em sistemas operacionais diferentes do Windows.
* **Suporte para projetos Maven**. Esta versão oferece suporte a projetos Maven como aplicativos, que o kit de ferramentas no Azure pode implantar e configurar o Application Insights.
* **Versão 2.6 do SDK do Azure**. Esta atualização mais recente para o SDK do Azure é o novo pré-requisito para o Kit de Ferramentas, quando é instalado no Windows. (Observe que isso não é necessário em sistemas operacionais diferente do Windows).
* **Atualização da implantação em vez de republicar**. Se você estiver republicando um projeto de implantação com a versão anterior já ativa, você poderá usar o kit de ferramenta que agora usa a funcionalidade de atualização de implantação do Azure em vez de desligar a implantação anterior e republicar do zero, como era feito no passado. Isso permite que seu serviço de nuvem seja executado sem interrupção sempre que possível, ajudando a alcançar alta disponibilidade até mesmo durante uma atualização e a acelerar o processo de republicação.
* **Suporte para o Zulu OpenJDK v8 mais recente - atualização 40**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].

### <a name="march-9-2015"></a>9 de março de 2015
O Kit de Ferramentas do Azure para Eclipse, versão de março de 2015, inclui os seguintes aprimoramentos:

* **Suporte para Mac, Ubuntu e tipos adicionais de Linux**. Esta versão do Kit de Ferramentas do Azure para Eclipse acrescenta suporte para Mac OS e várias plataformas Unix, para que os desenvolvedores possam instalar o kit de ferramentas e criar, configurar e publicar projetos Java nos Serviços de Nuvem do Azure (PaaS) do Eclipse em execução em sistemas operacionais diferentes do Windows.

> [!NOTE]
> Esse recurso está no modo de visualização e não é recomendado para uso em ambientes de produção. Não há SLA (Contrato de nível de serviço) para suporte ao cliente, mas todos os comentários são bem-vindos e incentivados.
> 
> 

* **Novo plug-in do Application Insights**. Agora, os desenvolvedores podem configurar a telemetria automática de servidor usando o Application Insights no Azure.
* **Automação de implantação de linha de comando baseada em Ant**. Esse recurso permite aos desenvolvedores automatizar a publicação de versões mais recentes de suas implantações usando o Ant fora do Eclipse. Um script pré-gerado é configurado automaticamente para um projeto após sua primeira implantação a partir do Eclipse, e as implantações subsequentes podem usar o script para automatizar totalmente as implantações somente pela linha de comando.
* **Disponibilidade do Tomcat e do Jetty no Azure para implantação mais simples e rápidas**. Agora, os desenvolvedores podem fazer referência direta a várias versões do Tomcat e do Jetty disponíveis no Azure, em vez de precisarem carregar um servidor Java em suas contas (ou pelo Kit de ferramentas), portanto, não é necessário carregar um servidor Java para cenários iniciais rápidos.
* **Método de atalho para publicar aplicativos web Java nos serviços de nuvem do Azure**. Para reduzir a curva de aprendizado para cenários simples de teste e desenvolvimento, agora os desenvolvedores podem publicar aplicativos Java diretamente no Azure. Em vez de ter que passar por todo o processo de criação e configuração de um projeto de implantação do Azure, os aplicativos serão implantados com uma instância padrão do Tomcat v8 e do Zulu JVM (OpenJDK).

### <a name="january-30-2015"></a>30 de janeiro de 2015
O Kit de Ferramentas do Azure para Eclipse, versão de janeiro de 2015, inclui os seguintes aprimoramentos:

* **Suporte para IBM® WebSphere® Application Server Liberty Core**. Essa versão adiciona o IBM WebSphere Application Server Liberty Core à lista de servidores de aplicativos com suporte a partir dos quais o Kit de ferramentas é capaz de implantar no Azure. Esta adição mais recente expande a lista atual de servidores de aplicativos que têm suporte &quot;nativo&quot; do Kit de ferramentas, que já inclui várias versões do Tomcat, Jetty, JBoss e GlassFish.
* **Inclusão do SDK do Application Insights**. Essa biblioteca de API do cliente lançada recentemente (v0.9.0) agora faz parte do Pacote para Bibliotecas do Azure para Java.
* **Pacote atualizado para Bibliotecas do Azure para Java**. Esta atualização inclui Bibliotecas do Azure para Java v0.7.0 e API do Cliente de Armazenamento v2.0.0, bem como o SDK do Application Insights v0.9.0 lançado recentemente.

### <a name="november-12-2014"></a>12 de novembro de 2014
O Kit de Ferramentas do Azure para Eclipse, versão de novembro de 2014, inclui os seguintes aprimoramentos:

* **Suporte para o SDK do Azure 2.5**. Esta atualização mais recente para o SDK do Azure é o novo pré-requisito para o Kit de Ferramentas.
* **Suporte para a versão atualizada dos pacotes Zulu OpenJDK v1.8, v1.7 e v1.6**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Suporte para os novos tamanhos Standard D de serviços de nuvem**, que oferecem mais desempenho e recursos de memória. Para obter mais informações, veja [Tamanhos de máquina virtual e serviço de nuvem para o Azure].

### <a name="october-17-2014"></a>17 de outubro de 2014
O Kit de Ferramentas do Azure para Eclipse, versão de outubro de 2014, inclui os seguintes aprimoramentos:

* **Aprimoramentos de desempenho nos cenários de Publicação na nuvem**. O carregamento de informações de assinatura é muito mais rápido quando os usuários têm várias assinaturas e contas de armazenamento.
* **Suporte para a versão atualizada do pacote Zulu OpenJDK v1.8**. Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Suporte para versões mais antigas e obsoletas de JDKs de terceiros**. Os pacotes de JDK obsoletos não aparecerão mais no menu suspenso dos novos projetos de implantação. Os projetos existentes que fazem referência a pacotes JDK obsoletos ainda poderão fazer isso no momento, mas recomendamos a atualização desses projetos para que dependam da versão mais recente.
* **Versão atualizada do pacote de Bibliotecas do Azure para a biblioteca de APIs de cliente Java**. Para saber mais, confira a [API de cliente do Microsoft Azure].
* **Correções de bug.** Esta versão contém diversas correções de bugs baseadas em relatórios e testes de usuários.

### <a name="august-5-2014"></a>5 de agosto de 2014
O Kit de Ferramentas do Azure para Eclipse, versão de agosto de 2014, inclui os seguintes aprimoramentos

* **Suporte para o SDK do Azure 2.4.** Versões mais antigas do Kit de Ferramentas do Eclipse não funcionarão com esse SDK recém-lançado.
* **Versões atualizadas dos pacotes Zulu OpenJDK v1.6, 1.7 e v1.8..** Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Versão atualizada do pacote de Bibliotecas do Azure para a biblioteca de APIs de cliente Java.** Para saber mais, confira a [API de cliente do Microsoft Azure].
* **Suporte para o formato de arquivo de configurações de publicação mais recente.** Adição do suporte para a versão 2.0 do formato do arquivo de Configurações de publicação.
* **Alterações de arquitetura por trás do recurso Publicar na nuvem.** Agora, o Kit de Ferramentas está usando a recém-lançada API de cliente do Microsoft Azure para Java para seu suporte de publicação na nuvem.
* **Correções de bug.** Esta versão contém várias correções de bugs solicitadas pelo usuário.

### <a name="june-12-2014"></a>12 de junho de 2014
O Kit de Ferramentas do Azure para Eclipse, versão de junho de 2014, é uma pequena atualização de serviço que fornece os seguintes aprimoramentos:

* **Suporte para o pacote do Zulu OpenJDK v1.8.** Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Versões atualizadas dos pacotes Zulu OpenJDK v1.6 e 1.7..** Para saber mais, consulte a [página da Web do Azul Systems para o Zulu OpenJDK].
* **Versão atualizada do pacote de Bibliotecas do Azure para a biblioteca de APIs de cliente Java.** Para saber mais, confira a [API de cliente do Microsoft Azure].
* **Correções de bug.** Esta versão contém várias correções de bugs solicitadas pelo usuário.

### <a name="april-4-2014"></a>4 de abril de 2014
O plug-in do Azure para Eclipse, versão de abril de 2014, foi lançado. Esta é uma atualização que acompanha a versão do SDK 2.3 do Azure, que é um pré-requisito, e será baixada automaticamente quando você instalar o plug-in. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de fevereiro de 2014:

* **Suporte para a versão 2.3 do SDK do Azure.** O Plug-in do Azure para Eclipse, versão de abril de 2014, exige o SDK 2.3 do Azure. Ao usar o novo plug-in, se você ainda não tiver o SDK 2.3 do Azure, você receberá uma solicitação para permitir sua instalação. Não use o SDK 2.3 do Azure com versões anteriores do plug-in.
* **Atualização de aplicativos sem a implantação completa do pacote.** Agora, ao implantar aplicativos Java que fazem parte de seu projeto, o plug-in os carrega automaticamente em sua conta de armazenamento selecionada para que você possa atualizá-la e reciclar as instâncias de função a fim de implantar os bits de aplicativo mais recentes sem precisar recompilar e reimplantar todo o pacote.
* **Agora, o Tomcat 8 é um servidor de aplicativos reconhecido.** Se você selecionar um diretório de instalação do Tomcat 8 em seu computador na guia **Servidor** da caixa de diálogo **Projeto de Implantação do Azure**, o plug-in o detectará automaticamente e será capaz de implantar o Tomcat 8 de modo automatizado, semelhante às versões mais antigas do Tomcat que já estão na lista.
* **Atualizações do pacote do Azul Zulu OpenJDK: atualização 51 da v1.7 e atualização 47 da v1.6.** A partir desta versão, atualização de pacote 51 do Zulu Open JDK v7 do Azul System está disponível. Além disso, os pacotes do Zulu Open JDK v6 estão começando a ficar disponíveis, começando com a atualização 47. Essas atualizações são acréscimos às atualizações 45, 40 e 25 disponíveis do pacote Zulu Open JDK v7.
* **Suporte para tamanhos A8 e A9 de máquina virtual do Microsoft Azure.** Agora você pode implantar um serviço de nuvem no tamanho de máquina virtual A8 e A9 de memória alta. Para saber mais sobre tamanhos de VM, confira [Tamanhos de máquina virtual e serviço de nuvem para o Azure].
* **Redirecionamento automático de HTTP para HTTPS para funções habilitadas para SSL.** Quando o serviço de nuvem contiver somente funções HTTPS, se a solicitação do usuário especificar HTTP, ele será automaticamente redirecionado para HTTPS. Não é necessário criar uma função separada para manipular as solicitações HTTP.
* **Emulador Express usado para a emulação local.** O Emulador Express do Azure agora é usado como emulador ao depurar seus aplicativos localmente.
* **O Azure foi rebatizado como Microsoft Azure.** As telas de interface do usuário agora refletem que o Azure foi rebatizado e não é mais chamado de Azure.

### <a name="february-6-2014"></a>6 de fevereiro 2014
Plug-in do Azure para Eclipse, versão de Visualização de fevereiro de 2014, foi lançado. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de outubro de 2013:

* **Suporte para o descarregamento de SSL.** O descarregamento de SSL (Secure Sockets Layer) foi adicionado como um recurso, permitindo o suporte ao protocolo HTTPS (Hypertext Transfer Protocol Secure) em sua implantação Java no Azure, sem a necessidade de configurar SSL em seu servidor de aplicativo Java. Isso é particularmente relevante em cenários de afinidade de sessão e/ou comunicação autenticada. Por exemplo, ao usar o Filtro ACS (Serviço de Controle de Acesso), que já recebe suporte do kit de ferramentas. Para saber mais, confira [Descarregamento de SSL] e [Como usar o descarregamento de SSL].
* **Agora, o GlassFish 4 é um servidor de aplicativos reconhecido.** Se você selecionar um diretório de instalação do GlassFish 4 em seu computador na guia **Servidor** da caixa de diálogo **Projeto de Implantação do Azure**, o plug-in o detectará automaticamente e será capaz de implantar o GlassFish OSE 4 de modo automatizado, semelhante à versão OSE 3 do GlassFish que já está na lista.
* **Atualização de pacote 45 do Azul Zulu OpenJDK.** A partir desta versão, a atualização 45 do Zulu (pacote Open JDK v7) do Azul System está disponível. Esse é um acréscimo às atualizações 40 e 25 disponíveis anteriormente.
* **Suporte para “automática” para portas de ponto de extremidade privadas.** Você pode definir uma porta privada como automática para pontos de extremidade de entrada e pontos de extremidade internos a fim de permitir que o Azure atribua automaticamente uma porta a esse ponto de extremidade. Anteriormente, era possível atribuir apenas um número de porta específico.
* **Suporte para personalização do nome do certificado (CN) na interface de usuário de criação de certificado autoassinado.** Anteriormente, o mesmo nome codificado era usado para todos os novos certificados; agora, você pode especificar seu próprio nome de certificado para ajudar a distinguir vários certificados no Portal do Azure usados para finalidades diferentes.
* **Barra de ferramentas do azure:** a barra de ferramentas do Azure foi atualizada com as seguintes alterações: 
  * ![][ic710876] Este ícone foi adicionado ao **Novo projeto de implantação do Azure**.
  * ![][ic710877] Este ícone foi adicionado como um atalho para a caixa de diálogo de criação de certificado autoassinado.
* **Suporte para tamanho A5 de máquina virtual do Azure.** Agora você pode implantar um serviço de nuvem no tamanho da máquina virtual A5 de memória alta. Para saber mais sobre esse tamanho de VM, confira [Tamanhos de máquina virtual e serviço de nuvem para o Azure].
* **Suporte para Microsoft Windows Server 2012 R2.** Agora, você pode selecionar o Windows Server 2012 R2 como o sistema operacional em nuvem.

### <a name="october-22-2013"></a>22 de outubro de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de outubro de 2013, foi lançado. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de setembro de 2013:

* **Suporte para a versão 2.2 do SDK do Azure.** O Plug-in do Azure para Eclipse, versão de Visualização de outubro de 2013, oferece suporte ao SDK 2.2 do Azure. O plug-in ainda funcionará com o SDK 2.1 do Azure e instalará automaticamente o SDK 2.2 do Azure se você ainda não tiver pelo menos o SDK 2.1 do Azure instalado.
* **Atualização de pacote 40 do Azul Zulu OpenJDK.** Conforme anunciado na versão de Visualização de setembro de 2013, o plug-in agora permite o uso de um JDK fornecido por terceiros diretamente no Azure, sem a necessidade de carregar seu próprio JDK. Na versão de outubro de 2013, a atualização 40 do Zulu (pacote Open JDK v7) do Azul System está disponível. Esse é um acréscimo à atualização 25 publicada originalmente.
* **Link de implantação em nuvem no Log de atividades.** Quando sua implantação apresenta um status de **Publicada** no Log de atividades do Azure, você pode clicar em **Publicada**, que agora é um link para sua implantação, e abri-la em seu navegador. (Antes, o status de **Publicada** era rotulado **Executando**.)
* **Seleção do sistema operacional de destino disponível no momento da publicação.** A caixa de diálogo **Publicar no Azure** contém um novo campo, **SO de Destino**, que fornece uma maneira mais detectável de definição de seu sistema operacional de destino.
* **Substituir automaticamente a implantação anterior.** A caixa de diálogo **Publicar no Azure** contém uma nova caixa de seleção, **Substituir implantação anterior**. Se esta opção estiver marcada, quando a nova implantação for publicada ela substituirá automaticamente a implantação anterior; você não enfrentará problemas de &quot;409 conflict&quot; ao publicar no mesmo local sem antes cancelar a publicação da implantação anterior.
* **Agora, o Jetty 9 é um servidor de aplicativos reconhecido.** Se você selecionar um diretório de instalação do Jetty 9 em seu computador na guia **Servidor** da caixa de diálogo **Projeto de Implantação do Azure**, o plug-in o detectará automaticamente e será capaz de implantar o Jetty 9 de modo automatizado, semelhante às versões do Jetty que já estão na lista.
* **Adicionar uma função no menu de contexto do projeto.** Agora, o menu de contexto do projeto **Azure** contém um novo item de menu, **Adicionar Função**, que fornece uma maneira mais rápida e detectável para adicionar uma nova função ao seu projeto do Azure.
* **Uma atualização ao pacote para as Bibliotecas do Azure para a biblioteca Java.** Isso tem base na versão 0.4.6 da [API de cliente do Microsoft Azure].

### <a name="september-25-2013"></a>25 de setembro de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de setembro de 2013, foi lançado. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de agosto de 2013:

* **Capacidade de implantar o pacote Azul Zulu OpenJDK disponível no Azure.** Uma nova opção foi adicionada ao especificar o JDK a ser usado com sua implantação do Azure. Com essa opção, você pode implantar um pacote JDK de terceiros diretamente na nuvem do Azure, sem a necessidade de carregar o seu próprio. O Azul Systems está fornecendo o primeiro pacote desse tipo, chamado Zulu, com base em OpenJDK, que agora pode ser implantado usando essa opção.
* **Uma atualização ao pacote para as Bibliotecas do Azure para a biblioteca Java.** Isso tem base na versão 0.4.5 da [API de cliente do Microsoft Azure].

### <a name="august-1-2013"></a>1º de agosto de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de agosto de 2013, foi lançado. Esta é uma atualização que acompanha a versão do SDK 2.1 do Azure, que é um pré-requisito, e será baixada automaticamente quando você instalar o plug-in. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de julho de 2013:

* **Remoção de opções para incluir o JDK local e o servidor de aplicativos local como parte do pacote de implantação.** É preferível baixar o JDK e o servidor de aplicativos do armazenamento em nuvem durante a implantação a fim de incorporar esses componentes no pacote, pois o download dos itens resulta em um pacote de implantação menor, mais rapidez na implantação e facilidade de manutenção. Como resultado, as opções para incluir o JDK e o servidor de aplicativos no pacote de implantação foram removidas. Projetos existentes que foram configurados para incluir o JDK local e o servidor de aplicativos local como parte do pacote de implantação serão automaticamente convertidos a fim de carregarem automaticamente o JDK e o servidor de aplicativos para armazenamento em nuvem.
* **Suporte para a versão 2.1 do SDK do Azure.** O Plug-in do Azure para Eclipse, versão de Visualização de agosto de 2013 exige o SDK 2.1 do Azure. Não use a visualização de agosto de 2013 com versões anteriores do SDK do Azure, e não usar o SDK 2.1 do Azure com versões anteriores do Plug-in do Azure para Eclipse.
* **Suporte para a versão Kepler do Eclipse.** Com relação a isso, a nova versão mínima exigida pelo IDE do Eclipse é a Indigo. O Plug-in do Azure para Eclipse não é mais oficialmente testado em Helios.

### <a name="july-3-2013"></a>3 de julho de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de julho de 2013, foi lançado. Esta atualização inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de maio de 2013:

* **Capacidade para criar uma nova conta de armazenamento.** Um botão **Novo** foi adicionado à caixa de diálogo **Adicionar Conta de Armazenamento**. Isso permite que você crie uma conta de armazenamento dentro do plug-in do Eclipse, sem exigir o logon no Portal de Gerenciamento do Azure. (Você já deve ter uma assinatura do Azure para usar esse recurso.) Para saber mais sobre como criar uma nova conta de armazenamento, confira [Para criar uma nova conta de armazenamento].
* **Nova opção &quot;(automática)&quot; para conta de armazenamento usada para a implantação automática do JDK e do servidor, e para caching.** Ao usar a opção **Carregar automaticamente** para o JDK e servidor de aplicativos, é possível especificar o uso da opção **(automática)** na URL e na conta de armazenamento ao carregar o JDK e o servidor de aplicativos, ou ao usar o Caching do Azure. Assim, esses recursos utilizarão automaticamente a mesma conta de armazenamento que você seleciona na caixa de diálogo **Publicar no Azure** . O tutorial [Criação de um aplicativo Hello World do Azure no Eclipse] foi atualizada para usar a nova opção **(automática)** .
* **Capacidade de definir os pontos de extremidade de serviço do Azure.** Especifique os pontos de extremidade de serviço que determinam se o aplicativo será implantado e gerenciado pela plataforma global do Azure, operado pelo Azure pela 21Vianet na China ou por uma plataforma privada do Azure. Para saber mais, confira [Ponto de extremidade de serviço do Azure].
* **Implantações de grande porte podem especificar um recurso de armazenamento local.** Agora, caso sua implantação seja muito grande para caber na pasta approot padrão, você pode especificar um recurso de armazenamento local como o destino de implantação para seu JDK e servidor de aplicativos. Para saber mais, confira [Implantações de grande porte].
* **Suporte para tamanhos A6 e A7 de máquina virtual do Azure.** Agora você pode implantar um serviço de nuvem no tamanho de máquina virtual A6 e A7 de memória alta. Para saber mais sobre esses tamanhos, confira [Tamanhos de máquina virtual e serviço de nuvem para o Azure].
* **Uma atualização ao pacote para as Bibliotecas do Azure para a biblioteca Java.** Isso tem base na versão 0.4.4 da [API de cliente do Microsoft Azure].

### <a name="may-1-2013"></a>1º de maio de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de maio de 2013, foi lançado. Esta é uma atualização importante que acompanha a versão do SDK 2.0 do Azure, que é um pré-requisito, e será baixada automaticamente quando você instalar o plug-in. Esta versão inclui novos recursos, correções de bugs e alguns aprimoramentos de uso gerados por comentários desde a versão de Visualização de fevereiro de 2013:

* **Carregamento automático do JDK e do servidor de aplicativos no Azure e implantação a partir do Azure.** Uma nova opção que carrega automaticamente, quando necessário, o JDK e o servidor de aplicativos selecionados em uma conta de armazenamento do Azure especificada, e implanta esses componentes a partir dessa conta, em vez de incorporá-los no pacote de implantação ou exigir que o usuário os carreguem manualmente. Esse recurso normalmente solicitados podem melhorar bastante a facilidade de implantação dos componentes de servidor e do JDK, especialmente para usuários menos experientes. Para obter uma orientação que usa essas opções, confira [Criação de um aplicativo Hello World do Azure no Eclipse].
* **Controle centralizado de conta de armazenamento e capacidade de fazer referência às contas de armazenamento com mais facilidade (por meio de um controle suspenso).** Isso se aplica a vários recursos que dependem do armazenamento, como a implantação do JDK e de componentes do servidor, e caching. Para saber mais, confira [Lista de contas de armazenamento do Azure].
* **Configuração simplificada do Acesso Remoto no assistente Publicar na Nuvem.** Basta digitar um nome de usuário e senha para habilitar o acesso remoto, ou deixar em branco para manter o acesso remoto desabilitado.
* **Uma atualização ao pacote para as Bibliotecas do Azure para a biblioteca Java.** Isso tem base na versão 0.4.2 da [API de cliente do Microsoft Azure].
* **Suporte a sessões temporárias no Windows Server 2012.** Anteriormente, as sessões temporárias funcionavam apenas no Windows Server 2008 R2. Agora, os dois destinos de sistema operacionais em nuvem oferecem suporte à afinidade de sessão.
* **Aprimoramentos de desempenho de carregamento do pacote.** Mesmo quando o JDK e o servidor de aplicativos são incorporados ao pacote de implantação, a parte de carregamento do processo de implantação pode ser quase duas vezes mais rápida quando comparado com versões anteriores.

### <a name="february-8-2013"></a>8 de fevereiro de 2013
O Plug-in do Azure para Eclipse, versão de Visualização de fevereiro de 2013, foi lançado. Esta é uma atualização secundária que inclui correções de bugs, aprimoramentos de uso gerados por comentários e alguns recursos novos desde a versão de Visualização de novembro de 2012:

* Suporte para implantação de JDKs, servidores de aplicativos e outros componentes aleatórios de downloads de armazenamento de blobs público ou privado do Azure em vez de incluí-los no pacote de implantação ao implantar na nuvem.
* Capacidade de alterar a ordem na qual os componentes de uma função definidos pelo usuário são processados, por meio da adição de botões **Mover para cima** e **Mover para baixo** na seção **Componentes** das **Propriedades de Função do Azure**.
* Uma atualização para o **Pacote para bibliotecas do Azure para Java** , com base na versão 0.4.0 da [API de cliente do Microsoft Azure].

### <a name="november-5-2012"></a>5 de novembro de 2012
O Plug-in do Azure para Eclipse, versão de Visualização de novembro de 2012, foi lançado. Esta é uma atualização importante que inclui vários recursos novos, bem como correções de bugs adicionais e aprimoramentos de uso gerados por comentários desde a versão de Visualização de setembro de 2012:

* Suporte para Microsoft Windows Server 2012 como o sistema operacional em nuvem.
* Suporte para caching colocalizado do Azure para clientes em cache de memória.
* Inclusão de bibliotecas de cliente Apache Qpid JMS para aproveitar as mensagens com base em AMQP do Azure.
* Um assistente aprimorado de **Novo Projeto** , com uma nova página no final que fornece aos usuários a capacidade de habilitar rapidamente vários recursos importantes comuns em seu projeto: sessões temporárias, caching e depuração remota.
* Redução automática de instâncias de função para 1 em execução no emulador de computação, a fim de evitar conflitos de associação de porta entre instâncias do servidor.

### <a name="september-28-2012"></a>28 de setembro de 2012
O Plug-in do Azure para Eclipse, versão de Visualização de setembro de 2012, foi lançado. Essa atualização de serviço inclui várias correções de bugs adicionais desde a versão de Visualização de agosto de 2012, bem como alguns aprimoramentos de uso gerados por comentários em recursos existentes:

* Suporte para Microsoft Windows 8 e Microsoft Windows Server 2012 como o sistema operacional de desenvolvimento, solucionando problemas que anteriormente impediam o funcionamento correto do plug-in nesses sistemas operacionais.
* Suporte aprimorado para especificar os intervalos de porta de ponto de extremidade.
* Correções de bugs relacionados aos caminhos de arquivos que contenham espaços.
* Aprimoramentos no menu de contexto de função para acesso mais rápido a configurações específicas de função.
* Aprimoramentos secundários no assistente **Publicar na nuvem** e diversas correções de bugs adicionais.

### <a name="august-28-2012"></a>28 de agosto 2012
O Plug-in do Azure para Eclipse, versão de Visualização de agosto de 2012, foi lançado. Essa atualização de serviço inclui correções de bugs adicionais desde a versão de Visualização de julho de 2012, bem como alguns aprimoramentos de uso gerados por comentários para recursos existentes:

* Na caixa de diálogo Filtro de Serviços de Controle de Acesso do Azure:
  * **Opção para incorporar o certificado de autenticação** em seu arquivo WAR do aplicativo, para simplificar a implantação em nuvem.
  * **Opção para criar um certificado autoassinado** na interface de usuário do filtro ACS. Para saber mais sobre o Filtro de Serviços de Controle de Acesso do Azure, confira [Como autenticar usuários da Web com o Serviço de Controle de Acesso do Azure usando o Eclipse].
* No assistente de Projeto de Implantação do Azure (também se aplica à página de propriedades de Configuração do Servidor da função):
  * **Descoberta automática do local do JDK** em seu computador (que pode ser substituído se for desejado).
  * **Detecção automática de tipo de servidor** quando você seleciona o diretório de instalação do servidor de aplicativo.

### <a name="july-15-2012"></a>15 de julho de 2012
O Plug-in do Azure para Eclipse, versão de Visualização de julho de 2012, que soluciona vários bugs de prioridade mais altas encontrados e/ou relatados por usuários após a versão de junho de 2012, foi lançado. Essa é apenas uma atualização de serviço e não há qualquer recurso novo.

### <a name="june-7-2012"></a>7 de junho de 2012
O Plug-in do Azure para Eclipse, CTP de junho de 2012, foi lançado. Os novos recursos incluem:

* **Novo assistente de projeto de implantação do Azure:** permite que você selecione seu JDK, servidor de aplicativos Java e aplicativos Java diretamente na interface de usuário aprimorada do assistente. Foram incluídos na lista de configurações do servidor nativas para sua escolha o Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 e JBoss 7 (autônomo). Além disso, você pode personalizar a lista de configurações do servidor. Esse aprimoramento da interface de usuário é uma alternativa à ação de arrastar e soltar arquivos compactados e copiar os scripts de inicialização, que era a abordagem principal. Esse método ainda funciona bem, mas provavelmente será usado apenas para cenários mais avançados.
* **Página de propriedades de função do Servidor de Configuração:** permite que você alterne facilmente os JDKs, servidores de aplicativos Java e aplicativos associados à sua implantação após a criação do projeto. Para saber mais, confira [Propriedades de configuração do servidor].
* **Assistente &quot;Publicar em nuvem&quot;:** fornece uma maneira fácil de implantar seu projeto no Azure diretamente do Eclipse, automatizando o trabalho manual pesado de obtenção de credenciais, entrada no Portal de Gerenciamento do Azure, carregamento de um pacote etc. Para obter um exemplo de como implantar o projeto diretamente no Azure, confira [Criação de um aplicativo Hello World do Azure no Eclipse].
* **Barra de ferramentas do Azure:** agora uma barra de ferramentas do Azure está disponível no Eclipse contendo botões que chamam os seguintes recursos:
  * ![][ic710879] **Executar no Emulador do Azure**: executa o projeto no emulador.
  * ![][ic710880] **Redefinir Emulador do Azure**: redefine o emulador.
  * ![][ic710881] **Compilar pacote para nuvem do Azure**: compila o pacote para implantação.
  * ![][ic710876] **Novo projeto de implantação do Azure**: cria um novo projeto de implantação do Azure.
  * ![][ic710882] **Publicar na Nuvem do Azure**: publica seu projeto no Azure.
  * ![][ic710883] **Cancelar publicação**: exclui a implantação.
  * Muitos desses botões da barra de ferramentas do Azure são usados na [Criação de um aplicativo Hello World do Azure no Eclipse].
* **Bibliotecas do Azure para Java:** agora estão disponíveis como parte do Pacote individual para Bibliotecas do Azure para a biblioteca Java no Eclipse, acompanhando a instalação do plug-in e contendo todas as dependências necessárias. Basta adicionar uma referência à biblioteca em seu projeto Java, e não é necessário baixar nada separadamente. Para saber mais, confira [Instalação do Kit de Ferramentas do Azure para Eclipse].
* **Microsoft JDBC Driver 4.0 para SQL Server disponível durante a instalação do plug-in:** durante a instalação do novo plug-in, a versão mais recente do Microsoft JDBC Driver para SQL Server pode ser instalada.
* **Filtro do Serviço de Controle de Acesso do Azure disponível durante a instalação do plug-in:** esse novo componente, incluído como uma biblioteca do Eclipse no kit de ferramentas, permite que seu aplicativo Web Java aproveite perfeitamente a autenticação ACS (Serviço de Controle de Acesso) do Azure usando vários provedores de identidade, como Google, Live.com e Yahoo!. Você não precisa escrever uma lógica de autenticação por conta própria, apenas configurar algumas opções e deixar o filtro fazer o trabalho pesado de permitir que os usuários façam logon usando ACS. Você pode se concentrar apenas em escrever o código que fornece aos usuários acesso aos recursos com base na identidade deles, conforme retorna ao seu aplicativo pelo filtro dentro do objeto de solicitação. Para obter um tutorial sobre como usar o filtro, confira [Como autenticar usuários da Web com o Serviço de Controle de Acesso do Azure usando o Eclipse].
* **Detecção automática do pré-requisito do SDK 1.7 do Azure:** quando você cria um novo projeto de implantação do Azure, o SDK 1.7 do Azure é baixado automaticamente, caso ainda não esteja instalado.
* **Pontos de extremidade de instância:** permite acesso direto ao ponto de extremidade de porta para comunicação com instâncias de função com carga balanceada. Os pontos de extremidade de instância podem ser adicionados pela interface de usuário dos pontos de extremidade, disponível na página [Propriedades de pontos de extremidade] . Isso ajuda a habilitar a depuração remota e o diagnóstico de JMX para determinadas instâncias de computação em execução na nuvem em cenários de implantações com várias instâncias. 
* **Interface de usuário dos componentes:** facilita, para os usuários avançados, a configuração de dependências de projeto entre funções individuais do Azure no projeto e outros recursos externos, como projetos de aplicativo Java; também facilita a descrição de suas lógicas de implantação. Para saber mais, consulte as [Propriedades dos componentes].
* **Atualização automática de versões anteriores de projetos:** quando você abre um espaço de trabalho que possui um projeto do Azure criado com uma versão anterior do plug-in, os projetos antigos aparecerão no Eclipse como fechados, pois as versões anteriores dos projetos não são compatíveis com a nova versão. Se você tentar abrir um desses projetos antigos, um assistente de atualização será iniciado. Se você concordar com a atualização, um novo projeto com **_Upgraded** anexado ao nome será criado e atualizado automaticamente a fim de funcionar com a nova versão. Você pode renomear o novo projeto conforme o necessário. Como parte da atualização, seu projeto original não será modificado (e permanecerá fechado).

### <a name="december-10-2011"></a>10 de dezembro de 2011
O plug-in do Azure para Eclipse, CTP de dezembro de 2011 foi lançado. Os novos recursos incluem:

* **Suporte para afinidade da sessão (&quot;sessão temporária&quot;):** ajudando a habilitar aplicativos Java com estado e em cluster com apenas uma caixa de seleção. Para saber mais, confira [Afinidade da sessão].
* **Exemplos de script de inicialização pré-criados :** para os servidores Java mais populares (Tomcat, Jetty, JBoss, GlassFish), que você pode simplesmente copiar/colar do diretório de exemplos do projeto em seu script de inicialização.
* **Saída de inicialização do emulador em tempo real:** agora você pode assistir à execução de todas as etapas de seu script de inicialização em uma janela de console dedicada, mostrando o andamento e as falhas no script conforme ele é executado pelo Azure.
* **Monitoramento leve e automático de java.exe:** que forçará uma reciclagem de função quando o java.exe deixar de ser executado, usando um script leve e predefinido incluído automaticamente em sua implantação.
* **Interface de usuário de configuração remota de depuração do aplicativo Java:** com ela você pode permitir facilmente o acesso do depurador remoto do Eclipse ao seu aplicativo Java em execução no Emulador ou na nuvem do Azure, para que você consiga percorrer e depurar seu código Java em tempo real. Para saber mais, confira [Debugging Azure Applications in Eclipse].
* **Interface de usuário de configuração do recurso de armazenamento local:** para que você não precise mais configurar recursos locais manipulando diretamente o XML. Este recurso também permite que você acesse o caminho do arquivo efetivo de seu recurso local após a implantação por meio de uma variável de ambiente, à qual você pode fazer referência diretamente de seu script de inicialização. Para saber mais, confira [Propriedades de armazenamento local].
* **Interface do usuário de configuração da variável do ambiente:** para que você não precise mais definir variáveis do ambiente por meio da edição manual do XML de configuração. Para saber mais, confira [Propriedades de variáveis do ambiente].
* **Driver JDBC para o SQL Azure:** é instalado por meio do plug-in como uma biblioteca do Eclipse totalmente integrada, permitindo uma programação mais fácil no SQL Azure. 
* **Acesso rápido de menu de contexto à interface de usuário de configuração de função**: apenas clique com o botão direito na pasta da função e clique em **Propriedades**.
* **Ícones personalizados de pasta de função e de projeto do Azure:** para obter melhor visibilidade e facilitar a navegação em seu espaço de trabalho e projeto.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Kit de Ferramentas do Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Instalação do Kit de Ferramentas do Azure para Eclipse]: azure-toolkit-for-eclipse-installation.md

[Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse]: azure-toolkit-for-eclipse-sign-in-instructions.md
[Como publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[Gerenciar Máquinas Virtuais usando o Azure Explorer para Eclipse]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[página da Web do Azul Systems para o Zulu OpenJDK]: http://go.microsoft.com/fwlink/?LinkId=402457
[Ponto de extremidade de serviço do Azure]: http://go.microsoft.com/fwlink/?LinkID=699526
[Lista de contas de armazenamento do Azure]: http://go.microsoft.com/fwlink/?LinkID=699528
[Propriedades dos componentes]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Criação de um aplicativo Hello World do Azure no Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Implantações de grande porte]: http://go.microsoft.com/fwlink/?LinkID=699536
[Propriedades de pontos de extremidade]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[Propriedades de variáveis do ambiente]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Plug-in das Ferramentas do HDInsight para Eclipse]: /azure/hdinsight/hdinsight-apache-spark-eclipse-tool-plugin
[Como autenticar usuários da Web com o Serviço de Controle de Acesso do Azure usando o Eclipse]: http://go.microsoft.com/fwlink/?LinkID=264703
[Como usar o descarregamento de SSL]: http://go.microsoft.com/fwlink/?LinkID=699545
[Propriedades de armazenamento local]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[API de cliente do Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=280397
[Propriedades de configuração do servidor]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[Afinidade da sessão]: http://go.microsoft.com/fwlink/?LinkID=699548
[Descarregamento de SSL]: http://go.microsoft.com/fwlink/?LinkID=699549
[Para criar uma nova conta de armazenamento]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Tamanhos de máquina virtual e serviço de nuvem para o Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
