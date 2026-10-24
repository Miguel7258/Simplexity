<p align="center">
  <img width="128" height="128" alt="Simplexity" src="docs/assets/simplexity-logo.jpg" />
</p>

<h1 align="center">Simplexity</h1>

<p align="center">
  <strong>Um assistente de IA local que trabalha no teu PC.</strong><br />
  Lê e cria ficheiros, escreve e executa scripts e diagnostica o Windows com modelos abertos, dos pequenos aos grandes MoE.<br />
  Funciona offline, sem contas e sem subscrições.
</p>

<p align="center">
  <a href="https://miguel7258.github.io/Simplexity/">Site</a> •
  <img src="https://img.shields.io/badge/estado-em%20desenvolvimento-orange?style=flat-square" alt="Em desenvolvimento" />
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-0078D6?style=flat-square" alt="Windows 10 e 11" />
  <img src="https://img.shields.io/badge/licença-MIT-green?style=flat-square" alt="Licença MIT" />
</p>

---

## O que é

O Simplexity é uma aplicação para Windows que corre modelos de linguagem abertos (formato GGUF, via `llama.cpp`) diretamente no teu computador e os usa como **agente**: em vez de só responder, faz a tarefa e confirma o resultado.

A ideia é dar a qualquer pessoa uma IA capaz de ajudar no dia a dia do PC, sem internet obrigatória, sem enviar dados para servidores e sem pagar subscrições, mesmo num computador com uma GPU de 8 GB. Funciona com modelos pequenos (4B a 9B) e também com modelos MoE grandes, como a Gemma 4 26B ou o Qwen3.6 35B.

Exemplos do que lhe podes pedir:

- «Cria um `backup.bat` que copie a pasta Documentos para `D:\Backup` com a data no nome, e testa-o.»
- «O `com_erro.py` dá erro quando o executo. Descobre o problema e corrige-o.»
- «Porque é que o meu disco C: está quase cheio? Só diagnóstico, não alteres nada.»
- «Lê o `vendas.csv` e cria um resumo com o total por vendedor.»

## Como funciona

- **Projetos com permissões.** O agente só trabalha nas pastas que autorizas. Comandos de leitura correm logo; tudo o que escreve, apaga ou altera o sistema só acontece quando o pedes.
- **Harness Cognitivo.** Um orquestrador próprio guia o modelo passo a passo: escolhe as ferramentas que cada pedido justifica, verifica cada resultado no disco, deteta repetições e reaproveita a cache do modelo (KV cache) para responder mais depressa numa GPU modesta.
- **Modelos MoE grandes numa GPU de 8 GB.** Nos modelos *Mixture of Experts*, o Simplexity lê a estrutura do ficheiro GGUF, mantém o essencial na GPU e põe os especialistas na RAM, escolhendo automaticamente a divisão que cabe no teu sistema.
- **Respostas honestas.** O Simplexity só dá uma ação como feita quando uma ferramenta a confirmou. Se algo falhar, diz o que falhou.
- **Privacidade.** Modelos, conversas, memória e ficheiros ficam no teu computador. Não há telemetria. A pesquisa na web é opcional e só acontece quando a pedes.
- **Memória editável.** O agente guarda preferências e factos em ficheiros Markdown que podes ler e editar.
- **Explorador Hugging Face.** Pesquisa e transfere modelos GGUF compatíveis a partir da aplicação.

## Estado

O Simplexity está em desenvolvimento ativo e **ainda não tem uma versão pública**. O suporte a modelos MoE grandes está a ser desenvolvido neste momento. Quando a primeira versão sair, ficará disponível em [Releases](https://github.com/Miguel7258/Simplexity/releases) como instalador (`.exe`) e versão portátil (`.zip`).

## Requisitos previstos

| | Mínimo | Recomendado |
| :--- | :--- | :--- |
| **Sistema** | Windows 10 / 11, 64 bits | Windows 11, 64 bits |
| **Processador** | x64 com 4 núcleos | 6 núcleos ou mais |
| **Memória RAM** | 8 GB (modelos de 4B, só CPU) | 16 GB (32 GB para MoE de 26B–35B) |
| **GPU** | Opcional | NVIDIA com 8 GB de VRAM (ex.: RTX 3060/4060/5050) |
| **Disco** | 10 GB livres (programa + 1 modelo) | SSD NVMe |

## Tecnologias

- **Aplicação:** [Tauri v2](https://tauri.app/) (Rust), React, TypeScript, Tailwind CSS
- **Backend local:** Python 3.11, FastAPI
- **Inferência:** [llama.cpp](https://github.com/ggml-org/llama.cpp) (`llama-server`), com CPU, NVIDIA CUDA e Intel Arc (SYCL)

## Licença

Distribuído sob a licença MIT. Consulta o ficheiro [`LICENSE`](LICENSE).

Desenvolvido por **Miguel**.
