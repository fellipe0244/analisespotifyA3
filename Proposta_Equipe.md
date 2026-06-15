## Proposta da equipe e vantagens:

Sugerimos **uma arquitetura híbrida**, combinando o processamento batch semanal com uma camada de ajuste quase em tempo real.

A ideia é manter o processamento principal em lote, pois ele é eficiente para calcular recomendações em grande escala. Porém, durante a semana, o sistema poderia atualizar parcialmente a recomendação com base em eventos recentes do usuário, como músicas puladas, curtidas, artistas pesquisados ou playlists salvas.
Para isso, poderia ser usada uma estrutura de dados baseada em fila de eventos, na qual cada interação relevante do usuário é registrada. Esses eventos seriam processados por uma camada mais leve de streaming, responsável por ajustar a prioridade das músicas recomendadas.

Além disso, o grupo propõe o uso de uma estrutura de fila de prioridade para organizar as músicas candidatas. Cada música receberia uma pontuação baseada em critérios como similaridade com o perfil do usuário, popularidade entre usuários parecidos, novidade e chance de aceitação. As músicas com maior pontuação ficariam no topo da fila.
Essa solução não substituiria o algoritmo principal do Spotify, mas poderia melhorar a adaptação da playlist ao comportamento recente do usuário.

## Limitações da proposta:

A principal limitação é o aumento da complexidade da arquitetura. O sistema passaria a depender não apenas do processamento batch, mas também de uma camada de eventos em tempo quase real.
Outro desafio seria o custo computacional. Processar eventos recentes de milhões de usuários exige infraestrutura robusta e pode aumentar o consumo de memória, processamento e armazenamento.
Também existe o risco de o sistema reagir rápido demais a comportamentos temporários. Por exemplo, se o usuário ouvir uma música fora do seu gosto apenas uma vez, o algoritmo não deve mudar completamente suas recomendações.
