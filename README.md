# Case Study: Android Security Controls & Application Isolation

Este repositório documenta uma análise técnica de segurança defensiva (AppSec / Blue Team) focada nos mecanismos de proteção do sistema operacional Android[span_0](start_span)[span_0](end_span). O objetivo é demonstrar a eficácia da *sandbox* do sistema, o isolamento do ecossistema de *Content Providers* e o tratamento seguro de exceções de E/S (*Input/Output*) em tempo de execução[span_1](start_span)[span_1](end_span).

---

## 1. Isolamento de Content Providers (`exported="false"`)

### Cenário de Teste
Simulação de uma tentativa de acesso *cross-app* não autorizado, onde um aplicativo gerenciador de arquivos de terceiros (`me.zhanghai.android.files`) solicita a leitura de um recurso mantido por um provedor interno restrito (`com.google.android.apps.nbu.files.provider`)[span_2](start_span)[span_2](end_span).

### Evidência Técnica (Stack Trace)
A tentativa de leitura acionou a restrição de segurança no nível do kernel e do runtime, gerando a seguinte exceção[span_3](start_span)[span_3](end_span):

```text
java.lang.SecurityException: Permission Denial: 
opening provider com.google.android.libraries.storage.storagelib.FileProvider 
from ProcessRecord{...} (pid=..., uid=10382) 
that is not exported from UID 10173

