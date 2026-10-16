# vigia-render

Robô que **acorda e mantém acordadas** as APIs no plano grátis do Render durante a
janela de uso (dias úteis, 9h–18h, horário de Brasília).

Por que existe: o Render põe o serviço grátis para dormir após 15 min sem uso e,
quando ele está dormindo, **recusa acordá-lo para serviços de ping** como o
cron-job.org (responde `503` com `x-render-routing: hibernate-wake-error`).
Um robô do GitHub Actions é aceito. Então o cron-job.org só dispara este robô,
e o robô faz os pings.

Como funciona:

1. O cron-job.org chama a API do GitHub às **8h50** e às **14h40**
   (seg–sex), disparando o workflow `vigia.yml`.
2. O workflow roda por até 6 h chamando as rotas leves das APIs a cada 10 min.
3. Fora da janela, os sites mostram a tela "Acordando o servidor" (35–50 s).

Rotas chamadas (todas públicas e sem dados):

- https://alugueis-api.onrender.com/healthz/
- https://planejador-api.onrender.com/healthz/
- https://brazai-api.onrender.com/api/v1/public/menu/atelier-gastronomico/
